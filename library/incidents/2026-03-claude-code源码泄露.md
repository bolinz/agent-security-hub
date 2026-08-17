---
title: Claude Code 源码泄露与钓鱼恶意仓库
date: 2026-03
type: 供应链
severity: critical
status: 已证实
impact: npm source map 暴露约 51.3 万行源码；伪造"泄露版"仓库分发 Vidar/GhostSocks 恶意软件
last_updated: 2026-08-18
tags: [Claude Code, 源码泄露, 供应链, 钓鱼, 恶意软件]
related_cves: []
related_reports: [04-incidents.md]
---

# Claude Code 源码泄露与钓鱼恶意仓库

## 事件概述

- **时间**：2026-03
- **类型**：供应链
- **影响对象**：Claude Code 用户及源码
- **影响**：npm source map 暴露约 51.3 万行源码；伪造"泄露版"仓库分发 Vidar/GhostSocks 恶意软件
- **状态**：已证实

## 经过

Claude Code 的 npm source map 暴露了约 51.3 万行源码。攻击者随后伪造"泄露版"仓库，利用该热点分发 Vidar/GhostSocks 恶意软件。事件属于供应链与社工结合的连环攻击。

## 影响与损失

约 51.3 万行源码经 source map 泄露；伪造"泄露版"仓库用于分发 Vidar/GhostSocks 恶意软件。受影响用户数量（报告未详述）。

## 来源

- 一手来源 URL：https://www.zscaler.com/blogs/security-research/anthropic-claude-code-leak
- 核验状态：✅ 证实（V45）