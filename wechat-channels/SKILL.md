---
name: xtree-wechat-channels
description: >-
  Fetch WeChat Channels (视频号) raw data via XTREE: search channels, list feeds,
  or related channel tools. Use for Channels monitoring and integration — not
  content creation or ranking analysis.
---

# XTREE · 视频号作品与列表

拉取视频号搜索与作品列表的**原始数据**。不要写脚本文案、不要做「爆款结论」。

## 前置

- MCP `xtree` + `XTREE_API_KEY`
- 钱包有余额：https://www.xtree.io/catalog

## 推荐流程

1. **找号**：`wechat_channels_search`（slug `wechat.channels.search`），关键词搜索。
2. 从结果取出 `channel_id`（或文档约定的等价字段）。
3. **拉作品**：`wechat_channels_feeds`（slug `wechat.channels.feeds`），传入 `channel_id`。
4. 需要 id 转换时再用 `wechat_channels_feeds_convert_id`（slug `wechat.channels.feeds.convert-id`）。

Python 对照：

```python
client.wechat.channels.search(keyword="...", page=1)
client.wechat.channels.feeds(channel_id, page=1)
```

## 翻页

与搜一搜相同：下一页回传上一轮 `data.session`，并递增 `page`。无 session / 空列表则停止。

## 计费提示

- 搜索 + 列表是**两次**（或更多）计费调用，事先告知用户「一盘多接口」。
- 余额不足 → 引导充值，不要静默重试打空请求。

## 失败

- 搜到账号但拿不到 `channel_id`：把原始 JSON 关键给用户，请其指定 id，不要猜测。
- 评论 / 下载 URL 等若未在本技能列出，引导用户查 OpenAPI 或换用 REST，不要假装已支持。

## 输出

返回原始列表字段 + `meta` 费用信息。禁止编造播放量或评论内容。

## Call

- Access: the MCP tool names in this file, or the Python SDK (`pip install xtree-sdk`).
- Auth: `XTREE_API_KEY` (request header `X-XTREE-Key`).
- Pagination: follow this file. Do not invent a cursor or session the response did not return.
- Billing: each call debits the user's wallet. Incomplete delivery is not billed. On 401 or insufficient balance, send the user to https://www.xtree.io. Do not use another key.
