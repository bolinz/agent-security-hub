---
title: GrafanaGhost 数据外泄攻击
date: 2026-04
type: 间接注入+外泄
severity: high
status: 已证实
impact: 诱导渲染外部图片以 URL 参数外泄企业数据（关联 CVE-2026-27876），已部分修复
last_updated: 2026-08-18
tags: [Grafana, 间接注入, 数据外泄, NomaSecurity]
related_cves: [CVE-2026-27876]
related_reports: [04-incidents.md]
---

# GrafanaGhost 数据外泄攻击

## 事件概述

- **时间**：2026-04
- **类型**：间接注入+外泄
- **影响对象**：Grafana 渲染场景下的企业数据
- **影响**：诱导渲染外部图片，以 URL 参数外泄企业数据
- **状态**：已证实

## 经过

Noma Security 披露 GrafanaGhost 攻击方式：攻击者诱导目标渲染外部图片，通过 URL 参数将企业数据外泄。该攻击关联 CVE-2026-27876，相关组件已部分修复。

## 影响与损失

企业数据可通过 URL 参数经外部图片请求被外泄。受影响规模（报告未详述）；相关组件已部分修复。

## 来源

- 一手来源 URL：https://noma.security/blog/grafana-ghost/
- 核验状态：✅ 证实（V48）