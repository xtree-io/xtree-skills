---
name: xtree-wechat-accounts-by-owner
description: >-
  Live-search WeChat official accounts by owner/entity name via XTREE.
  Use for raw account hits under a legal or brand name — not rankings or BI.
---

# XTREE · 按主体搜号

按**主体名 / 运营主体**实时搜公众号，返回原始命中。不要做排行或声量结论。

## 前置

- MCP `xtree` + `XTREE_API_KEY`
- 用户提供主体名称（公司名、品牌名等），不要空字符串
- 钱包有余额：https://www.xtree.io/catalog

## Tools

| 需求 | MCP tool | 计费 slug |
|------|----------|-----------|
| 按主体实时搜号 | `wechat_accounts_search_by_owner_live` | `wechat.accounts.search-by-owner-live` |

参数：`owner_name` + `page`（从 1 起）。翻页规则以响应为准（无 session 时递增 `page` 直到空列表）。

## 与搜一搜的区别

- 关键词搜号 → `xtree-wechat-search`（`wechat_search_accounts`）
- **主体名下**搜号 → 本技能
- 拿到 `gh_id` 后拉历史发文 → `xtree-wechat-accounts-posts`

## 失败与计费

- 主体名无效 / 无结果：如实告知，勿反复空打。
- 余额不足 → https://www.xtree.io 充值。
- 本技能通常**一盘一接口**；后续拉发文 / 阅读数另计。

## 输出

返回原始账号字段 + 费用 meta。禁止编造粉丝数。

## Call

- Access: the MCP tool names in this file, or the Python SDK (`pip install xtree-sdk`).
- Auth: `XTREE_API_KEY` (request header `X-XTREE-Key`).
- Pagination: follow this file. Do not invent a cursor or session the response did not return.
- Billing: each call debits the user's wallet. Incomplete delivery is not billed. On 401 or insufficient balance, send the user to https://www.xtree.io. Do not use another key.
