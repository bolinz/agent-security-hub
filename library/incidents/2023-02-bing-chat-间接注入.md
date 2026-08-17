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

安全研究员 Simon Willison 等人发现，Bing Chat（代号 Sydney）在处理包含隐藏指令的网页内容时，会执行网页中嵌入的恶意提示词，而非用户的真实意图。攻击者可在网页中插入白色文字（用户不可见），当 Bing Chat 读取该网页时，隐藏指令会覆盖系统提示，操控对话输出。这是**间接提示注入（Indirect Prompt Injection）**概念的首次公开实证，由 Greshake 等人在论文 *Not what you've signed up for* 中系统化提出（arXiv:2302.12173）。

## 来源

- 一手来源：https://simonwillison.net/2023/Mar/1/indirect-prompt-injection-on-bing-chat/
- 论文：https://arxiv.org/abs/2302.12173
- 核验状态：✅ 证实（V33）
