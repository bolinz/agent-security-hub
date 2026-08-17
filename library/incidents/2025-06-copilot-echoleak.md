---
title: Microsoft 365 Copilot EchoLeak（CVE-2025-32711）
date: "2025.06"
type: 间接注入/越权
severity: critical
status: 已证实
impact: 零点击提示注入导致数据外泄，CVSS 9.3
last_updated: 2026-08-18
tags: [提示注入, Copilot, EchoLeak, CVE-2025-32711, 数据外泄]
related_cves: [CVE-2025-32711]
related_reports: [04-incidents.md]
---

# Microsoft 365 Copilot EchoLeak（CVE-2025-32711）

## 事件概述

- **时间**：2025.06
- **类型**：间接注入/越权
- **影响对象**：Microsoft 365 Copilot
- **影响**：零点击提示注入导致数据外泄，CVSS 评分 9.3
- **状态**：已证实

## 经过

2025 年 6 月，Microsoft 365 Copilot 曝出 "EchoLeak" 漏洞（CVE-2025-32711），攻击者可通过零点击提示注入实现数据外泄，CVSS 评分 9.3。该漏洞已被修复。

## 影响与损失

零点击提示注入可导致数据外泄，CVSS 评分 9.3；漏洞已修复。

## 来源

- 一手来源 URL：https://nvd.nist.gov/vuln/detail/CVE-2025-32711
- 核验状态：✅ 证实（V40）