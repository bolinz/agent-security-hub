# Changelog

本文件记录 Agent Security Hub 的重要变更。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)。

## [1.2.0] - 2026-08-18

### 变更
- `docs/presentation-30min.md` 重构为 `docs/agent-security-guide.md`《Agent 安全指南：威胁、风险与量化评估》
  - 演讲稿改为书面学习文档（弱化演讲形式，移除读法与演讲速用路线）
  - 评估模型章节移至收官位置，新增三件套 × 三问价值收束
  - "致命三角（Simon Willison）"改为"结构性风险组合"，锚定 OWASP LLM/Agentic Top 10 与 MITRE ATLAS
  - 新增阅读时间表、每节核心要点、术语速查、权威性分级、推荐阅读
  - 案例精简为 3 起（Meta AI 客服 / Flowise / OpenAI×HuggingFace），新增"OpenAI 攻击 HuggingFace"自主智能体入侵案例
- 新增事件条目 `library/incidents/2026-07-openai-攻击huggingface.md`（HF 官方技术时间线 + OpenAI 官方公告）
- 已证实事件清单补充至 19 起
- README.md / docs/index.md / CLAUDE.md 同步更新文件名与描述

### 修复
- 风险评分矩阵图例阈值 `15-20 高` 修正为 `15-16 高`
- L×I 方法论注明出处（NIST SP 800-30 Rev.1 + AI RMF）

## [1.1.0] - 2026-08-18

### 改进
- 拆分报告为 7 个独立章节文件（00-overview 到 06-fact-check）
- 事件库拆分为 17 个独立条目文件
- 漏洞库拆分为 6 个独立条目文件
- 所有主要文件增加 frontmatter 元数据
- 增加 CHANGELOG.md
- 增加 CONTRIBUTING.md 贡献指南
- 增加 docs/index.md 按风险等级/时间线/主题的索引

### 变更
- reports/README.md 更新为章节导航
- incidents/README.md 更新为条目导航
- vulnerabilities/README.md 更新为条目导航

### 修复
- 修复 docs/index.md 链接路径与风险登记表锚点
- 修正风险分级阈值口径（高 15-16 / 极危 20-25）

## [1.0.0] - 2026-08-17

### 初始版本
- 初始化 Agent Security Hub 知识库
- 6 个分类库：reports/incidents/vulnerabilities/vendors/papers/tools
- 双评估模型：风险打分 + 成熟度模型
- 30 分钟分享文档
- 种子数据：18 事件（17 已证实 + 1 待证实）、6 CVE、14+ 厂商、10 论文、9+ 工具
- 完整研究报告（2333 行，79 条核验声明）