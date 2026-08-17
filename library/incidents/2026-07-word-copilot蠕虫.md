---
title: "2026 07 word copilot蠕虫"
date: "2023-02"
type: "间接注入"
severity: "low"
status: "confirmed"
impact: "PoC"
last_updated: "2026-08-17"
tags: [indirect-injection]
related_cves: []
related_reports: ["../reports/04-incidents.md"]
---

# 2026 07 word copilot蠕虫

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2026 年 7 月，安全研究员 Håkon Måløy 负责任披露了一个自复制提示词注入蠕虫，该蠕虫可通过 Microsoft Word 文档在 Copilot 系统间自我传播。攻击者在 Word 文档中嵌入隐藏的提示指令，当 Copilot 处理该文档时，指令会被执行，将恶意提示复制到新生成的文档中，实现自我传播。Simon Willison 报道称，截至 2026 年 7 月披露时，微软已 144 天未给出全类别修复。这是首起公开报道的 AI Agent 蠕虫，证明了自复制注入攻击的可行性。

## 来源

- 一手来源：https://simonwillison.net/2026/Jul/29/ai-worming-through-word/
- 核验状态：✅ 证实（V50）
