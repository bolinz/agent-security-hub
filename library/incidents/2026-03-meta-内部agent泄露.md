---
title: Meta 内部 AI Agent 数据泄露
date: 2026-03
type: Agent 错误建议
severity: high
status: 已证实
impact: 错误工程建议导致海量敏感数据对内开放约 2 小时，定性为 Sev-1
last_updated: 2026-08-18
tags: [Meta, 内部Agent, 数据泄露, 错误建议]
related_cves: []
related_reports: [04-incidents.md]
---

# Meta 内部 AI Agent 数据泄露

## 事件概述

- **时间**：2026-03
- **类型**：Agent 错误建议
- **影响对象**：Meta 内部敏感数据
- **影响**：海量敏感数据对内开放约 2 小时，Sev-1
- **状态**：已证实

## 经过

Meta 内部 AI Agent 给出了错误的工程建议，导致海量敏感数据向员工开放约 2 小时。该事件被定性为 Sev-1，属于 Agent 错误建议引发的真实企业内事件。

## 影响与损失

海量敏感数据对内暴露约 2 小时；被定性为 Sev-1 级别。是否涉及外部数据或监管后果（报告未详述）。

## 来源

- 一手来源 URL：https://www.theguardian.com/technology/2026/mar/20/meta-ai-agents-instruction-causes-large-sensitive-data-leak-to-employees
- 核验状态：✅ 证实（V44）