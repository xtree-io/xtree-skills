---
name: xtree-xhs-user-notes
description: >-
  Find users and list their notes for portfolio checks.
---

# XTREE · 小红书用户笔记

用顾客自己的 XTREE API Key，通过 MCP / REST 拉取**原始数据**。不要生成标题、不要做爆款分析。

官网详情：https://www.xtree.io/skills/xhs-user-notes

## 前置

- 已配置 MCP `xtree`（见仓库 README），环境变量 `XTREE_API_KEY`
- 钱包有余额；单价见 https://www.xtree.io/catalog

## 计费 slug

| slug |
|------|
| `xhs.users.notes` |
| `xhs.users.profile` |
| `xhs.search.users` |

## 失败与计费

- 余额不足 / 401：提示用户到 https://www.xtree.io 充值或检查 Key；**不要**改用他人 Key。
- 交付不完整：说明哪一步缺数据；残缺交付通常不计费，以响应 `meta` 为准。
- 组合技能可能一次对话打多个 slug。

## 输出给用户

只给结构化字段与费用 meta；结论与运营建议留给用户自己写。
