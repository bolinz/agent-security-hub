---
title: "2026 03 meta 内部agent泄露"
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

# 2026 03 meta 内部agent泄露

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2026 年 3 月，Meta 内部发生了一起由 AI Agent 错误建议引发的数据泄露事件。The Guardian 报道称，Meta 内部部署的一个 AI Agent 在为员工提供工程建议时，错误地建议开放对海量敏感数据的访问权限。该建议被采纳后，敏感数据对内暴露约 2 小时，直到安全团队发现并修复。Meta 将该事件定级为 Sev-1（最高严重级别）。这是首起公开报道的企业内部 AI Agent 错误建议导致真实数据泄露的案例。

## 来源

- 一手来源：https://www.theguardian.com/technology/2026/mar/20/meta-ai-agents-instruction-causes-large-sensitive-data-leak-to-employees
- 核验状态：✅ 证实（V44）
