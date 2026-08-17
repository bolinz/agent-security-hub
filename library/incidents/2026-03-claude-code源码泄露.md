---
title: "2026 03 claude code源码泄露"
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

# 2026 03 claude code源码泄露

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2026 年 3 月 31 日，Anthropic 的 Claude Code 工具 v2.1.88 版本的 npm source map 文件意外暴露了约 51.3 万行源代码。Zscaler ThreatLabz 安全团队于 2026 年 3 月发现并报告了该问题。泄露发生后，攻击者迅速利用该事件创建了多个伪装为"Claude Code 泄露版"的钓鱼 GitHub 仓库，这些仓库实际上分发的是 Vidar 和 GhostSocks 恶意软件。用户如果下载并运行这些伪造仓库中的文件，将感染恶意软件。这是一起典型的"供应链+社会工程"组合攻击。

## 来源

- 一手来源：https://www.zscaler.com/blogs/security-research/anthropic-claude-code-leak
- 核验状态：✅ 证实（V45）
