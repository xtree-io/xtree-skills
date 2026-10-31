---
name: xtree-wechat-accounts-posts
description: >-
  Fetch WeChat official-account historical posts via XTREE by gh_id (account_id).
  Use for raw post lists and pagination — not summaries or content rewriting.
---

# XTREE · 公众号历史发文

按公众号 `gh_id` 拉取**历史发文列表**原始数据。不要写摘要、不要改写正文。

## 前置

- MCP `xtree` + `XTREE_API_KEY`
- 已知目标号的 `gh_id`（可先用搜一搜 / 按主体搜号拿到）
- 钱包有余额：https://www.xtree.io/catalog

## Tools

| 需求 | MCP tool | 计费 slug |
|------|----------|-----------|
| 历史发文列表 | `wechat_accounts_posts` | `wechat.accounts.posts` |

参数：`account_id` 当前传 `gh_id`；翻页回传 `data.next_cursor` 作为下一轮 `cursor`，并递增 `page`。

Python：`client.wechat.accounts.posts(account_id=..., page=1)`（以 SDK 为准）。

## 推荐流程

1. 若用户只有名称：先 `xtree-wechat-search` 或 `xtree-wechat-accounts-by-owner` 找到 `gh_id`（另计费）。
2. 再调本技能拉列表。
3. 需要阅读互动时，对单篇 URL 用 `xtree-wechat-articles-metrics`（另计费）。

## 失败与计费

- 缺 `gh_id`：说明原因，勿空打。
- 余额不足 / 401 → 引导充值；不要改用他人 Key。
- 交付 `limited`：如实展示已有字段。

## 输出

返回原始列表字段 + `meta` 费用。禁止编造未返回的阅读数。

## Call

- Access: the MCP tool names in this file, or the Python SDK (`pip install "git+https://github.com/xtree-io/xtree-python.git"`).
- Auth: `XTREE_API_KEY` (request header `X-XTREE-Key`).
- Pagination: follow this file. Do not invent a cursor or session the response did not return.
- Billing: each call debits the user's wallet. Incomplete delivery is not billed. On 401 or insufficient balance, send the user to https://www.xtree.io. Do not use another key.
