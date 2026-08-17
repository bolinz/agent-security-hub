---
title: "2023 02 bing chat 间接注入"
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

# 2023 02 bing chat 间接注入

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2023 年 2-3 月，多个安全研究者独立发现 Microsoft Bing Chat（代号 Sydney）存在间接提示注入漏洞。Greshake 等人在论文 *Not what you've signed up for* 中首次系统化提出间接注入概念并以 Bing Chat 为主要演示目标。攻击者可在网页中插入隐藏指令（白色文字），当 Bing Chat 读取该网页时，隐藏指令会覆盖系统提示，操控对话输出。这是**间接提示注入（Indirect Prompt Injection）**概念的首次公开实证。

## 来源

- 论文（一手来源）：Greshake et al., *Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection*, https://arxiv.org/abs/2302.12173
- Microsoft 官方文档：https://learn.microsoft.com/en-us/security/zero-trust/catalog-ai-attack-techniques/prompt-injection
- 核验状态：✅ 证实（V33）
