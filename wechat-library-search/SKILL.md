---
name: xtree-wechat-library-search
description: >-
  Search XTREE WeChat article/account library (ES / Phase 2) by keyword or name.
  Use for historical library hits — not real-time 搜一搜, not analytics conclusions.
---

# XTREE · 文章库与账号库

检索 **ES 灌库** 的文章库 / 账号库原始结果（Phase 2）。不是实时搜一搜；不要做选题或声量分析。

## 前置

- MCP `xtree` + `XTREE_API_KEY`
- 钱包有余额；单价见 https://www.xtree.io/catalog
- 交付状态以 API 目录为准（可能为 `limited`）

## 何时用哪个 tool

| 用户意图 | MCP tool | 计费 slug |
|----------|----------|-----------|
| 关键词搜文章库 | `wechat_library_search_articles` | `wechat.library.articles.search` |
| 分词搜文章库 | `wechat_library_search_articles_tokenized` | `wechat.library.articles.tokenized` |
| 搜账号库 | `wechat_library_search_accounts` | `wechat.library.accounts.search` |
| 库内账号指数/粉丝估计 | `wechat_library_accounts_metrics` | `wechat.library.accounts.metrics` |

翻页用 `page` / `page_size`，**无** `session`。默认先用非分词搜索；用户明确要分词再用 tokenized（**另一次计费**）。

## 与实时搜的区别

- 实时搜一搜 → `xtree-wechat-search`
- 库内历史检索 → 本技能
- 需要单篇实时互动 → `xtree-wechat-articles-metrics`（要有文章 URL）

## 失败与计费

- 组合调用是**一盘多接口**，事先说明。
- 余额不足勿静默重试；`limited` 如实展示。
- 库无命中 ≠ 实时也没有：可建议改用搜一搜。

## 输出

返回库内原始字段 + `meta`。禁止把库指数说成实时粉丝真值。

## Call

- Access: the MCP tool names in this file, or the Python SDK (`pip install "git+https://github.com/xtree-io/xtree-python.git"`).
- Auth: `XTREE_API_KEY` (request header `X-XTREE-Key`).
- Pagination: follow this file. Do not invent a cursor or session the response did not return.
- Billing: each call debits the user's wallet. Incomplete delivery is not billed. On 401 or insufficient balance, send the user to https://www.xtree.io. Do not use another key.
