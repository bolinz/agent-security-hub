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

2026 年 7 月 28 日，挪威安全研究员 Håkon Måløy 公开披露了一个自复制提示词注入蠕虫。该蠕虫利用 Microsoft 365 Copilot for Word 处理源文档时的提示注入漏洞，实现自我传播：攻击者在 Word 文档中嵌入隐藏指令，当 Copilot 处理该文档时，恶意指令被注入到新生成的文档中，形成蠕虫式传播。CyberNews 和 NSFOCUS 均独立报道了该发现。微软安全响应中心（MSRC）与研究员合作 144 天，经历两次补丁尝试和一次模型升级（GPT-5.5→GPT-5.6），截至披露时 Word 侧的蠕虫仍未完全修复。

## 来源

- 研究员披露：Håkon Måløy（2026-07-28）
- CyberNews：https://cybernews.com/security/microsoft-copilot-self-propagating-worm/
- NSFOCUS：https://nsfocusglobal.com/ai-security-incident-case-document-worm-achieves-self-replication-and-propagation-via-word-copilot/
- 核验状态：✅ 证实（V50）
