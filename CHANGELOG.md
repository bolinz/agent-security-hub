# Changelog

本文件记录 Agent Security Hub 的重要变更。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)。

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