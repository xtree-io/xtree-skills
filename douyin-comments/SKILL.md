---
name: xtree-douyin-comments
description: >-
  Fetch video comments for engagement scouting.
---

# XTREE · 抖音评论

用顾客自己的 XTREE API Key，通过 REST 或 Python SDK 拉取**原始数据**。公开的 MCP 目前只注册微信工具，本技能不在其中。不要生成标题、不要做爆款分析。

官网详情：https://www.xtree.io/skills/douyin-comments

## 前置

- 环境变量 `XTREE_API_KEY`。Python：`pip install xtree-sdk`，或调用 REST `https://api.xtree.io/api`
- 钱包有余额；单价见 https://www.xtree.io/catalog

## 计费 slug

| slug |
|------|
| `douyin.videos.comments` |
| `douyin.videos.sub-comments` |

## 失败与计费

- 余额不足 / 401：提示用户到 https://www.xtree.io 充值或检查 Key；**不要**改用他人 Key。
- 交付不完整：说明哪一步缺数据；残缺交付通常不计费，以响应 `meta` 为准。
- 组合技能可能一次对话打多个 slug。

## 输出给用户

只给结构化字段与费用 meta；结论与运营建议留给用户自己写。

## Call

- Access: REST `https://api.xtree.io/api` or the Python SDK (`pip install xtree-sdk`). This skill is not an MCP tool. The public MCP server currently registers WeChat tools only.
- Auth: `XTREE_API_KEY` (request header `X-XTREE-Key`).
- Slugs: `douyin.videos.comments`, `douyin.videos.sub-comments`
- Billing: each call debits the user's wallet. Incomplete delivery is not billed. On 401 or insufficient balance, send the user to https://www.xtree.io. Do not use another key.
