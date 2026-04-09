# OpenClaw Skills

为 [OpenClaw](https://github.com/diwuwudi123/openclaw-skills) 打造的技能集合，让 AI 助手能够执行各种实用任务。

## 技能列表

### 微信公众号发布

**目录**: `wechat-article-mulit-publisher/`

从 Markdown 文件或网页链接提取文章并发布到微信公众号。

#### 功能特性

- 多账号支持：通过 `--account` 指定发布到哪个公众号
- 两种排版模板：`standard`（科技风格）和 `viral`（高传播风格）
- 自动生成封面图（无本地图片时）
- 文章内图片自动上传：自动将文章中的图片上传到微信素材库并替换为微信 CDN URL
- 草稿管理：支持列出草稿列表、删除草稿
- 素材管理：支持单独上传图片到素材库（本地文件或网络 URL）
- 支持 `--dry-run` 预览
- 支持直接发布草稿 `--publish`

#### 安装

```bash
cd wechat-article-mulit-publisher
pip install -r scripts/requirements.txt
```

#### 配置

编辑 `config.json`：

```json
{
  "default_account": "your_account",
  "accounts": {
    "your_account": {
      "name": "公众号名称",
      "app_id": "wx...",
      "app_secret": "...",
      "author": "作者",
      "default_template": "standard"
    }
  }
}
```

#### 使用方法

```bash
# 列出所有已配置的账号
python scripts/publish_wechat.py --list-accounts

# 预览（不调用微信 API）
python scripts/publish_wechat.py <文章.md> --dry-run

# 发布到默认账号
python scripts/publish_wechat.py <文章.md>

# 发布到指定账号
python scripts/publish_wechat.py <文章.md> --account account2

# 直接发布（跳过草稿直接发布）
python scripts/publish_wechat.py <文章.md> --publish --status

# 列出草稿箱
python scripts/publish_wechat.py --list-drafts

# 删除草稿
python scripts/publish_wechat.py --delete-draft <media_id>

# 上传本地图片到素材库
python scripts/publish_wechat.py --upload-material /path/to/image.jpg

# 上传网络图片到素材库
python scripts/publish_wechat.py --upload-material-url https://example.com/image.jpg
```

#### 命令行参数

| 参数              | 说明                            |
| ----------------- | ------------------------------- |
| `--account`       | 指定公众号账号（账号标识名）    |
| `--list-accounts` | 列出所有已配置的账号            |
| `--template`      | 覆盖模板：`standard` 或 `viral` |
| `--author`        | 覆盖作者名                      |
| `--cover-image`   | 指定本地封面图路径              |
| `--source-url`    | 覆盖原文链接                    |
| `--dry-run`       | 仅渲染预览，不调用微信 API      |
| `--publish`       | 草稿创建后直接提交发布          |
| `--status`        | 查询发布状态                    |
| `--list-drafts`   | 列出草稿箱中的所有草稿          |
| `--delete-draft`  | 删除指定 media_id 的草稿        |
| `--upload-material` | 上传本地图片到素材库（传入图片路径） |
| `--upload-material-url` | 上传网络图片到素材库（传入图片URL） |

---

## 贡献

欢迎提交新的技能！请确保：

1. 每个技能有独立的目录
2. 包含 `SKILL.md` 描述文件
3. 提供清晰的安装和使用说明
4. 包含 `requirements.txt`（如有依赖）

## 目录结构

```
openclaw-skills/
├── README.md
├── wechat-article-mulit-publisher/
│   ├── SKILL.md           # 技能描述
│   ├── config.json         # 配置文件
│   └── scripts/
│       ├── publish_wechat.py
│       └── requirements.txt
└── <future-skills>/
```

## License

MIT
