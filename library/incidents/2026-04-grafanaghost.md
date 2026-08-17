---
title: "2026 04 grafanaghost"
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

# 2026 04 grafanaghost

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2026 年 4 月，安全公司 Noma Security 披露了一个名为"GrafanaGhost"的提示注入+数据外泄漏洞（CVE-2026-27876）。攻击者通过诱导 Grafana 的 AI 助手渲染外部图片，在图片 URL 参数中嵌入企业敏感数据（如用户信息、Token 等）。当 Grafana 向外部服务器请求图片时，URL 中的敏感数据随之外泄。该漏洞利用了 Grafana 图片渲染功能中对外部 URL 参数缺乏过滤的设计缺陷。Grafana 团队在收到报告后进行了部分修复。

## 来源

- 一手来源：https://noma.security/blog/grafana-ghost/
- 核验状态：✅ 证实（V48）
