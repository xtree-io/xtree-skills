---
name: xtree-wechat-search
description: >-
  Fetch WeChat (搜一搜) raw search results via XTREE: articles, videos, or accounts
  by keyword. Use when the user wants WeChat search data, mp.weixin article hits,
  or account search — not copywriting or analytics conclusions.
---

# XTREE · 微信搜一搜

用顾客自己的 XTREE API Key，通过 MCP / REST 拉取**原始搜索结果**。不要生成标题、不要做爆款分析。

## 前置

- 已配置 MCP `xtree`（见仓库 README），环境变量 `XTREE_API_KEY`
- 钱包有余额；单价见 https://www.xtree.io/catalog

## 何时用哪个 tool

| 用户意图 | MCP tool | 计费 slug |
|----------|----------|-----------|
| 搜公众号文章 | `wechat_search_articles` | `wechat.search.articles` |
| 搜视频 | `wechat_search_videos` | `wechat.search.videos` |
| 搜账号 | `wechat_search_accounts` | `wechat.search.accounts` |

也可用 Python：`client.wechat.search.articles(keyword=..., page=1)`。

## 翻页

1. 首次调用：`keyword` + `page=1`（不要传空 keyword）。
2. 若响应 `data.session` 非空，下一页把该值原样回传为 `session`，并递增 `page`。
3. 没有 `session` / 列表空 → 说明没有更多页，停止重试。

## 失败与计费

- 余额不足 / 401：提示用户到 https://www.xtree.io 充值或检查 Key；**不要**改用他人 Key。
- 交付不完整（如 `limited`）：说明哪一步缺数据；残缺交付通常不计费，以响应 `meta` 为准。
- 本技能**一盘一接口**；若用户还要阅读数，改用 `xtree-wechat-articles-metrics`。

## 输出给用户

返回结构化原始字段（标题、链接、账号名等），附带本次 `cost_cny` / `balance_cny`（若有）。禁止编造未返回的互动数。
