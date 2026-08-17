---
title: DeepSeek 云数据库泄露
date: "2025.01"
type: 云配置错误
severity: high
status: 已证实
impact: 100 万+ 日志行真实暴露（含对话记录与 API key）
last_updated: 2026-08-18
tags: [云配置错误, DeepSeek, 数据泄露, Wiz Research]
related_cves: []
related_reports: [04-incidents.md]
---

# DeepSeek 云数据库泄露

## 事件概述

- **时间**：2025.01
- **类型**：云配置错误
- **影响对象**：DeepSeek 云数据库（用户对话记录与 API key）
- **影响**：100 万+ 日志行真实暴露
- **状态**：已证实

## 经过

2025 年 1 月，Wiz Research 发现 DeepSeek 的云数据库因配置错误暴露于公网，其中包含 100 万+ 行日志。暴露数据涉及用户对话记录与 API key，属于真实数据暴露。

## 影响与损失

100 万+ 行日志暴露，内容涉及用户对话记录与 API key。

## 来源

- 一手来源 URL：https://www.wiz.io/blog/wiz-research-uncovers-exposed-deepseek-database-leak
- 核验状态：✅ 证实（V37）