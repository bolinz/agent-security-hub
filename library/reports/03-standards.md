---
title: 安全标准、框架与合规
chapter: 3
parent: ai-agent-security-report.md
last_updated: 2026-08-18
status: 完成
prev: 02-defenses.md
next: 04-incidents.md
---

> 本页为《AI Agent 领域安全挑战与应对方法调研》第 3 章。[上一章 02-defenses.md](02-defenses.md) · [下一章 04-incidents.md](04-incidents.md) · [返回报告概览](00-overview.md)

---

# 三、安全标准、框架与合规（Standards & Frameworks）


## 3.1 主要标准/框架清单

> 下表汇总 Agent 安全相关的主要标准/框架及其最新版本。各框架详细内容见 3.2-3.6 节；核验明细见 [06-来源核验表](06-fact-check.md)。

| 框架 | 组织 | 范围 | 关键文件 |
|------|------|------|---------|
| OWASP Top 10 for LLM Applications | OWASP GenAI Security | LLM 应用漏洞 Top 10 | 2023-24、2025 版（无"LLM Top 10 2026"，2026 年的 Agentic Top 10 见下行） |
| OWASP Agentic AI Threat Matrix / ASI 系列 | OWASP Agentic Security Initiative | Agentic AI 威胁模型与缓解 | Threats & Mitigations v1.0 (2025-02)、Top 10 for Agentic 2026 (2025-12) |
| MITRE ATLAS™ | MITRE | AI/ML 系统对抗战术/技术知识库 | atlas.mitre.org，STIX 开源（16 tactics / 178 techniques） |
| NIST AI RMF | NIST | AI 全生命周期风险管理 | AI 100-1、AI 600-1 GenAI Profile |
| NIST 对抗机器学习 | NIST | AML 攻击/缓解分类学 | AI 100-2e2023 |
| ISO/IEC 42001 | ISO/IEC JTC 1/SC 42 | AI 管理体系（可认证） | ISO/IEC 42001:2023 |
| EU AI Act | 欧盟 | 面向风险分级的产品合规法规 | Regulation (EU) 2024/1689（时间表见 3.4） |
| CISA/NCSC 等 21 国机构 | CISA、NCSC 等 | AI 系统安全开发 | Guidelines for Secure AI System Development (2023-11) |
| 中国《生成式人工智能服务管理暂行办法》 | 国家网信办等七部门 | 境内 GenAI 服务监管 | 令第 15 号，2023-08-15 施行 |
| MCP / A2A | Anthropic 开源 / Linux Foundation | Agent 互操作协议安全 | MCP 规范安全章节、A2A（Agent2Agent）v1.0 |
| 安全基准 | ETH SPyLab 等 | Agent 攻防评测 | AgentDojo、ASB、AgentLeak、CyberSecEval（明细见 3.5） |

## 3.2 OWASP 详解

**LLM Top 10 2025 版**（注：该版本实际发布于 **2024-11-17**，命名"2025"为版本代号）：

| 编号 | 2025 分类 | 变化 |
|------|-----------|------|
| LLM01 | Prompt Injection | 保留（居首） |
| LLM02 | Sensitive Information Disclosure | 提前 |
| LLM03 | Supply Chain | 保留 |
| LLM04 | Data and Model Poisoning | 由 Training Data Poisoning 改名扩围 |
| LLM05 | Improper Output Handling | 改名 |
| LLM06 | Excessive Agency | 保留（对 Agent 关键） |
| LLM07 | System Prompt Leakage（新） | 明确"系统提示不应被当作安全控制" |
| LLM08 | Vector and Embedding Weaknesses（新） | RAG 向量库、嵌入反转、数据投毒 |
| LLM09 | Misinformation（新） | 取代 Overreliance |
| LLM10 | Unbounded Consumption（新） | 取代 Model DoS，含成本耗尽 |

**OWASP Agentic Security Initiative（ASI）**：
- **Agentic AI – Threats and Mitigations v1.0**（2025-02-17）：基于威胁建模的 Agentic 威胁清单 + 交互式 Agentic AI Threat Matrix；
- **Agentic Threats Navigator**（2025-03-06，正确 URL slug 为 `owasp-gen-ai-security-project-agentic-threats-navigator`）：划定六大攻击面——推理、记忆、工具、身份、人类监督、多 Agent 交互；
- **Securing Agentic Applications Guide 1.0**（2025-07-27）：落地技术指南；
- **Top 10 for Agentic Applications 2026**（2025-12-09）：**ASI01 Agent Goal Hijack / ASI02 Tool Misuse / ASI03 Identity & Privilege Abuse / ASI04 Agentic Supply Chain / ASI05 Unexpected Code Execution / ASI06 Memory & Context Poisoning / ASI07 Insecure Inter-Agent Communication / ASI08 Cascading Failures / ASI09 Human-Agent Trust Exploitation / ASI10 Rogue Agents**。
- 配套：Agent Observability Standard（aos.owasp.org）、MCP 安全专项指南、FinBot CTF。

## 3.3 MITRE ATLAS 详解

[MITRE ATLAS](https://atlas.mitre.org/) 是 ATT&CK 在 AI 领域的对应物，Tactics–Techniques–Case Studies 三级结构，STIX 开源：
- **16 个 Tactic**、**178 个 Technique**，含 AI 专属 Tactic **AI Model Access（AML.TA0000）** 与 **AI Attack Staging（AML.TA0001）**。
- 关键 LLM/Agent 技术（逐一在 ATLAS 数据中确认）：LLM Prompt Injection（**AML.T0051**，含 .000 Direct/.001 Indirect/.002 Triggered 子技术）、LLM Jailbreak（**AML.T0054**）、Training Data Poisoning（**AML.T0020**）、AI Supply Chain Compromise: AI Agent Tool（**AML.T0010.005**）、User Execution: Poisoned AI Agent Tool（**AML.T0011.002**）、Exfiltration via AI Inference API（**AML.T0024**）、Cost Harvesting（**AML.T0034**）。
- OWASP 各条目均标注对应 AML.T####，因此 ATLAS 常被用作其底层分类学（本报告表述，非官方定义）；两者共同支撑红队演练与 SOC 检测规则映射。

## 3.4 NIST / ISO / 法规合规

- **NIST**：AI RMF 1.0（AI 100-1，2023-01-26）；AI 600-1 GenAI Profile（2024-07-26）；对抗机器学习分类学 AI 100-2e2023（2024-01-04 定稿，evasion/data poisoning/privacy breach/abuse 四大类）；SP 800-218A（SSDF，Secure Software Development Framework，GenAI 安全开发，2024-07-26）。Agentic 专项标准仍在推进中。
- **ISO/IEC 42001:2023**：首个**可认证**的 AI 管理体系标准（AIMS），可与 ISO 27001 对接；配套 ISO/IEC 23894（风险，2023）、42005（影响评估，2025）、42006（审计/认证，2025）、5338（生命周期，2023）。
- **EU AI Act**（Regulation (EU) 2024/1689）：按风险分级——不可接受风险（Art.5）禁止；高风险系统（Art.6+Annex）须满足 Art.8–17，含风险管理（Art.9）、**人类监督（Art.14）**、**准确性/鲁棒性/网络安全（Art.15）**；GPAI（通用人工智能模型，General-Purpose AI）系统性风险模型（训练算力 >10²⁵ FLOPs）须做模型评估与对抗测试。**时间表已按 Digital Omnibus（2026-07-27 生效）更新**：禁止条款 **2025-02-02** 生效；GPAI 义务 **2025-08-02** 生效；Annex III 高风险 **2027-12-02**（原 2026-08-02，已推迟）；Annex I 高风险 **2028-08-02**（原 2027-08-02，已推迟）。来源：EUR-Lex 原 Reg. + Commission Digital Omnibus（2026-07）。
- **中国**：《生成式人工智能服务管理暂行办法》（令第 15 号，2023-08-15 施行）——训练数据合法来源、安全评估、算法备案、内容标识；《人工智能生成合成内容标识办法》（国信办通字〔2025〕2 号，**2025-09-01 生效**）；国家网信办 2024-09 发布《人工智能安全治理框架》1.0（来源：cac.gov.cn，见官方来源列表）。对 Agent：境内对外提供 Agent 服务**通常落入"生成式 AI 服务提供者"监管范围**（本报告解读，具体适用以主管部门解释为准，见待官方明确清单）。
- **CISA/ENISA**：21 国机构《Guidelines for Secure AI System Development》（2023-11-27，安全设计/开发/部署/运维四阶段）；ENISA Multilayer Framework（2023，三层实践框架）。

## 3.5 安全基准与评估

> 下表汇总可用于 agent 安全评估的公开基准。各基准的评测方法详见 3.9 节与论文原文；核验明细见 [06-来源核验表](06-fact-check.md)。

| 基准 | 来源 | 规模/特点 |
|------|------|-----------|
| AgentDojo | ETH SPyLab（arXiv:2406.13352） | 97 个真实任务、629 个安全用例 |
| Agent Security Bench (ASB) | Zhejiang University + Rutgers（arXiv:2410.02644） | 10 场景、400+ 工具、27 种攻防方法；最高平均攻击成功率 **84.3%** |
| AgentLeak | arXiv:2602.11510（Privatris 团队） | 多 Agent 内部信道隐私泄露基准 |
| MCPTox | arXiv:2508.14925 | 真实 MCP 服务器工具投毒基准：45 服务器/353 工具/1312 用例；最高攻击成功率 72.8%、主流模型拒绝率 <3% |
| CyberSecEval 1/2 | Meta Purple Llama | *Purple Llama CyberSecEval: A Secure Coding Benchmark*（arXiv:2312.04724）：原始版模型不安全代码约 **30%**；"26–41% 不安全代码率"属 **CyberSecEval 2**（arXiv:2404.13161）的 prompt injection 成功率区间 |
| AgentAttackBench | 清华 NLP | 交互式工具使用对抗指令鲁棒性基准（github.com/thunlp/AgentAttackBench） |

## 3.6 框架对照表（Cross-mapping）

| 风险维度 | OWASP LLM Top10 2025 | OWASP Agentic / ASI | MITRE ATLAS | NIST | EU AI Act | ISO 42001 |
|---|---|---|---|---|---|---|
| 提示词操纵 | LLM01 Prompt Injection | Prompt Injection | AML.T0051 | SP 800-218A / AI RMF | Art.15 + Art.55 | AI 风险管理控制 |
| 数据/模型投毒 | LLM04 Data & Model Poisoning | Memory/Training Poisoning | AML.T0020, T0018 | AI 100-2 | Art.10 | Annex A 控制 |
| 越权/过度自主 | LLM06 Excessive Agency | 过度自主权 | AML.T0046 | AI RMF Manage | Art.14 人类监督 | 影响评估 42005 |
| 敏感信息泄露 | LLM02 Sensitive Info Disclosure | 记忆/工具数据泄露 | AML.T0024 | AI 100-2 | GDPR + Art.15 | 审计 42006 |
| 供应链 | LLM03 Supply Chain | 工具/MCP 供应链 | AML.T0010 | SP 800-218A | Annex III | AIBOM（AI 组件清单）/SBOM |
| 资源滥用/DoS | LLM10 Unbounded Consumption | Unbounded Consumption | AML.T0034, T0029 | — | Art.15 | — |
| Agent 特有（记忆/身份/多代理） | LLM07/08 | 记忆投毒、身份混淆 | AML.T0011.002, T0002.002 | 修订中 | Art.14 | 42001 全生命周期 |

**合规落点**：把 OWASP（工程漏洞）→ ATLAS（威胁建模技术标识）→ NIST/ISO 42001（风险管理与体系）→ EU AI Act / 中国办法（强制合规）串成"漏洞-威胁-风险-监管"四层，是当前 Agent 安全治理的主流映射思路（本报告判断，非官方标准表述）。

## 3.7 合规落地映射（义务→控制）

> 3.6 的四层映射在此落到具体法条→控制对。法条引用精确到条款号并附官方原文 URL；**二手转述不作为法条原文**；凡未获官方明确处标注"待官方明确"。

### 执行摘要（BLUF）

**如果只记住一件事**：如果你的 agent 产品在欧盟或中国提供服务,**"安全"已经不是可选项而是法律义务**——EU AI Act 要求高风险 AI 系统满足人类监督(Art.14)与网络安全(Art.15)义务,中国则要求具舆论属性的服务完成算法备案、安全评估、内容标识三线流程。**这些义务能直接映射成我们已经讨论过的技术控制**（HITL=人在回路 human-in-the-loop 审批、注入防御、审计日志),所以合规与安全是同一条工程。

**三个关键发现**：
1. **EU 侧,agent 是否高风险取决于"用途"而非"自主性"**——通用聊天 agent 通常非高风险;同一 agent 若用于招聘/信用评分/监考/选举即变高风险。Art.14(人类监督)与 Art.15(网络安全)对高风险 agent 是强制的。
2. **中国侧,三线流程的触发词是"舆论属性或社会动员能力"**——这是中国 agent 产品最关键的分水岭;一旦触发,须在 10 个工作日内算法备案、上线前安全评估、所有生成内容加显式+隐式标识(2025-09-01 起强制)。
3. **两个体系都还有"待官方明确"地带**——EU 的 Art.6 实施规范（common specifications，法定期限 2026-02-02，**检索日 2026-08 的实际发布状态待核**）将最终界定高风险边界;中国对"通用 agent 工具调用是否触发安全评估"也无官方解释。

**行动建议**：按"产品用途 → 判定适用法律 → 映射控制 → 准备证据"四步走。先做合规影响评估,再决定要满足哪套义务。

---

### 一、EU AI Act：Art.14/15 怎么映射到 Agent 控制

> 原文均取自 EUR-Lex：[Regulation (EU) 2024/1689](https://eur-lex.europa.eu/eli/reg/2024/1689/oj)

#### 1.1 Art.14 人类监督 → 技术控制

EU AI Act 要求高风险 AI 系统"使用期间可被自然人有效监督"(Art.14(1)),并列举了监督者必须具备的能力。对 Agent 系统,这直接对应我们已讨论的 HITL 控制：

| 法条要求（原文要点） | Agent 技术控制 |
|----------------|---------------|
| 14(1) 可被自然人有效监督 | HITL 审批门、运行/暂停/恢复监督控制台 |
| 14(3) 与风险/自主程度/使用场景相称 | **分级自主**：按动作类别设护栏（只读→工具调用→不可逆动作） |
| 14(3)(a) 提供商内置措施 | 内置约束：动作白名单、工具沙箱、系统自身不可覆写 |
| 14(4)(a) 监测异常/故障 | **Agent 遥测**：动作日志、工具调用审计、行为漂移检测 |
| 14(4)(b) 防止自动化偏差 | 重要输出由人确认；置信度展示 |
| 14(4)(c) 正确解读输出 | 可解释层：推理轨迹、工具结果引用 |
| 14(4)(d) 否决/覆写/逆转输出 | 每个 agent 动作提供人工否决原语 |
| 14(4)(e) 通过"停止按钮"中断 | **急停**：终止工具执行与网络访问、安全状态停机 |
| 14(5) 双人核验 | 仅适用于生物识别场景（Annex III 1(a)），非 agent 通用 |

#### 1.2 Art.15 准确性/鲁棒性/网络安全 → 技术控制

Art.15 是"网络安全"义务的核心条款,直接要求抵御投毒、对抗样本、漏洞利用——这几乎就是一份 agent 安全需求清单：

| 法条要求（原文要点） | Agent 技术控制 |
|----------------|---------------|
| 15(1) 全生命周期一致的准确性/鲁棒性/网络安全 | 每个 agent 版本 eval 门禁；模型/版本锁定 + 回滚 |
| 15(3) 指标在说明书声明 | 发布任务成功率、工具错误率、安全 eval 分数 |
| 15(4) 对错误/故障有韧性 | 冗余工具、故障安全计划、外部 API 断路器 |
| 15(4) 持续学习防反馈回路 | **记忆/自学习治理**：冻结或沙箱化在线学习、反馈回路检测 |
| 15(5) 抵抗第三方利用漏洞 | 提示注入防御（指令层级、工具权限边界）、OWASP agentic 覆盖、最小权限凭证 |
| 15(5) 数据投毒/模型投毒/对抗样本/模型规避 | 训练数据来源核验、发布前红队、RAG 知识隔离、不可信输出沙箱 |

#### 1.3 配套条款（对 Agent 尤其相关）

- **Art.9 风险管理**：将工具滥用视为"可合理预见的误用"；风险登记表按 agent 能力/自主级别建账（对应本报告 [风险登记表（01 章 1.7）](01-threats.md)）
- **Art.12 记录**：只追加、防篡改的提示/动作/工具调用/决策日志；提供商日志**至少保留 6 个月**（条款号以官方文本为准，原文为 EUR-Lex Reg. 2024/1689）。
- **Art.17 质量体系**：变更管理对持续更新的 agent 至关重要（"实质修改"重新触发合规,Art.43(4)）
- **Art.50 透明度**：面向自然人交互的 AI 必须告知"与 AI 交互"；合成内容须机器可读标记（对所有 agent 适用,不限高风险）

#### 1.4 GPAI Code of Practice 状态

- GPAI 义务自 **2025-08-02** 起适用（Art.113(2)(b)）
- 最终版代码 2025-07-10 提交委员会；2025-08-01 批准
- 覆盖 Art.53（GPAI 技术文档/下游信息/版权政策/训练数据摘要）与 Art.55（系统性风险模型）
- 来源：https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice

---

### 二、中国三线合规流程：算法备案 / 安全评估 / 内容标识

#### 2.1 触发判定:你的 agent 服务需要走流程吗?

> 暂行办法 Art.17 原文:"提供具有舆论属性或者社会动员能力的生成式人工智能服务的,应当按照国家有关规定开展**安全评估**,并按照《互联网信息服务算法推荐管理规定》履行**算法备案**和变更、注销备案手续。"

**判断逻辑**：如果你的 agent 服务具"舆论属性或社会动员能力"(如面向公众的内容生成、信息聚合、舆论影响),三线全走;否则至少内容标识义务(对生成内容)。

#### 2.2 三线流程走查（面向境内公众的智能体产品）

**① 算法备案**
- **时限**：提供服务后 **10 个工作日内**；变更 10 工作日内；注销 20 工作日内（Art.24）
- **备案内容**：提供者名称、服务形式、应用领域、算法类型、**算法自评估报告**、拟公示内容
- **系统**：互联网信息服务算法备案系统（beian.cac.gov.cn，域名待再核验）
- **结果**：30 个工作日内发备案编号并公示；网站/APP 须展示备案编号（Art.25-26）

**② 安全评估**
- **触发**：舆论属性/社会动员能力；或生物识别编辑工具；或涉国家安全内容（深度合成 Art.15(2)）
- **时机**：**新产品/新应用/新功能上线前**（Art.20）
- **形式**：自评估或委托专业机构；备案/评估时须同时提交标识相关材料（标识办法 Art.12）
- **⚠️ 待官方明确**：通用 agent 工具调用本身是否触发"新功能"评估

**③ 内容标识（2025-09-01 起强制）**
- **显式标识**（用户可感知）：文本→界面提示；音频→语音提示；图像→显著标记；视频→首帧标记（标识办法 Art.4）
- **隐式标识**（文件元数据）：嵌入生成属性、提供者名称/编码、内容编号；鼓励水印（Art.5）
- **传播环节**：平台核验隐式标识、对未标识内容加"疑似"提示（Art.6）
- **日志**：用户申请无标识须保留日志 **≥6 个月**（Art.9）
- **禁止**：不得删除/篡改/伪造标识（Art.10）

#### 2.3 对 Agent 产品的具体含义

1. 实时生成输出（对话文本、图片、音视频、拟真场景）必须**显式标识**
2. 可下载文件（agent 生成的报告/PDF/图片）元数据应**隐式标识**（依《标识办法》Art.5；配套国标 GB 45438-2025 号已确认，具体技术细节以官方文本为准——见待官方明确清单）。
3. 若具备舆论属性 → 三线全走 + 应用商店上架前核验（深度合成 Art.13；标识办法 Art.7）

---

### 三、ISO/IEC 42001：Annex A → Agent 控制映射

> ⚠️ 标准全文付费（iso.org 对自动化抓取 403）；Annex A 结构（A.2-A.10，38 项控制）经二手来源核实，**逐控制 ID 文本待官方核对**。ISO/IEC 42001:2023（[iso.org/standard/81230.html](https://www.iso.org/standard/81230.html)）。

**ISO 42001 是可认证的 AI 管理体系(AIMS)**——企业客户/监管方可能要求你具备它。它的 38 项 Annex A 控制是组织级的,但可直接映射到 agent 控制：

| 控制域 | 聚焦 | Agent 产品相关性 |
|--------|------|----------------|
| A.2 AI 相关策略 | AI 政策 | Agent 可接受使用与自主政策 |
| A.3 内部组织 | 角色/责任 | Agent 负责人；**人类监督角色定义**（对应 Art.14） |
| A.4 AI 系统资源 | 资源记录 | 算力、模型许可、eval 工具清单 |
| A.5 AI 影响评估 | 影响评估 | 上线前 AI 影响评估；为高风险判定提供输入 |
| A.6 AI 生命周期 | 设计/开发/部署 | Agent SDLC；**实质修改变更管理**；agent 退役 |
| A.7 AI 系统数据 | 数据治理 | RAG 语料、工具调用日志、反馈回路数据（对应 Art.15(4)） |
| A.8 利益相关方信息 | 透明度 | Agent 披露文档（对应 Art.50(1)） |
| A.9 AI 系统使用 | 使用边界/滥用 | 工具白名单、禁止动作、影子 agent 监控（对应 Art.14(4)(a)） |
| A.10 第三方/客户 | 供应链风险 | 模型厂商尽调、子 agent 供应商、第三方模型集成责任 |

**配套标准**：ISO/IEC 42005:2025（影响评估）、ISO/IEC 42006:2025（AIMS 审计与认证机构要求）。

---

### 四、Agent 产品 EU 高风险分类:怎么判定?

**主规则（Art.6(2))**：agent 仅当其**预期用途**落入 Annex III 领域才为高风险。八大领域:①生物识别 ②关键基础设施 ③教育职业培训 ④就业员工管理 ⑤基本公共服务 ⑥执法 ⑦移民庇护边境 ⑧司法与民主过程。

**豁免（Art.6(3))**：不构成重大伤害风险 + 满足(狭窄程序任务/改善人工活动/检测模式但人工审查/预备任务)之一 → 非高风险。**但"对自然人画像"总是高风险**。

**双层现实**：
- **模型层**：基于 GPAI 模型构建 → 模型提供者承担 Chapter V 义务；系统性风险(>10²⁵ FLOPs)触发 Art.55
- **系统层**：agent 按 Art.6/Annex III 单独分类

**关键结论**：agent 的**自主性本身不是**系统高风险的分类器。通用聊天 agent 通常**非高风险**;同一 agent 若用于招聘/信用评分/监考/选举即变高风险。

**待官方明确**：Art.6(5) 要求委员会不迟于 **2026-02-02** 通过实施规范（common specifications，非"指南"）→ 检索日 2026-08 的实际通过状态待核，最终界定以该规范为准。

---

### 五、待官方明确清单

| # | 事项 | 状态 |
|---|------|------|
| 1 | 深度合成规定/标识办法 cac.gov.cn 精确文章 URL | ⚠️ 内容经核实，URL 待再核对 |
| 2 | 《安全评估规定》(2018) 全文 | ⚠️ 被 Art.17 引用但未抓取全文 |
| 3 | 算法备案系统域名 beian.cac.gov.cn | ⚠️ 待再核验 |
| 4 | ISO 42001 Annex A 逐控制 ID 文本 | ⚠️ 标准付费，仅结构级确认 |
| 5 | 通用 agentic 工具调用是否触发深度合成 Art.20 安全评估 | ⚠️ 无官方解释 |
| 6 | 通用 agent 按 Art.6(3) 非高风险 | 法条上成立；实际边界待 2026-02-02 实施规范（状态待核） |
| 7 | 中国是否采用 ISO 42001 为国家标准 | ⚠️ 未确认 |
| 8 | GB 45438-2025 技术细节 | ⚠️ 标准号已确认，内容待官方文本 |

### 下一步

- 若需把合规义务量化为控制成本:见 [经济损失与 ROI 模型（05 章 5.2）](05-conclusions.md)
- 若需合规证据的技术支撑:见 [检测与响应资产包（02 章 2.9）](02-defenses.md)（审计日志章节）

---

### 官方来源

- EU AI Act：https://eur-lex.europa.eu/eli/reg/2024/1689/oj
- GPAI Code of Practice：https://digital-strategy.ec.europa.eu/en/policies/ai-code-practice
- 《生成式人工智能服务管理暂行办法》：https://www.cac.gov.cn/2023-07/13/c_1690898327029107.htm
- 《算法推荐管理规定》：https://www.cac.gov.cn/2022-01/04/c_1642894606364259.htm
- 《深度合成管理规定》/《标识办法》：https://www.cac.gov.cn（2022-12-11 / 2025-03-14 页，精确 URL 待核对）
- ISO/IEC 42001:2023：https://www.iso.org/standard/81230.html

## 3.8 标准演进提案

> 本节为**建议/提案**,非已发布标准事实。所有"建议"明确标注"提议/待讨论",不得表述为既有标准。

### 执行摘要（BLUF）

**如果只记住一件事**：现有 AI 安全标准是**为"单模型应用"设计的,还没跟上 agent 的独特风险**——agent 的记忆、工具权限、委派链、跨 agent 传播在 OWASP ASI Top 10 和 MITRE ATLAS 里要么缺失、要么没有严重度模型。**标准的滞后意味着企业无法用标准驱动优先级(哪个风险先修)或采购(供应商要达到什么水平)。**

**三个关键发现**：
1. **OWASP ASI Top 10 是扁平列表,无严重度分级**——CISO 无法用它回答"先修哪个",急需 agent 化 CVSS。
2. **"高风险 agent"在全球定义不一致**——EU 按用途、中国按服务性质、美国是州级碎片化。一个 **SAE-J3016 式自主等级阶梯(L0-L5)** 可能是跨法域的共同尺度。
3. **MCP/A2A 安全仍是"最佳实践"而非规范要求**——OX Security 的"by-design"缺陷(V78)证明把 best-practices 提升为规范是当务之急（详见 §五）。

**行动建议**：这些提案的价值在于**向标准组织提交输入**(OWASP ASI TG、ATLAS GitHub、NIST、ISO SC 42)——它们是可行动的研究方向,不是空谈。

---

### 一、OWASP ASI Top 10 → 2027 修订建议

**现状**：ASI01-ASI10（2025-12-09 发布）为扁平列表,无严重度模型（见 3.2）。

**核心问题**：CISO 打开 ASI Top 10,看到 10 项风险,但没有"哪个更严重/先修哪个"的答案。这与我们 12 章风险登记表的需求直接相关——**标准需要能驱动优先级**。

| 缺口 | 建议（提案） |
|------|------------|
| 无严重度/优先级模型 | **Agent-adapted CVSS**：因子 = 工具广度、数据敏感性、自主级别、人类监督强度、委派深度、恢复成本 |
| 蠕虫/自我传播缺失 | 新增 **ASI11 Propagation**（自我复制注入,Word/Copilot 蠕虫为证明案例,V50） |
| 记忆机密性 vs 投毒混淆 | 将 ASI06 扩展为记忆信道 + 持久化攻击独立条目 |
| 编排层缺失 | 新增编排攻击面：任务分解、计划执行、委派链 |
| 身份生命周期缺失 | 新增 agent 入职/离职、联邦身份、token passthrough 审计 |
| 无基准映射/CWE 层 | 建立 ASI ↔ AgentDojo/ASB 可测性映射 + 候选"agentic CWE"清单 |

### 二、MITRE ATLAS 新增 agent 技术

**现状**：16 tactics / 178 techniques（[atlas.mitre.org](https://atlas.mitre.org/)），V9 已核验关键 ID。

**核心问题**：ATLAS 是 ATT&CK 的 AI 版,但**缺少 agent 特有的记忆、编排、传播技术**,且案例库是回顾式的,2025-26 的事件(如 Flowise、Mercor、Word 蠕虫)未见导入 ATLAS 案例库（截至 2026-08 检索）。

| 缺失技术 | 建议新增（提案） |
|---------|----------------|
| 记忆子系统篡改 | 区别于 AML.T0020 的记忆区污染技术 |
| 编排操纵 | 计划/任务劫持技术 |
| agent 间传播 | 跨 agent 自我复制/污染技术 |
| 身份欺骗 | 互 agent 身份伪造技术 |
| MCP 特定技术 | 超越 AML.T0010.005 的 MCP server/tool 特有技术 |
| STIX 事件导入 | 建立 2025-26 事件 → ATLAS 案例库的机器可读导入流程 |

### 三、NIST AI 600-2 Agentic AI Profile（提案）

**现状**：AI RMF 1.0（AI 100-1）+ AI 600-1 GenAI Profile 早于 agentic 系统（03 章 3.4）。

**核心问题**：RMF 的四个职能(Govern/Map/Measure/Manage)对 agent 没有具体指引;尤其 **Measure(测量)缺少 agent 专项指标目录**——没有指标就无法度量、无法管理。

| RMF 职能 | Agent 专项建议（提案） |
|---------|----------------------|
| Govern | agent 自主级别文档化、监督委员会、autonomy 等级角色分配 |
| Map | 用 OWASP ASI + ATLAS 作为风险分类学输入 |
| Measure | agent 专项指标：注入 ASR（AgentDojo/ASB）、工具误用率、审批/覆写率、PII 泄露率、egress 例外数 |
| Manage | 风险处置计划、残余风险接受、监控 |

**额外建议**：**autonomy ladder（L0-L5）**——SAE-J3016 式自主等级阶梯,作为"高风险 agent"的缺失共同度量;人类监督比例指引（基于 V56 的 93% 审批通过率现象——即大量权限请求被用户自动批准，Anthropic 将其归因为"审批疲劳"，本报告沿用此解读，属厂商口径）。

### 四、ISO/IEC 42001 agent Annex（提案）

**现状**：42001 的 38 项 Annex A 控制为组织级,无工具使用策略/agent 身份/委派/记忆（见 [合规落地映射（3.7 节）](#37-合规落地映射义务控制) 3 节）。

**核心问题**：企业获得 42001 认证,但认证**不测试 agent 特有安全**——体系"看起来合规",实际 agent 风险未覆盖。

| 缺失 | 建议（提案） |
|------|------------|
| 工具使用策略 | 新增 agent 工具白名单/批准控制 |
| agent 身份 | 新增 agent 身份生命周期/凭证控制 |
| 委派 | 新增委派链与权限继承控制 |
| 记忆 | 新增 agent 记忆数据治理控制 |
| 认证 | 建立 agent 安全 conformance 测试套件与审计员技能要求（42006 扩展） |

**落地路径（提案）**：向 ISO/IEC JTC 1/SC 42 提交 NWIP/TR"Security of agentic AI systems"。

### 五、MCP / A2A 规范化安全（提案）

**现状**：MCP 安全是版本化 best-practices 教程（V58）；A2A v1.0 规范中 agent 间认证能力尚不完善（本报告基于规范审查的判断，具体缺口以 A2A 规范最新版为准）。

**核心问题**：OX Security 的"by-design"发现(V78)证明,把 best-practices 提升为**规范要求**是当务之急——教程性质的文档无法约束实现。

| 协议 | 建议规范化（提案） |
|------|-------------------|
| MCP | 服务器认证/签名、每服务器信任配置、OAuth 2.1 + PKCE + audience 校验（token passthrough 修复）、SSRF/egress 强制、工具描述清洗（防元数据投毒）、审计钩子 |
| A2A | agent 间认证、能力证明、委派限制、不可否认性、审计 |
| Agent SBOM | CycloneDX/SWID 扩展：模型、工具、提示、记忆、插件清单（映射 SP 800-218A） |

### 六、"高风险 agent"定义协调（提案）

**核心问题**：四个法域对"高风险 agent"的定义不可调和——这是跨法域合规的最大障碍。

| 法域 | 现状 | 协调建议（提案） |
|------|------|----------------|
| EU | Annex III 面向产品用途；GPAI 阈值基于算力 | 基于"自主 × 爆炸半径"定义高风险 agent；Art.6 实施规范（2026-02-02 期限，状态待核）为关键节点 |
| 中国 | 基于服务（舆论属性/社会动员） | TC260 指南纳入 agent 自主与工具安全措施 |
| 美国 | 州级碎片化（Colorado/California） | 联邦层面采纳 autonomy ladder |
| 共通 | — | **autonomy ladder（L0-L5）+ blast radius 作为跨法域共同尺度** |

### 下一步

- 若需把"标准滞后"量化成企业风险:见 [风险登记表（01 章 1.7）](01-threats.md)
- 若需了解现状标准:见本章 3.1-3.6

## 3.9 开放研究议程

> 本节为**开放研究问题梳理**。所有引用的论文/基准注明 arXiv ID；现有结论数字与原文核对（延续核验纪律）；研究假设明确标注"待验证"。

### 执行摘要（BLUF）

**如果只记住一件事**：agent 安全的**最大研究空白不是"更多攻击手法",而是"没有可靠的测量与证明手段"**——现有基准是静态、防御盲的;防御依赖启发式而非可证边界;多智能体安全停留在案例描述而非理论。**没有测量,就没有优先级;没有理论,就无法规模化防御。**

**三个关键发现**：
1. **基准 2.0 是优先级最高的研究方向**——现有 AgentDojo/ASB 用静态攻击、无攻击预算、合成工具,系统性高估模型鲁棒性(真实 MCP 上 ASR 差异显著)。需要 ASR@budget 和自适应攻击者。
2. **多智能体安全缺理论**——四篇 2026 新论文(ChannelGuard/SafeFlow/ChainWatch/When Prompts Control Robots)都证明了现象,但没人把"安全模型组合不出安全系统"形式化为定理。这是理论空白,也是基金级机会。
3. **防御有效性缺独立复现**——厂商数字(Auto Mode 83%/0.4%)驱动架构决策,但没人独立复现;指令层级在工具上下文中的退化是开放问题。

**行动建议**：如果你是研究者,优先做**可证无外泄架构**与**记忆子系统威胁模型**——两者都是基金级且目前无人占领。

---

### 一、基准 2.0:自适应与成本感知

**现状局限**（见 3.5）：AgentDojo（97 任务/629 用例）、ASB（最高 ASR 84.3%）、AgentAttackBench、MCPTox（45 服务器/353 工具）均为**静态、防御盲**基准。

**核心问题**：这些基准报告裸 ASR,但攻击者会自适应——看到你的防御 classifier 后调整攻击。真实世界攻击有预算(查询次数/token 成本),基准却不计。这导致**"模型很稳"的结论被系统性高估**。

| 局限 | 建议研究方向（待验证） |
|------|----------------------|
| 静态攻击、无自适应对手 | 观测防御方 classifier 并调整的自适应攻击者（参考 Andriushchenko et al., arXiv:2404.02151；AgentHarm arXiv:2410.09024） |
| 无攻击预算/成本 | **ASR@budget**：按攻击者预算（token/查询数）报告成功率,建立攻防成本曲线 |
| 合成工具 | 真实 MCP 集成（MCPTox 显示真实 vs 合成 ASR 差异显著,arXiv:2508.14925） |
| 无规避鲁棒性维度 | 编码/翻译/跨语言规避测试 |
| 无长周期/恢复任务 | 会话间持久性、记忆投毒跨会话 ASR |
| 无纵向再污染控制 | 防基准泄露的持续刷新机制 |

**建议产出（提案）**：HELM 式独立运营的版本化排行榜。

### 二、多智能体组合安全理论

**现象**：ChannelGuard"安全模型组合不出安全多智能体系统"（arXiv:2607.19430）、SafeFlow（arXiv:2607.25255）、ChainWatch（arXiv:2607.19432）、When Prompts Control Robots（arXiv:2608.00747）——四篇均为 2026-07/08 全新预印本（见 01 章 1.5）。

**核心问题**：这些论文**证明现象,但没给理论**。我们需要知道:哪些安全属性在组合下保持?委派何时等于提权?——否则无法规模化设计安全的多智能体系统。

**开放问题（待验证）**：
- **组合性**：哪些安全属性（机密性/授权/终止性）在 agent 组合下保持？ChannelGuard 负结果应形式化为定理 + 精确失效条件
- **委派信任**：agent B 执行 agent A 委派的工具时,能力继承何时等价于权限提升？
- **信息流**：agent 消息总线上的信息流安全（SafeFlow 是实例,需推广）
- **拓扑**：限定级联爆炸半径的网络拓扑；agent swarm 的拜占庭/自传播失效模型

**建议产出**：形式化模型 + 定理 + 在生产框架（AutoGen/LangGraph/A2A）上验证。

### 三、Agent 记忆子系统安全模型

**现象**：记忆是持久的第二上下文（Claude Memory Heist,V79；AgentPoison <0.1% 投毒率 >80% ASR,V26）。

**核心问题**：现有研究只覆盖"投毒"这一面,但记忆子系统的**持久性、来源追踪、重放、机密性、擦除**都未系统研究。而记忆正是 agent 与其他 AI 应用最大的区别之一。

**威胁模型维度（待验证）**：
- **来源/污点**：来自不可信工具输出/网页内容的记忆条目须污点标记并可隔离
- **重放/再注入**：注入内容跨会话持久 → 递归投毒；应测**跨会话** ASR 而非单轮
- **机密性**：跨会话 PII 聚合；记忆库差分隐私
- **擦除**：GDPR Art.17 与持久记忆冲突——技术遗忘、回滚、版本化记忆

**建议产出**：记忆威胁模型 + "MemoryDojo" 类基准 + 缓解原型。

### 四、防御有效性研究

**核心问题**：业界依赖的防御有效性证据,要么是厂商自测(Auto Mode 83%/0.4%),要么是单一论文——缺少跨模型、跨工具的独立评估。

| 研究方向 | 关键问题（待验证） |
|---------|------------------|
| 指令层级（instruction hierarchy） | OpenAI 的层级在工具上下文中的退化程度（Meta AI 接管是反面案例）；跨模型/跨工具系统评估 |
| 训练期防御 | 安全 RLHF/DPO 用于工具使用、计划验证训练——对**新型工具集**的泛化与回归 |
| 分类器鲁棒性 | LlamaGuard/Prompt Guard/Anthropic classifier 的规避鲁棒性（改写/编码/翻译）系统性测试 |
| 厂商声明复现 | Auto Mode 83% 拦截/0.4% 误报（V56）独立复现——该数字驱动架构决策 |

### 五、攻击前沿与可复现性

| 方向 | 开放问题（待验证） |
|------|------------------|
| Agent 蠕虫 | Morris II（arXiv:2406.08317）+ Word/Copilot 蠕虫（V50）：传播率、低配额隐形复制、跨协议蠕虫（MCP→email→A2A）、canary token 遏制 |
| 供应链规模化 | MCP server 农场、依赖混淆、工具元数据投毒（MCP-ITP 84.2% ASR / 0.3% 检出,V25）、带签名权重溯源 |
| 可复现性 | 环境固定（模型/工具版本）、种子控制、LLM-as-judge 验证、泄露检测、持续刷新 |

### 六、论文/基准追踪清单（供持续关注）

- 期刊/会议：AISec @ CCS、USENIX Security、IEEE S&P、NDSS；COLM/ICLR/NeurIPS agent-safety workshops
- arXiv 类别：cs.CR / cs.MA
- 标准：OWASP Agentic TG、MITRE ATLAS 案例库
- 厂商红队博客：Anthropic、OpenAI、OX、JFrog

### 七、基金级开放问题（建议）

1. **可证无外泄 agent 架构**（provable exfiltration-free）：把 Lethal Trifecta 从启发式变为形式条件
2. **自传播多智能体威胁的遏制**
3. **工具权限系统的形式化基础**
4. **持续自适应红队**
5. **记忆隐私 vs 效用**
6. **全球 agent 事件数据集**（桥接学术与标准组织）

### 下一步

- 若需落地已成熟的部分:见 [MCP 安全实操包（02 章 2.10）](02-defenses.md)（dual-prompt 等已是实践而非研究）

---

