---
title: "2025 06 copilot echoleak"
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

# 2025 06 copilot echoleak

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2025 年 6 月，安全公司 Aim Security 披露了 Microsoft 365 Copilot 中的一个零点击提示注入漏洞（CVE-2025-32711，CVSS 9.3），命名为"EchoLeak"。攻击者只需向受害者发送一封包含隐藏提示指令的电子邮件，当受害者使用 Copilot 处理该邮件时，隐藏指令会被执行，导致 Copilot 将企业内部敏感数据通过构造的请求外泄给攻击者。整个过程无需用户点击任何链接或执行任何操作（零点击）。微软在收到报告后通过服务器端修复了该漏洞。截至 2026 年 8 月，未见在野利用报告。

## 来源

- NVD：https://nvd.nist.gov/vuln/detail/CVE-2025-32711
- 核验状态：✅ 证实（V40）
