---
title: 真实事件案例与生态格局
chapter: 4
parent: ai-agent-security-report.md
last_updated: 2026-08-18
status: 完成
prev: 03-standards.md
next: 05-conclusions.md
---

> 本页为《AI Agent 领域安全挑战与应对方法调研》第 4 章。[上一章 03-standards.md](03-standards.md) · [下一章 05-conclusions.md](05-conclusions.md) · [返回报告概览](00-overview.md)

---

# 四、真实事件案例与生态格局（Incidents & Ecosystem）


## 4.1 真实安全事件案例（全部经逐条核验）

> 下表 18 起事件：**17 起已证实**、1 起（2025.03 香港深伪语音案）细节仅获二手来源证实。另有 1 条（NVIDIA Chat with RTX）因无法证实已不列入正文，仅留档供参考（见末行）。

| 时间 | 事件 | 类型 | 影响 |
|------|------|------|------|
| 2023.02–03 | Bing Chat/Sydney 间接提示注入（网页隐藏指令操控对话） | 间接注入 | PoC |
| 2023.05 | 中国"AI 换脸"视频诈骗案（包头） | Deepfake 欺诈 | 约 430 万元（警银联动追回 330 余万，净损<430万；被冒充者为**熟人**） |
| 2024.01 | 香港 Deepfake CFO 视频会议诈骗（15 笔转账，涉事公司为 Arup） | Deepfake 欺诈 | 2 亿港元（约 2560 万美元） |
| 2025.01–03 | DeepSeek 云数据库泄露（配置错误，Wiz Research 发现 100 万+ 日志行含对话/API key） | 云配置错误 | 真实数据暴露 |
| 2025.03 | 香港 Deepfake 语音银行诈骗 | Deepfake 语音 | **⚠️ 仅找到二手来源，具体"~$2500 万美元/绕过声纹认证"细节无法在原始来源证实** |
| 2025.04 | DeepSeek 未经同意向境外（火山引擎）传输韩国用户数据/提示词，韩 PIPC 责令整改 | 数据跨境违规 | 监管处罚 |
| 2025.06 | 麦当劳 AI 招聘机器人（Paradox McHire/"Olivia"）弱口令"123456"可访问约 6400 万求职者记录 | 弱认证 | **研究者披露的访问权限，非确认的恶意利用** |
| 2025.06 | Microsoft 365 Copilot "EchoLeak"（CVE-2025-32711）零点击提示注入→数据外泄 | 间接注入/越权 | CVSS 9.3，已修复 |
| 2025.06 | "Skynet"提示词注入型恶意软件（Check Point） | 对抗 AI 检测 | **真实样本，但注入对实测模型（o3/GPT-4.1）未生效** |
| 2025.12–2026.02 | 墨西哥政府数据泄露（Claude 辅助自动侦察+漏洞开发） | AI 辅助攻击 | 约 150GB 税务/选民数据 |
| 2026.02 | OpenClaw 邮箱删除事故（Meta 研究员 Summer Yue 的代理无视"停止"指令批量删信） | 自主代理失控 | 真实事故 |
| 2026.03 | Meta 内部 AI Agent 数据泄露（错误工程建议→海量敏感数据对内开放约 2 小时，Sev-1） | Agent 错误建议 | 真实企业内事件 |
| 2026.03–04 | Claude Code 源码泄露 + 钓鱼恶意仓库（npm source map 暴露 ~51.3 万行源码；伪造"泄露版"仓库分发 Vidar/GhostSocks 恶意软件） | 供应链+社工 | 真实事件 |
| 2026.03–04 | Mercor / LiteLLM 供应链事件（Mercor 官方确认 3-31 遭恶意 LiteLLM 依赖供应链攻击，Meta 暂停合作） | 供应链 | 波及多家 AI 实验室 |
| 2026.04 | Flowise CVE-2025-59528 在野利用（CustomMCP 注入 JS → RCE，CVSS 10.0） | Agent 平台 RCE | **1.2 万–1.5 万个暴露实例** |
| 2026.04 | GrafanaGhost（Noma Security）：诱导渲染外部图片以 URL 参数外泄企业数据（相关 CVE-2026-27876） | 间接注入+外泄 | 已部分修复 |
| 2026.06 | Meta AI 支持机器人账号接管（"把目标账号邮箱换成我的"绕过恢复流程） | AI 客服社工 | 真实账号接管 |
| 2026.07 | Word/Copilot 自复制提示词注入蠕虫（Håkon Måløy 负责任披露；微软 144 天未给出全类别修复） | 自复制注入 | 研究披露 |
| 2024.06 | NVIDIA "Chat with RTX" 恶意网页→本地命令执行演示 | 研究演示 | **未获证实，不列入正文**（ChatRTX 确有代码执行 CVE-2024-2624/2625 及 NVIDIA AI Red Team 的 LangChain 注入→RCE 演示，但"2024-06 特定演示"无一手来源） |

**重要提示**（据 OWASP GenAI Q1'26 报告原文）：2025 年以来，AI 相关安全事件的**绝大多数没有对应 CVE**——它们源于配置错误、设计缺陷（代理自主性、信任边界）、供应链弱点和数据流操纵，而非离散代码漏洞；只有嵌入 AI 平台的经典软件漏洞（如 Flowise RCE）才持续获得 CVE 编号。

## 4.2 重要研究论文与演示攻击

| 研究 | 要点 | 来源 |
|------|------|------|
| Greshake et al. IPI | *Not what you've signed up for*，首次系统化提出间接注入，演示 Bing Chat/代码补全引擎 | arXiv:2302.12173（AISec '23） |
| AgentPoison（NeurIPS 2024） | <0.1% 投毒率、>80% 攻击成功率、良性影响<1% | arXiv:2407.12784 |
| AgentDojo | 97 任务/629 安全用例动态攻防评测 | arXiv:2406.13352 |
| HouYi | 36 个真实应用 31 个可注入；10 家厂商确认（含 Notion） | arXiv:2306.05499 |
| CyberSecEval（Purple Llama） | 模型不安全代码约 30%；"26–41%"属 CyberSecEval 2 的注入成功率 | arXiv:2312.04724 / 2404.13161 |
| 200+ Custom GPTs 注入评估 | 全部可注入，可窃取系统提示词与上传文件 | arXiv:2311.11538 |
| OpenAI 红队 | 系统性演示 Agent 工作流数据外泄，论证人类监督必要性 | OpenAI 官方研究（"Assessing Prompt Injection Risk in AI Agents"，2025） |
| CAIN / PARASITE | 定向提示劫持：仅对特定问题返回恶意答案（v1 标题 *CAIN*，后更名 *PARASITE*，内容一致） | arXiv:2505.16888 |
| MCP 纵深防御框架 | *Enterprise-Grade Security for the Model Context Protocol (MCP)*，作者 AWS（Vineeth Sai Narajala）+ Intuit（Idan Habler），7 类威胁含工具投毒/数据外泄/C2/身份破坏 | arXiv:2504.08623 |

## 4.3 安全厂商与开源工具生态

- **专注 AI/Agent 安全的商业厂商**（含已被收购者，并购明细见 4.6 §三）：Lakera、Prompt Security、Invariant Labs、Robust Intelligence、Protect AI、Aim Security、TrojAI、Securiti AI（均已被收购），以及未收购的 Lasso Security、HiddenLayer、PromptArmor、Noma、Aqua Security（OWASP GenAI 项目赞助商）；事件驱动型：Wiz Research、Zscaler ThreatLabz、Check Point Research、Palo Alto Unit 42。
- **传统平台厂商的 AI 安全能力**：Wiz（CSPM+AI-SPM）、Orca、CrowdStrike/SentinelOne 的 AI-SPM/CNAPP、ArmorCode（ASPM）。
- **开源与开放工具/标准**：OWASP LLM Top 10 2025 + Top 10 for Agentic Applications 2026 + FinBot CTF；NVIDIA NeMo Guardrails（新路径）、Meta LlamaGuard / Prompt Guard、Guardrails AI、Rebuff（已归档）、Invariant Labs MCP Scan（→Snyk）。

## 4.4 市场与行业趋势

- **Gartner 预测**："到 2028 年，25% 的企业安全事件将可追溯到 AI Agent 滥用"出自 Gartner **2024-10-22** 发布的《Top Predictions for IT Organizations and Users in 2025 and Beyond》，**并非 2025-10-07** 新闻稿；且"2024 年 <1%"基线未出现在该新闻稿中（无法从一手来源证实，引用需谨慎）（[Gartner 2024-10-22](https://www.gartner.com/en/newsroom/press-releases/2024-10-22-gartner-unveils-top-predictions-for-it-organizations-and-users-in-2025-and-beyond)）。
- **Gartner 预测 2**：2025-06-25，>40% Agentic AI 项目 2027 年底前被取消。
- **威胁从理论走向实战**（据 OWASP Q1'26）：核心结论是"从模型级防护转向系统/身份/运维级控制"，攻击者已瞄准 Agent 身份、编排层与供应链（墨西哥事件、Mercor、Flowise 均为证据）。
- **2025–2026 趋势判断**（本报告基于 4.1 事件与 4.4 预测的分析判断，非可核验统计数据）：AI 攻击自动化降低攻击门槛、deepfake 欺诈规模化（香港两案）、供应链成为主战场（MCP/依赖/数据供应商）、"人类过度信任 AI 输出"成为一致弱点（Meta 事件、ASI09）。

## 4.5 经验教训总结

1. **"致命三要素"（Lethal Trifecta）**：当 Agent 同时具备私有数据访问 + 接触不可信内容 + 外泄渠道时，注入几乎必然导致数据外泄。最可靠缓解是**确定性切断外泄通道**（OpenAI Lockdown Mode 即此思路）。
2. **不要用 AI 做唯一裁判**：凡是"AI 决策"参与安全判断或数据流出，都需叠加确定性校验与人的审批。
3. **最小权限与最小自主（least privilege & least agency）**：默认过度授权是代理风险的主要来源；Agent 身份应像管理员特权一样管理。
4. **破坏性操作必须硬确认**：OpenClaw 事故说明删除/转账/发布类权限不能依赖用户"赶回去按停止"。
5. **供应链是主战场**：工具描述投毒、恶意 MCP 服务器、伪造"泄露版"仓库、AI 数据供应商（LiteLLM/Mercor）——SBOM、依赖锁定、签名与来源验证成为必选项。
6. **模型训练在进步，但不可依赖**：HackMyClaw 挑战中 6000 次尝试失败（见核验表 V32）被解读为前沿模型防注入能力提升（解读性判断，非确定结论），但不能因"暂时没被攻破"就解除纵深防御。
7. **事件可见性缺口**：多数 Agent 安全事件无 CVE、无监管上报渠道，企业只能依赖自身可观测性（日志 Agent 工具调用、外部请求、权限变更）与 OWASP 社区情报来感知风险。

## 4.6 市场规模与竞争格局

> 4.3 的厂商生态在此补充市场量化视角。所有数字为**分析师预测/媒体报道**,非既成事实；每个数字标注来源与口径；未披露项标注"未披露"。**严格区分"agent 专属"与"AI 安全大盘"口径**（"5% 规则"警惕）。

### 执行摘要（BLUF）

**如果只记住一件事**：AI Agent 安全是一个**真实但很小、增长极快**的市场——分析师预测 2026 年 agent 专属安全约 **$1.65B**,预计以 **42% CAGR** 增长到 2032 年的 **$13.52B**(MarketsandMarkets,预测值)。但要清醒:**这约只占"AI 安全"大盘的 5-10%**,而"AI 安全"又只占整体信息安全市场(2026 年 $248.9B)的一个零头。

**三个关键发现**：
1. **市场正在快速并购整合**——2025-04 至 2026-06 约 15 个月内已有 7 家纯玩家被收购（明细见 §三 M&A 表；Robust Intelligence→Cisco 在 2024-08，略早）。这既是"验证了退出机会"的牛市信号,也可能意味着"没有独立市场、只是大厂功能"的熊市信号——两种解读都需要证据。
2. **大多数并购价格是媒体估计,官方未披露**——$300M/$250M/$400M/$1.7B 等数字互相冲突,引用时须标注"媒体价,未证实"。
3. **最大的空白市场可能不在"检测"而在"供应链与身份"**——MCP 注册表安全、Agent 身份/OAuth、Agent 专用 SIEM 都是低密度高价值区,但都面临云厂商/大模型厂商原生功能推进的平台风险。

**投资者/创始人警示**：在投入前先验证"agent 安全是否是一个独立采购品类"——目前它很可能只是 AI 安全/数据安全 RFP 的一个功能项,而非绿野采购类别。

---

### 一、市场有多大?（TAM/CAGR,口径是关键）

> 下面的数字来自不同机构,口径差异巨大。"AI 安全"类数字是 broad 口径(含用 AI 做安全 + 保护 AI),"Agentic AI Security"才是真正接近 agent 的细分。**引用任何数字前先确认口径。**

| 细分口径 | 数据 | 机构 | 日期 | 类型 |
|---------|------|------|------|------|
| **Agentic AI Security**（最接近 agent 安全） | $1.65B (2026) → $13.52B (2032)，CAGR **42.0%** | MarketsandMarkets | 2026-04 | 预测 |
| Agentic AI in Cybersecurity | CAGR **36.4%** | Market.us | 2026-07 | 预测 |
| Securing AI（Gartner） | $15.6B (2025) → $37.6B (2030)，CAGR **18.5%** | Gartner 2Q26 | 2026-06-25 | 预测 |
| AI in Cybersecurity | $22.37B (2025) → $50.83B (2031)，CAGR **14.8%** | MarketsandMarkets | 2026 | 预测 |
| AI in Cybersecurity | $31.5B (2025) → $182.9B (2033)，CAGR **24.7%** | Grand View | 2026 | 预测 |
| AI in Cybersecurity | $34.09B (2025) → $213.17B (2034)，CAGR **21.71%** | Fortune BI | 2026-07 | 预测 |
| 总信息安全市场（背景） | $248.9B (2026) → $372.6B (2030)，CAGR **10.7%** | Gartner 2Q26 | 2026-06 | 预测 |

#### 如何解读这些数字（"5% 规则"）

- **agent 安全 ÷ AI 安全 ≈ 5-10%**：M&M agentic 2026 基准 $1.65B ÷ AI 安全大盘（M&M 2025 基准 $22.37B，年份口径略有错位）≈ 7.4%；÷ Gartner securing AI $15.6B ≈ 10%。
- **因 CAGR 差异,占比会快速上升**：agent 安全 42% vs AI 安全大盘 15-25%,到 2030 年代初期 agent 安全占比可能翻倍（推算，非精确预测）。
- **⚠️ 口径警告**：M&M 的 agentic 口径**含基础设施层安全**(报告原文称基础设施层占最大份额),不是"纯 agent 运行时安全"。真正的 agent 运行时安全细分可能更小,且**无公开的独立权威口径**。

> 注：表中 CAGR 为各机构公布值（计算期长不同：Gartner 4 年、Fortune BI 9 年等），直接采用来源口径，与表中端点值的手算 CAGR 有细微出入。

---

### 二、谁在融资?（AI 安全厂商融资）

> 融资数据有助于判断赛道热度与玩家实力。以下为公开报道金额,估值普遍未披露。

| 公司 | 轮次/金额 | 日期 | 备注 |
|------|-----------|------|------|
| Lasso Security | Seed **$6M** | 2023-02 | 后成为 M&A 焦点 |
| HiddenLayer | Series A **$50M**（累计 ~$57M） | 2023-09 | |
| PromptArmor | **无公开融资数据** | 2025-04 发布 | 未披露 VC 轮 |
| Securiti AI | A $31M / B $50M / C $75M | 2019-2022 | 后被 Veeam $1.73B 收购 |
| Noma Security | Series A **$32M** | 2024-11 | |
| Aim Security | Seed $10M / A $18M | 2024 | 后被 Cato ~$350M 收购 |
| Protect AI | Series B **$60M**（累计 ~$108.5M） | 2024-07 | 后被 PANW $500M+ 收购 |
| TrojAI | Seed **$5.75M** | 2024-04 | 后被 A10 收购 |
| Pillar Security | **$9M** | 2025-04 | |
| 瑞莱智慧（中国） | A 轮超 3 亿元 RMB / B 轮数亿元 | 2021-2026 | 估值数十亿元 RMB |
| 中科睿鉴（中国） | 近亿元 / 中国电信入股 | 2024-2026 | |

**解读**：种子/A 轮集中在 $6M-$60M 区间,是典型的企业安全早期赛道规模。**多家在 1-3 年内就被收购**——说明退出通道通畅,但也暗示独立规模化困难。

---

### 三、谁收购了谁?（M&A,价格普遍未证实）

> ⚠️ **重要**：以下价格多为**媒体报道**,官方普遍未披露;部分来源冲突(如 Prompt Security $250M vs $300M)。**引用时标注"媒体价,未证实"**,不得当作官方事实。

| 标的 → 收购方 | 日期 | 媒体报道价 | 备注 |
|---|---|---|---|
| Lakera → Check Point | 2025-09-16 | ~$300M | 官方未披露 |
| Invariant Labs → Snyk | 2025-06-24 | **未披露** | Snyk 官方公告 |
| Prompt Security → SentinelOne | 2025-08-04 | $250M（另一来源 $300M） | 冲突 |
| Robust Intelligence → Cisco | 2024-08-26 | ~$400M | 官方未披露 |
| Aim Security → Cato Networks | 2025-09-03 | ~$350M | 官方未披露 |
| Securiti AI → Veeam | 2025-10-21 | $1.7B-$1.73B | 较可靠(Reuters) |
| Protect AI → Palo Alto Networks | 2025-04 公告 | $500M+ | 早期传 $700M |
| TrojAI → A10 Networks | 2026-06 | **未披露** | |
| Astrix → Cisco（进行中） | 2026-04 报道 | 传 ≥$250M | 未完成 |

#### 解读:为什么大厂在扫货

- **Check Point** 要 LLM 防火墙(Lakera);**Snyk** 要 appsec 邻接能力(Invariant);**SentinelOne** 要端点 AI 防御(Prompt Security);**Palo Alto** 要 AI-SPM(Protect AI)。
- 这验证了:agent 安全能力正被并入**平台级安全套件**,而非作为独立产品存在——对创业者的含义:要么做成"跨平台中立层",要么成为平台功能的候选。

---

### 四、竞争格局:谁在做什么?（厂商定位）

> 厂商自我归类常跨品类;"LLM 防火墙/guardrails/AI-SPM" 边界模糊。下表基于官方产品页与 MarketsandMarkets 报告归类。**这是导航表,不是裁决**——每个品类后附"怎么看"。

| 厂商 | 主要品类 | 宣称买家 | 怎么看（简评） |
|------|---------|---------|--------------|
| Lakera（→Check Point） | LLM 防火墙 / GenAI 安全 | 企业 | 实时注入防御,已被 Check Point 收编 |
| Prompt Security（→SentinelOne） | GenAI/LLM 安全平台 | 企业安全 | 覆盖 250+ 模型 |
| Invariant Labs（→Snyk） | Agentic 安全 / agent 运行时 | DevSecOps | MCP 扫描能力被 Snyk 吸收 |
| Robust Intelligence（→Cisco） | 模型验证 / 对抗鲁棒性 | 模型用户 | 模型红线测试 |
| Lasso Security | GenAI 数据保护 | 企业 | 上下文数据防泄漏 |
| HiddenLayer | AI 安全 / 模型保护 | 企业 AI 团队 | guardrails + 模型扫描 |
| PromptArmor | 第三方 AI 风险 / 注入防护 | 企业 | 评估 + 监测 |
| Securiti AI（→Veeam） | 数据安全 + AI 治理 | 数据/隐私团队 | 后被 Veeam 收购 |
| Wiz | CSPM + AI-SPM | 云安全团队 | 平台型 AI-SPM |
| Zscaler | SASE/零信任 + AI 保护 | 网络/零信任 | 网络侧切入 |
| Noma Security | AI 应用安全 / AI-SPM | 应用安全团队 | |
| Aim Security（→Cato） | GenAI/agentic 安全 | 企业安全 | 被 Cato 收购 |
| Protect AI（→PANW） | AI-SPM + MLSecOps | 平台安全/ML | 被 PANW 收购 |
| TrojAI（→A10） | 模型风险 / 对抗测试 | 模型团队 | |
| Pillar Security | AI agent 原生安全 | 部署 agent 企业 | 较新玩家 |
| 开源/平台内置 | NeMo Guardrails 等 | 开发者 | 平台内置,非独立 SKU |

#### 品类饱和度速判

- **拥挤且正在整合**：guardrails / LLM 防火墙(Lakera、Prompt Security、Invariant、Robust Intelligence 全部被收购)
- **偏空**：MCP 供应链安全、Agent 身份/OAuth、Agent 专用 SIEM——低密度但平台风险高

---

### 五、空白市场清单（创业者视角,假设待验证）

| 空白机会 | 现状 | 平台风险 | 判断 |
|---------|------|---------|------|
| **MCP 供应链安全**（签名/扫描/SBOM） | 密度低;Invariant→Snyk 后无人独占 | 中（Anthropic 官方 registry 在推进） | 机会与风险并存 |
| **Agent 专用 SIEM/检测** | 近零;Splunk 等缺 agentic 遥测 | 低（建设成本高） | 高机会但重投入 |
| **Agent 身份/SSO/OAuth** | MCP 规范安全章节仅文档化 | 高（Microsoft/Anthropic 在圈） | 谨慎 |
| **记忆安全**（mem0/Zep 无安全层） | 研究仅限论文 | 低-中 | 早期机会 |
| **Agent DLP / egress 控制** | 仅大厂（OpenAI Lockdown）有 | 低（实施难度高） | 高价值 |
| **合规证据自动化**（EU Art.14/15 → 证据工件） | 无成熟映射工具 | 中 | 政策驱动,真实需求 |
| **Agent 保险/承保技术** | 无索赔数据可承保 | 高（估计 2027+ 才成市） | 过早 |

---

### 六、无公开数据 / 口径标注

| 项目 | 状态 |
|------|------|
| PromptArmor 融资额 | **无公开数据** |
| Invariant→Snyk、TrojAI→A10 对价 | **未披露** |
| Check Point/SentinelOne/Cisco 官方对价 | 官方均**未披露**（表内为媒体价） |
| 各厂商 ARR/收入 | 除 HiddenLayer 非官方估 $34.9M 外**均无公开数据** |
| 纯"agent 运行时安全"独立 TAM | **无公开权威口径** |
| 中国 agent 安全 TAM | **无公开权威数据** |

### 七、关键警示

1. **口径陷阱**：Gartner "securing AI" 含 agent 在内的 broad 口径,不能直接当 agent 安全 TAM。
2. **媒体价格未证实**：M&A 价格均未经官方确认,部分来源冲突。
3. **国内玩家口径不同**：RealAI/中科睿鉴主打"AI 安全/伪造检测",与西方"agent 安全"非同一细分。
4. **市场可能尚未成形**："agent 安全"可能是 AI 安全/数据安全 RFP 的功能,而非独立采购品类——**投入前先验证是否存在绿野 RFP**。

### 下一步

- 若需风险视角:见 [风险登记表（01 章 1.7）](01-threats.md)
- 若需厂商/开源工具细节:见 [02-防御方法与最佳实践](02-defenses.md) 2.8
- 若需合规市场驱动:见 [合规落地映射（03 章 3.7）](03-standards.md)

## 4.7 厂商声明审计与公共政策

> 本节提供**信息可信度审计**与**政策讨论**两个视角。审计表严格复用 [06-来源核验表](06-fact-check.md) 结果,**不新增未经核验的裁决**；政策 Q&A 区分"现行法律事实"与"政策建议"。

### 执行摘要（BLUF）

**如果只记住一件事**：**AI 安全行业的信息生态里,夸大是常态,不是例外**——本报告 79 条声明核验发现 13 条需修正、1 条删除（见 [06-来源核验表](06-fact-check.md)）;其中不乏"把未成功的攻击说成绕过""把未证实数据当事实引用""把模拟实验当真实事件"的典型案例。**读者必须养成三个习惯:查一手来源、区分演示与实战、警惕厂商口径数字。**

**三个关键发现**：
1. **最常见的夸大模式是"演示/尝试"被说成"实战成功"**——Skynet 恶意软件的注入对实测模型**未生效**,却被宣传为"绕过检测";Anthropic misalignment 是**模拟**红队(虚构场景),却常被引用为真实行为。
2. **最危险的是"无来源数字被反复引用"**——Gartner"2024 年 <1%"基线、香港深伪语音案 ~$2500 万细节,都只有二手来源;一经核查要么错误要么无法证实。
3. **政策层面最大的缺口是"无 CVE 的 AI 事件没有强制披露渠道"**——多数 agent 安全事件无 CVE(见 4.1 重要提示,OWASP Q1'26),企业只能依赖社区情报,这直接削弱了市场的风险感知能力。

**行动建议**：引用任何 AI 安全数字前,对照本报告的核验方法论(附录一)。政策讨论请区分"现行法律"与"建议主张"。

---

### 一、厂商声明审计表

> 本表复用 [06-来源核验表](06-fact-check.md) 结果，按"声明→核验→裁决"格式给出每条声明的审计结论。

#### 12 条代表性声明审计

| # | 厂商/来源声明 | 核验结果 | 裁决 |
|---|--------------|---------|------|
| 1 | "Skynet 恶意软件用提示注入绕过 AI 检测" | ✅ 真实样本，但注入对 o3/GPT-4.1 **未生效**（V41） | ⚠️ 夸大——宣传为"绕过"，实为**未成功的尝试** |
| 2 | "香港 2025-03 深伪语音银行诈骗 ~$2500 万" | ⚠️ 仅二手来源，细节无法在一手来源证实（V36） | ⚠️ 不可引用为已证实事实 |
| 3 | "Gartner：2028 年 25% 事件归因 agent 滥用（2024 年 <1%）" | ⚠️ 预测真实（2024-10-22），但"<1%"基线无一手来源（V69） | ⚠️ 基线不可引用；预测与基线分开表述 |
| 4 | "Bedrock Guardrails 拦截最多 88% 有害内容、99% 可解释准确率" | ⚠️ 厂商营销口径，未经独立验证（V62） | ⚠️ 标注"厂商口径" |
| 5 | "Anthropic Auto Mode 拦截 83% 越权、误报 0.4%、93% 审批通过" | ✅ 官方数据，但为厂商自测遥测（V56） | ⚠️ 厂商口径，需独立复现 |
| 6 | "Lakera 被 Cisco 收购" | ❌ 实际为 Check Point（2025-09-16）（V63） | ❌ 错误 |
| 7 | "Greshake 论文《Prompt Injection attack against LLM-integrated Applications》" | ⚠️ 标题实际为 *Not what you've signed up for*（V23） | ⚠️ 标题引用错误 |
| 8 | "CyberSecEval 不安全代码率 26-41%" | ⚠️ 该数字属 CyberSecEval 2 的注入成功率，原版约 30%（V21） | ⚠️ 归因错误 |
| 9 | "ASB 为 Ant Group 基准" | ⚠️ 实为浙江大学+Rutgers（V20） | ⚠️ 归属错误 |
| 10 | "Rebuff 是推荐的注入检测方案" | ⚠️ 仓库已归档不再维护（V68） | ⚠️ 不建议新项目采用 |
| 11 | "Anthropic misalignment：Claude Opus 4 黑mail 率 96%" | ✅ 真实红队实验，但为**模拟**（虚构场景）非真实事件（V52） | ⚠️ 引用必须注明"模拟" |
| 12 | "NVIDIA Chat with RTX 演示命令执行" | ❌ 无法证实，已删除（V51） | ❌ 删除 |

#### 这些案例揭示的三种夸大模式

1. **演示/尝试 → 实战成功**（#1、#11）：研究或未成功尝试被表述为真实危害
2. **二手数字 → 事实**（#2、#3、#8）：无一手来源的数字被反复引用
3. **营销口径 → 能力事实**（#4、#5）：拦截率/准确率未经独立验证

#### 审计方法论（复用纪律）

- **一手来源优先**：CVE 条目、监管公告、arXiv、官方文档
- **三来源规则**：关键声明需 ≥2 独立来源
- **PoC vs 利用**：研究演示 ≠ 在野利用
- **厂商口径标注**：所有拦截率/延迟等为厂商自述

---

### 二、公共政策 Q&A

> 以下每个问题先给**现行法律事实**,再给**政策建议(主张)**——两者分开,读者勿混淆。

#### Q1：消费级 agent(能花钱/发消息)是否应强制披露自主级别?
- **现行事实**：EU Art.50(1) 要求告知"与 AI 交互"；中国标识办法要求 AI 生成内容显式标识（[合规落地映射（03 章 3.7）](03-standards.md)）。但均未要求披露**自主级别/工具权限**。
- **政策建议（主张）**：提议"Agent 透明度标签"——类似营养标签,标注可访问的数据、可执行的动作、是否需人确认。

#### Q2：无 CVE 的 AI 事件是否应强制披露?
- **现行事实**：EU AI Act Art.73 有严重事件上报；中国无 agent 对应机制；美国各州数据泄露法仅覆盖个人数据（见 4.1"多数 AI 事件无 CVE"）。
- **政策建议（主张）**：建议建立类似数据泄露通知的 AI 事件强制披露框架。

#### Q3：深伪欺诈损失由谁承担——受害者、银行还是平台?
- **现行事实**：无统一规则。包头案警方/银行追回 330 余万（V34，证明快速冻结有效）；Arup 案 2 亿港元损失归属不明（V35）。
- **政策建议（主张）**：建议"平台/银行责任 + 快速冻结机制"组合。

#### Q4：招聘 AI（如麦当劳 McHire）是否应强制安全与偏见审计?
- **现行事实**：EU AI Act 将招聘 AI 列为 Annex III 高风险（[合规落地映射（03 章 3.7）](03-standards.md) 4 节）；但无强制第三方安全审计条款。
- **政策建议（主张）**：建议高风险 agent 强制定期安全评估 + 认证（呼应 ISO 42006）。

#### Q5："agent 干的"——责任地板是什么?
- **现行事实**：EU AI Liability Directive + Product Liability Directive (2024/2853) 处理中;中国民法典产品责任条款适用。精确适用待专业法律评估。
- **政策建议（主张）**：责任分配应基于自主级别与人类监督强度。

> ⚠️ 政策 Q&A 中"政策建议"为**主张**,非法律意见；涉法律责任问题需专业法律评估。

---

### 三、社区报道准则（Simon Willison 式）

> 这是给安全媒体/技术 KOL 的写作规范,与本报告 06 核验表的方法论一脉相承。

1. 每条声明标注：PoC / 已证实事件 / 厂商主张
2. 要求一手来源；二手转述注明
3. 公开纠错文化（如本报告 4.7 审计表的核验结论）
4. 避免两极化：既非 FUD 也非"模型更强=可撤护栏"
5. **月度 Agent 安全摘要**格式：发生了什么 / 已验证 / 哪些是炒作 / 链接回核验表

### 下一步

- 若需完整核验明细:见 [06-来源核验表](06-fact-check.md)
- 若需事件背景:见本章 4.1-4.5
- 若需合规事实基础:见 [合规落地映射（03 章 3.7）](03-standards.md)

---

