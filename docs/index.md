# Agent Security Hub 索引

> 最近更新：2026-08-18
> 索引按风险等级 / 时间线 / 主题组织，数据与 `library/` 各库条目一致。

## 按风险等级

> 仅收录风险值 ≥ 15 的向量（11/17），完整 17 向量表见 [01-threats.md 1.7](../library/reports/01-threats.md#17-风险评估与优先级风险登记表)。

### 极危（风险值 20-25）

| 向量 | 风险值 | 详情 |
|------|--------|------|
| 间接提示注入 | 25 (L5×I5) | [详情](../library/reports/01-threats.md#1-间接提示注入--风险-25l5i5极危) |
| 直接提示注入 | 25 (L5×I5) | [详情](../library/reports/01-threats.md#2-直接提示注入--风险-25l5i5极危) |
| 过度授权/自治 | 25 (L5×I5) | [详情](../library/reports/01-threats.md#3-过度授权过度自治--风险-25l5i5极危) |
| 数据外泄 | 25 (L5×I5) | [详情](../library/reports/01-threats.md#4-数据外泄--风险-25l5i5极危) |
| 恶意/错位智能体 | 20 (L4×I5) | [详情](../library/reports/01-threats.md#5-恶意错位智能体--风险-20l4i5极危) |
| Vishing/深伪 | 20 (L4×I5) | [详情](../library/reports/01-threats.md#6-vishing深伪社工--风险-20l4i5极危) |

### 高（风险值 15-16）

| 向量 | 风险值 | 详情 |
|------|--------|------|
| 越狱 | 16 (L4×I4) | [详情](../library/reports/01-threats.md#12-提示注入agentic-系统的头号杀手) |
| 供应链攻击 | 16 (L4×I4) | [详情](../library/reports/01-threats.md#7-供应链攻击--风险-16l4i4高) |
| 凭证盗窃 | 16 (L4×I4) | [详情](../library/reports/01-threats.md#8-凭证盗窃--风险-16l4i4高) |
| RAG/向量投毒 | 16 (L4×I4) | [详情](../library/reports/01-threats.md#9-rag向量库投毒--风险-16l4i4高) |
| RCE | 15 (L3×I5) | [详情](../library/reports/01-threats.md#10-rce--风险-15l3i5高) |

## 按时间线

### 2026

| 时间 | 事件 | 类型 | 详情 |
|------|------|------|------|
| 2026-02 | OpenClaw 邮箱删除 | 自主代理失控 | [详情](../library/incidents/2026-02-openclaw邮箱删除.md) |
| 2026-03 | Meta 内部 Agent 泄露 | Agent 错误建议 | [详情](../library/incidents/2026-03-meta-内部agent泄露.md) |
| 2026-03 | Claude Code 源码泄露 | 供应链 | [详情](../library/incidents/2026-03-claude-code源码泄露.md) |
| 2026-03 | Mercor/LiteLLM 供应链 | 供应链 | [详情](../library/incidents/2026-03-mercor-litellm供应链.md) |
| 2026-04 | Flowise CVE-2025-59528 | RCE | [详情](../library/incidents/2026-04-flowise-cve-rce.md) |
| 2026-04 | GrafanaGhost | 注入+外泄 | [详情](../library/incidents/2026-04-grafanaghost.md) |
| 2026-06 | Meta AI 账号接管 | AI 客服社工 | [详情](../library/incidents/2026-06-meta-ai账号接管.md) |
| 2026-07 | Word/Copilot 蠕虫 | 自复制注入 | [详情](../library/incidents/2026-07-word-copilot蠕虫.md) |

### 2025

| 时间 | 事件 | 类型 | 详情 |
|------|------|------|------|
| 2025-01 | DeepSeek 云数据库泄露 | 云配置错误 | [详情](../library/incidents/2025-01-deepseek云数据库泄露.md) |
| 2025-04 | DeepSeek 数据跨境 | 数据跨境 | [详情](../library/incidents/2025-04-deepseek数据跨境.md) |
| 2025-06 | 麦当劳 McHire | 弱认证 | [详情](../library/incidents/2025-06-mcdonalds-mchire.md) |
| 2025-06 | Copilot EchoLeak | 注入+外泄 | [详情](../library/incidents/2025-06-copilot-echoleak.md) |
| 2025-06 | Skynet 恶意软件 | 对抗检测 | [详情](../library/incidents/2025-06-skynet恶意软件.md) |
| 2025-12 | 墨西哥政府泄露 | AI 辅助攻击 | [详情](../library/incidents/2025-12-墨西哥政府泄露.md) |

### 2024

| 时间 | 事件 | 类型 | 详情 |
|------|------|------|------|
| 2024-01 | 香港 Deepfake CFO | Deepfake 欺诈 | [详情](../library/incidents/2024-01-香港deepfake-cfo.md) |

### 2023

| 时间 | 事件 | 类型 | 详情 |
|------|------|------|------|
| 2023-02 | Bing Chat 间接注入 | 间接注入 | [详情](../library/incidents/2023-02-bing-chat-间接注入.md) |
| 2023-05 | 包头 AI 换脸 | Deepfake 欺诈 | [详情](../library/incidents/2023-05-包头AI换脸诈骗.md) |

## 按主题

### 供应链攻击

| 事件 | 时间 | 详情 |
|------|------|------|
| Claude Code 源码泄露 + 恶意仓库 | 2026-03 | [详情](../library/incidents/2026-03-claude-code源码泄露.md) |
| Mercor/LiteLLM 供应链事件 | 2026-03 | [详情](../library/incidents/2026-03-mercor-litellm供应链.md) |
| CVE-2025-6514 mcp-remote RCE | 2025 | [详情](../library/vulnerabilities/CVE-2025-6514-mcp-remote.md) |

### Deepfake 欺诈

| 事件 | 时间 | 损失 | 详情 |
|------|------|------|------|
| 香港 Deepfake CFO 案 | 2024-01 | 2 亿港元 | [详情](../library/incidents/2024-01-香港deepfake-cfo.md) |
| 包头 AI 换脸案 | 2023-05 | 约 430 万元 | [详情](../library/incidents/2023-05-包头AI换脸诈骗.md) |

### 过度授权 / 自主代理失控

| 事件 | 时间 | 详情 |
|------|------|------|
| OpenClaw 邮箱删除 | 2026-02 | [详情](../library/incidents/2026-02-openclaw邮箱删除.md) |
| Meta AI 账号接管 | 2026-06 | [详情](../library/incidents/2026-06-meta-ai账号接管.md) |

### RCE / 代码执行

| CVE | 组件 | CVSS | 详情 |
|-----|------|------|------|
| CVE-2025-59528 | Flowise | 10.0 | [详情](../library/vulnerabilities/CVE-2025-59528-flowise-rce.md) |
| CVE-2025-6514 | mcp-remote | 9.6 | [详情](../library/vulnerabilities/CVE-2025-6514-mcp-remote.md) |
| CVE-2025-53773 | GitHub Copilot | 9.6 | [详情](../library/vulnerabilities/CVE-2025-53773-copilot-rce.md) |
| CVE-2025-59536 | Claude Code | 8.7 | [详情](../library/vulnerabilities/CVE-2025-59536-claude-code.md) |

## 评估模型

| 模型 | 用途 | 详情 |
|------|------|------|
| 风险评估打分 | 评估单个 Agent 系统风险 | [详情](evaluation/risk-score.md) |
| 成熟度模型 | 评估组织 Agent 安全能力 | [详情](evaluation/maturity-model.md) |

## 分享材料

| 材料 | 用途 | 详情 |
|------|------|------|
| 入门指南 | 威胁、风险与量化评估（自学入门） | [详情](agent-security-guide.md) |

## 报告章节

| 章 | 标题 | 详情 |
|----|------|------|
| 0 | 报告概览 | [详情](../library/reports/00-overview.md) |
| 1 | 攻击面与威胁分类 | [详情](../library/reports/01-threats.md) |
| 2 | 防御方法与最佳实践 | [详情](../library/reports/02-defenses.md) |
| 3 | 安全标准、框架与合规 | [详情](../library/reports/03-standards.md) |
| 4 | 真实事件案例与生态格局 | [详情](../library/reports/04-incidents.md) |
| 5 | 结论与行动建议 | [详情](../library/reports/05-conclusions.md) |
| 6 | 信息来源核验表 | [详情](../library/reports/06-fact-check.md) |