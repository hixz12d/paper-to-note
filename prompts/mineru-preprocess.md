# MinerU 预处理

## 任务

将 PDF 通过 MinerU 转为结构化 Markdown + 图片，供后续分析阶段使用。MinerU 输出的 Markdown 中公式已为 LaTeX 格式、表格已为 HTML 格式，可提升笔记质量并节省 token。

## 模式选择

根据用户的 `--mineru` 参数确定模式：

| 用户输入 | 模式 | 认证 | 适用场景 |
|---------|------|------|---------|
| `--mineru` 或 `--mineru auto` | 自动 | 视检测结果 | 推荐默认 |
| `--mineru light` | 轻量 API | 无需 Token | 零门槛试用，≤20 页论文 |
| `--mineru api` | 精确 API | `MINERU_TOKEN` 环境变量 | 生产使用，长论文（≤600 页） |
| `--mineru local` | 本地 CLI | 无需 | 离线 / 隐私敏感 |

### 自动模式选择逻辑

按以下优先级依次检测：

1. 运行 `mineru --version` → 成功则使用**本地模式**
2. 读取环境变量 `MINERU_TOKEN` → 非空则使用**精确 API 模式**
3. 以上均不可用 → 使用**轻量 API 模式**

## 输出目录

在 PDF 所在目录创建缓存：`{pdf_dir}/.mineru-cache/{pdf_stem}/`

若缓存目录已存在且包含 `.md` 文件，提示用户：
> "检测到已有 MinerU 缓存，是否直接使用？（y = 使用缓存 / 其他 = 重新解析）"

## 各模式执行步骤

### 轻量模式

使用 MinerU Agent Lightweight Parsing API（免 Token，有页数和文件大小限制）。

**API 端点：**
- 提交任务：`POST https://mineru.net/api/v1/agent/parse/file`（multipart/form-data，字段名 `file`）
- 查询结果：`GET https://mineru.net/api/v1/agent/parse/{task_id}`

**步骤：**

1. 通过 Bash 执行 curl 上传 PDF：
   ```bash
   curl -s -X POST "https://mineru.net/api/v1/agent/parse/file" \
     -F "file=@{pdf_path}" \
     -F "enableFormula=true" \
     -F "enableTable=true"
   ```
2. 从响应 JSON 中提取 `task_id`
3. 轮询查询端点，间隔 5 秒，最多轮询 60 次（5 分钟超时）
4. 任务完成后，从结果中获取 Markdown 内容和图片资源 URL
5. 下载 Markdown 和图片到缓存目录

### 精确 API 模式

使用 MinerU Precision Parsing API（需 Token，完整功能）。

**API 端点：**
- 提交任务：`POST https://mineru.net/api/v4/extract/task`
- 查询结果：`GET https://mineru.net/api/v4/extract/task/{task_id}`
- 鉴权头：`Authorization: Bearer {MINERU_TOKEN}`

**步骤：**

1. 检查 `MINERU_TOKEN` 环境变量：
   ```bash
   echo "$MINERU_TOKEN"
   ```
   若为空 → 提示用户："需要设置 MINERU_TOKEN，请前往 https://mineru.net/apiManage/token 获取" → 尝试回退至轻量模式
2. 通过 curl 上传 PDF 并提交任务（添加 `Authorization` 头，参数 `enableFormula=true`, `enableTable=true`）
3. 从响应中提取 `task_id`
4. 轮询查询端点（间隔 5 秒，最多 60 次 / 5 分钟超时）
5. 任务完成后下载结果到缓存目录

### 本地模式

使用本地安装的 MinerU CLI。

**步骤：**

1. 检查可用性：
   ```bash
   mineru --version
   ```
   若失败 → 提示："MinerU 未安装，可通过 `pip install \"mineru[all]\"` 安装" → 回退
2. 执行解析：
   ```bash
   mineru -p "{pdf_path}" -o "{cache_dir}" -l en
   ```
3. 等待完成（视论文长度和硬件，通常 30-120 秒）

## 预处理完成后

缓存目录中应包含：

```
{cache_dir}/
├── {name}.md           # 主 Markdown 文件（公式=LaTeX，表格=HTML）
├── images/             # 提取的图片文件
│   ├── img_0_0.png
│   └── ...
└── content_list.json   # 结构化内容列表（可选参考）
```

执行以下操作：

1. 使用 Read 工具读取 `.md` 文件全文，作为后续阶段的论文内容源
2. 记录 `images/` 目录的完整路径，供阶段 2（Figure 分析）加载图片使用
3. 告知用户："MinerU 预处理完成，已转为结构化 Markdown。"

## 错误处理

| 错误情况 | 处理 |
|---------|------|
| API 超时（轮询超过 5 分钟） | 告知用户，回退至直读 PDF |
| API 返回错误码 | 告知具体错误信息，回退 |
| 文件超出轻量 API 页数限制 | 建议用 `--mineru api` 或 `--mineru local`，回退 |
| Token 未设置（精确 API 模式） | 提示获取地址，尝试轻量模式 |
| `mineru` 命令不存在（本地模式） | 提示安装方式，尝试云 API |
| 网络不可用 | 告知用户，回退 |

**回退统一格式：**
> "MinerU 预处理未成功（{原因}），已回退至 Claude 直读 PDF 模式继续。"
