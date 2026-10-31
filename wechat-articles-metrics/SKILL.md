---
name: xtree-wechat-articles-metrics
description: >-
  Fetch WeChat official-account article engagement metrics (reads, likes,
  looking/wow) via XTREE by public article URL. Use for raw metrics only —
  not sentiment analysis or content rewriting.
---

# XTREE · 公众号阅读互动

按文章 URL 拉取阅读 / 点赞 / 在看等**原始互动数字**。不要写摘要、不要做情感分析。

## 前置

- MCP `xtree` + `XTREE_API_KEY`
- 用户提供可公开访问的文章链接（`https://mp.weixin.qq.com/s/...`）

## Tools

| 需求 | MCP tool | 计费 slug |
|------|----------|-----------|
| 标准互动 | `wechat_articles_metrics` | `wechat.articles.metrics` |
| 增强互动 | `wechat_articles_metrics_pro` | `wechat.articles.metrics-pro` |

默认先用标准接口；用户明确要 pro 字段时再调 pro（**另一次计费**）。

Python：

```python
client.wechat.articles.metrics(url="https://mp.weixin.qq.com/s/...")
client.wechat.articles.metrics_pro(url="https://mp.weixin.qq.com/s/...")
```

## 参数

- 必填：`url`（完整文章链接）。不要用标题模糊匹配去「猜」URL。
- 若用户只有标题：先用 `xtree-wechat-search` 搜到链接，再回来调本技能（两次计费，需说明）。

## 失败与计费

- URL 无效 / 非公众号文：说明原因，勿反复空打。
- 交付 `limited` 或缺字段：如实展示已有字段，标明缺失项。
- 余额不足 → https://www.xtree.io 充值。

## 输出

只输出接口返回的数字与相关元数据 + 本次费用。禁止推算「预计阅读」或改写正文。

## Call

- Access: the MCP tool names in this file, or the Python SDK (`pip install "git+https://github.com/xtree-io/xtree-python.git"`).
- Auth: `XTREE_API_KEY` (request header `X-XTREE-Key`).
- Pagination: follow this file. Do not invent a cursor or session the response did not return.
- Billing: each call debits the user's wallet. Incomplete delivery is not billed. On 401 or insufficient balance, send the user to https://www.xtree.io. Do not use another key.
