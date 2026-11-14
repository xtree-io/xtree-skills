# XTREE Skills（官方 Agent 技能）

面向 Cursor / Claude 等宿主的**可复制 SKILL 包**：教 Agent 如何用 XTREE **取原始数据**，**不**做选题、文案、爆款或运营结论。

微信搜索、视频号、阅读数、历史发文、文章库可以走 [xtree-mcp](https://github.com/xtree-io/xtree-mcp)。其余技能走 REST 或 [Python SDK](https://github.com/xtree-io/xtree-python)。公开的 MCP 还没有这些平台的工具。计费仍是顾客自己的 Key + 钱包，按次扣费。残缺交付不计费。单价见 [API 目录](https://www.xtree.io/catalog)。

官网索引：https://www.xtree.io/skills （含搜索 / 分类 / **真实用量**）。

## 安装前提

1. 在 [xtree.io](https://www.xtree.io/login?tab=signup) 注册并拿到 `XTREE_API_KEY`
2. 微信技能可配置 MCP。其他技能用 REST，或安装 Python SDK：`pip install xtree-sdk`

```json
{
  "mcpServers": {
    "xtree": {
      "command": "uvx",
      "args": ["--from", "git+https://github.com/xtree-io/xtree-mcp.git", "xtree-mcp"],
      "env": { "XTREE_API_KEY": "xt_live_..." }
    }
  }
}
```

3. 将下方某个技能目录复制到宿主 Skills 路径（如 Cursor project `.cursor/skills/`），或按宿主文档引用本仓路径。

## 官方技能

| 目录 | 场景 |
|------|------|
| [wechat-search](wechat-search/) | 微信搜一搜 |
| [wechat-channels](wechat-channels/) | 视频号搜索与作品列表 |
| [wechat-articles-metrics](wechat-articles-metrics/) | 公众号阅读互动 |
| [wechat-accounts-posts](wechat-accounts-posts/) | 公众号历史发文 |
| [wechat-accounts-by-owner](wechat-accounts-by-owner/) | 按主体实时搜号 |
| [wechat-library-search](wechat-library-search/) | 文章库 / 账号库 |
| [wechat-comments](wechat-comments/) | 微信评论 |
| [wechat-article-detail](wechat-article-detail/) | 公众号文章详情 |
| [wechat-channels-metrics](wechat-channels-metrics/) | 视频号作品互动 |
| [douyin-search](douyin-search/) | 抖音搜索 |
| [douyin-creator-insight](douyin-creator-insight/) | 抖音创作者洞察 |
| [douyin-user-posts](douyin-user-posts/) | 抖音用户作品集 |
| [douyin-comments](douyin-comments/) | 抖音评论 |
| [xhs-notes-search](xhs-notes-search/) | 小红书笔记搜索 |
| [xhs-user-notes](xhs-user-notes/) | 小红书用户笔记 |
| [xhs-comments](xhs-comments/) | 小红书评论 |
| [kuaishou-search](kuaishou-search/) | 快手搜索 |
| [kuaishou-hot-board](kuaishou-hot-board/) | 快手热榜 |
| [weibo-search](weibo-search/) | 微博搜索 |
| [weibo-hot-search](weibo-hot-search/) | 微博热搜 |
| [bilibili-search](bilibili-search/) | B站搜索 |
| [bilibili-portfolio](bilibili-portfolio/) | B站账号作品集 |
| [tiktok-search](tiktok-search/) | TikTok 搜索 |
| [tiktok-user-posts](tiktok-user-posts/) | TikTok 用户作品 |
| [youtube-channel](youtube-channel/) | YouTube 频道作品 |
| [taobao-item-search](taobao-item-search/) | 淘宝商品搜索 |
| [video-download](video-download/) | 视频下载解析 |

门户能力见 https://www.xtree.io/catalog （非本仓 SKILL 包）。

## 原则

- 只教取数与翻页；结论留给用户
- 不发明未上架 API
- 不内嵌共享 Key
- 与官网 `/skills/{id}` 一一对应

完整约定见本仓 `docs/06-客户端/Agent技能.md`。
