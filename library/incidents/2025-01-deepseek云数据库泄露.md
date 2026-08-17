---
title: "2025 01 deepseek云数据库泄露"
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

# 2025 01 deepseek云数据库泄露

## 事件概述

- **时间**：
- **类型**：
- **影响**：
- **状态**：已证实

## 经过

2025 年 1 月，Wiz Research 安全团队发现中国 AI 公司 DeepSeek 的一个 ClickHouse 云数据库完全公开可访问，无需任何认证。该数据库包含超过 100 万行日志记录，内含用户与 DeepSeek 聊天机器人的完整对话内容、API 密钥、后端操作日志等敏感信息。Wiz 于 2025 年 1 月 29 日负责任披露，DeepSeek 在收到通知后迅速修复。泄露原因为云数据库配置错误，未设置访问控制。

## 来源

- 一手来源：https://www.wiz.io/blog/wiz-research-uncovers-exposed-deepseek-database-leak
- 核验状态：✅ 证实（V37）
