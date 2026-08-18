# Changelog

本文件记录 Agent Security Hub 的重要变更。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)。

## [1.3.0] - 2026-08-18

### 变更
- 新增红蓝对抗评审报告 `docs/evaluation/red-blue-confrontation-report.md`（3 轮对抗：16 项漏洞 → 16 项防御 → 优化 → 共识）
- `docs/evaluation/risk-score.md` 按 P0 行动项修订：
  - 新增验证等级 V0-V3（结论可信度门控，与数值运算解耦）；V0 未验证不得"接受"
  - 新增评估产出模板（验证状态/署名/证伪条件/模型版本元数据块）
  - 新增边界滞回（6→中、12→高、16→极危）、尾部覆盖（I≥4 最低"中"、I=5 最低"高"）、保守主导规则
  - 5×5 热力表改为公式派生查值表（删除逐格赋值）；新增攻击链布尔门控
  - 使用步骤增加必选向量条款、偏差留痕、链检查；处置建议改为档位制
- `docs/evaluation/maturity-model.md` 按 P0 行动项修订：
  - 新增验证要求小节（验证状态元数据块、证据分级、名义等级标注、维度 0 强制复核）

### 改进（P1 行动项）
- `risk-score.md` 新增：模型版本头 + 失效条款、范围与链预注册、确定性修正规则表、阈值登记表
- `maturity-model.md` 新增：模型版本头 + 失效条款
- 新增对抗性测试用例集 `docs/evaluation/adversarial-test-cases.md`（正/负例 7 条，含示例回归）作为模型使用前置门禁
- `docs/index.md` 评估模型区补充对抗性测试与红蓝对抗评审链接

### 改进（P2 行动项）
- `risk-score.md` 新增：适用范围强制前置检查（安全关键/非财务场景不适用）、验证闭环 Tier 0/1/2 明细（内审抽样 ≥50%、第三方审计防宽松条款）、评估产出模板补充对抗性测试结果与审计方声明字段
- `adversarial-test-cases.md` 扩充对抗性用例 T8-T10（乐观评估/圈除向量/未验证结论）
- 自动失效钩子：`library/incidents/_template.md` 与 `library/vulnerabilities/_template.md` 新增入库登记提醒
- `maturity-model.md` L4/L5 量化升级：指标须日志实测、方向/公式/来源登记、结果型指标优先、红队报告须含改进闭环

## [1.2.0] - 2026-08-18

### 变更
- `docs/presentation-30min.md` 重构为 `docs/agent-security-guide.md`《Agent 安全指南：威胁、风险与量化评估》
  - 演讲稿改为书面学习文档（弱化演讲形式，移除读法与演讲速用路线）
  - 评估模型章节移至收官位置，新增三件套 × 三问价值收束
  - "致命三角（Simon Willison）"改为"结构性风险组合"，锚定 OWASP LLM/Agentic Top 10 与 MITRE ATLAS
  - 新增阅读时间表、每节核心要点、术语速查、权威性分级、推荐阅读
  - 案例精简为 3 起（Meta AI 客服 / Flowise / OpenAI×HuggingFace），新增"OpenAI 攻击 HuggingFace"自主智能体入侵案例
  - L×I 风险评分矩阵移至第 5 章评估模型，§1.5 仅保留四个极危向量结论
  - I 影响维度改为 OWASP 式双因子（技术影响 C/I/A + 业务影响），美元降为校准参照
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