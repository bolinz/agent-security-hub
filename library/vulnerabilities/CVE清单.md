# 漏洞库

Agent 相关漏洞（CVE 为主）。种子数据来自研究报告 01 章 1.3/1.4、02 章 2.9。

## CVE 清单

| CVE | 组件 | 类型 | CVSS | 说明 |
|-----|------|------|------|------|
| CVE-2025-6514 | mcp-remote | RCE（OAuth 注入） | 9.6 | 连接不可信 MCP 服务器触发任意命令执行 |
| CVE-2025-32711 | M365 Copilot | 注入+数据外泄 | 9.3 | EchoLeak 零点击注入 |
| CVE-2025-59528 | Flowise | RCE（CustomMCP JS） | 10.0 | 在野利用，1.2-1.5 万实例 |
| CVE-2026-27876 | Grafana | 注入+外泄 | — | GrafanaGhost 图片渲染外泄 |
| CVE-2025-53773 | GitHub Copilot | RCE（注入 PR 描述） | 9.6 | — |
| CVE-2025-59536 | Claude Code | RCE（注入→代码执行） | 8.7 | — |

> 来源：研究报告 01 章 1.3/1.4、02 章 2.9；核验见 reports/ 核验表（V77 等）。
