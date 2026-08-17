---
title: 信息来源核验表
chapter: 6
parent: ai-agent-security-report.md
last_updated: 2026-08-18
status: 完成
prev: 05-conclusions.md
next: 
---

> 本页为《AI Agent 领域安全挑战与应对方法调研》第 6 章。[上一章 05-conclusions.md](05-conclusions.md) · [返回报告概览](00-overview.md)

---

# 六、信息来源核验表（Fact-check Appendix）

> 核验日期：2026-08-06。方法：4 个并行 fact-checking agent + 手动补充核验，均以官方/原始来源为准。✅=证实；⚠️=部分属实；❌=错误。表内 V51（NVIDIA Chat with RTX）为唯一 ❌ 行。

## V-A 标准/框架类

| # | 声明 | 结论 | 来源链接 |
|---|------|------|---------|
| V1 | Prompt Injection 居 OWASP LLM Top 10 两版榜首 | ✅ | https://genai.owasp.org/llm-top-10/ |
| V2 | 2025 版 10 项分类与官方发布一致 | ✅ | https://genai.owasp.org/llm-top-10/ |
| V3 | 2025 版移除 Insecure Plugin Design 与 Model Theft | ✅ | https://genai.owasp.org/llm-top-10-2023-24/ |
| V4 | Agentic Threats & Mitigations v1.0（2025-02-17） | ✅ | https://genai.owasp.org/resource/agentic-ai-threats-and-mitigations/ |
| V5 | Top 10 for Agentic Applications 2026（2025-12-09）+ ASI01–ASI10 | ✅ | https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/ |
| V6 | Securing Agentic Applications Guide 1.0（2025-07-27） | ✅ | https://genai.owasp.org/resource/securing-agentic-applications-guide-1-0/ |
| V7 | Agentic Threats Navigator（2025-03-06，6 攻击面） | ⚠️ URL 以官方发布页为准 | https://genai.owasp.org/resource/owasp-gen-ai-security-project-agentic-threats-navigator/ |
| V8 | MITRE ATLAS 16 tactics / 178 techniques | ✅ | https://atlas.mitre.org/ |
| V9 | ATLAS 技术编号 AML.T0051/T0054/T0020/T0010.005/T0011.002/T0024/T0034 存在 | ✅（快照：ATLAS 2026.07 版数据） | https://atlas.mitre.org/atlas-data/dist/v6/ATLAS-2026.07.yaml |
| V10 | NIST AI RMF 1.0（2023-01-26）/ AI 600-1（2024-07-26） | ✅ | https://www.nist.gov/itl/ai-risk-management-framework |
| V11 | NIST AI 100-2e2023（2024-01-04 定稿，4 类攻击） | ✅ | https://csrc.nist.gov/pubs/ai/100/2/e2023/final |
| V12 | NIST SP 800-218A（2024-07-26） | ✅ | https://csrc.nist.gov/pubs/sp/800/218/a/final |
| V13 | ISO/IEC 42001:2023 可认证 AIMS | ✅ | https://www.iso.org/standard/42001 |
| V14 | ISO 23894/42005/42006/5338 存在 | ✅ | https://www.iso.org/standards（各编号检索） |
| V15 | EU AI Act Reg.2024/1689 + Art.8-17 + 10²⁵ FLOPs | ✅ | https://eur-lex.europa.eu/eli/reg/2024/1689/oj |
| V16 | EU AI Act 时间表（禁例/高风险生效日） | ⚠️ 已按 Digital Omnibus（2026-07-27 生效）更新：禁例 2025-02-02、GPAI 2025-08-02、Annex III **2027-12-02**（原 2026-08-02 推迟）、Annex I **2028-08-02**（原 2027-08-02 推迟） | https://eur-lex.europa.eu/eli/reg/2024/1689/oj（Art.113）+ Commission Digital Omnibus（2026-07） |
| V17 | 中国《暂行办法》令第 15 号 2023-08-15 施行 | ✅ | https://www.cac.gov.cn/2023-07/13/c_1690898327029107.htm |
| V18 | 《标识办法》2025-09-01 生效 | ✅ | https://www.cac.gov.cn/2025-03/14/c_1743654684782215.htm |
| V19 | AgentDojo 97 任务/629 用例 | ✅ | https://arxiv.org/abs/2406.13352 |
| V20 | ASB 84.3% ASR / 归属 | ⚠️ 修正：ZJU+Rutgers（非 Ant Group） | https://arxiv.org/abs/2410.02644 |
| V21 | CyberSecEval 标题与数字 | ⚠️ 修正：正式标题 Purple Llama CyberSecEval；~30% 不安全代码；26–41% 属 CyberSecEval 2 注入成功率 | https://arxiv.org/abs/2312.04724 · https://arxiv.org/abs/2404.13161 |
| V22 | AgentLeak 基准存在 | ✅ | https://arxiv.org/abs/2602.11510 |

## V-B 论文类

| # | 声明 | 结论 | 来源链接 |
|---|------|------|---------|
| V23 | Greshake et al. 间接注入论文（Bing Chat/代码补全演示） | ⚠️ 修正标题为 *Not what you've signed up for* | https://arxiv.org/abs/2302.12173 |
| V24 | MCPTox 45 服务器/353 工具/1312 用例/72.8%/拒绝率<3% | ✅ | https://arxiv.org/abs/2508.14925 |
| V25 | MCP-ITP 隐式投毒 84.2% ASR / 0.3% 检出 | ✅ | https://arxiv.org/abs/2601.07395 |
| V26 | AgentPoison <0.1% 投毒率 / >80% ASR | ✅ | https://arxiv.org/abs/2407.12784 |
| V27 | HouYi 36/31/10/Notion | ✅ | https://arxiv.org/abs/2306.05499 |
| V28 | 200+ Custom GPTs 均可注入 | ✅ | https://arxiv.org/abs/2311.11538 |
| V29 | CAIN/PARASITE 定向劫持 | ✅ | https://arxiv.org/abs/2505.16888 |
| V30 | MCP 纵深防御框架（AWS+Intuit） | ⚠️ 修正：作者为 AWS+Intuit，OWASP 非作者 | https://arxiv.org/abs/2504.08623 |
| V31 | 多智能体 4 论文（2608.00747/2607.19430/2607.25255/2607.19432） | ✅ 全部存在（全新预印本） | https://arxiv.org/abs/2608.00747 · 2607.19430 · 2607.25255 · 2607.19432 |
| V32 | HackMyClaw 挑战（6000 次/$500/Opus 4.6 未泄露） | ✅ 真实事件，但**非 arXiv 论文**（来源为 Willison 博客与官方站点） | https://simonwillison.net/2026/Jun/26/hack-my-ai-assistant/ · https://hackmyclaw.com/ |

## V-C 真实事件类

| # | 事件 | 结论 | 来源链接 |
|---|------|------|---------|
| V33 | Bing Chat/Sydney 间接注入（2023） | ✅ | https://simonwillison.net/2023/Mar/1/indirect-prompt-injection-on-bing-chat/ |
| V34 | 包头 AI 换脸 430 万案 | ✅（被冒充者为熟人，追回 330 余万） | https://gaj.baotou.gov.cn/jffb/article/detail?articleId=857963750869831680 |
| V35 | 香港 Deepfake CFO 2 亿港元案（Arup） | ✅ | https://www.cnn.com/2024/02/04/asia/deepfake-cfo-scam-hong-kong-intl-hnk |
| V36 | 香港 Deepfake 语音银行案（~$2500 万） | ⚠️ 仅二手来源，细节无法证实 | https://dailysecurityreview.com/phishing/deepfake-vishing-incidents-surge-by-170-in-q2-2025/ |
| V37 | DeepSeek 云数据库泄露（Wiz） | ✅ | https://www.wiz.io/blog/wiz-research-uncovers-exposed-deepseek-database-leak |
| V38 | DeepSeek→火山引擎，韩 PIPC 整改 | ✅ | https://www.reuters.com/technology/south-korea-agency-says-deepseek-transferred-user-info-prompts-without-consent-2025-04-24/ |
| V39 | 麦当劳 Olivia/McHire 6400 万记录 | ✅（研究者披露，非确认恶意利用） | https://www.wired.com/story/mcdonalds-ai-hiring-chat-bot-paradoxai/ |
| V40 | M365 Copilot EchoLeak（CVE-2025-32711） | ✅ | https://nvd.nist.gov/vuln/detail/CVE-2025-32711 |
| V41 | Skynet 恶意软件（注入未生效） | ✅ | https://research.checkpoint.com/2025/ai-evasion-prompt-injection/ |
| V42 | 墨西哥政府 150GB 泄露（Claude 辅助） | ✅ | https://www.bloomberg.com/news/articles/2026-02-25/hacker-used-anthropic-s-claude-to-steal-sensitive-mexican-data |
| V43 | OpenClaw 邮箱删除事故 | ✅ | https://techcrunch.com/2026/02/23/a-meta-ai-security-researcher-said-an-openclaw-agent-ran-amok-on-her-inbox/ |
| V44 | Meta 内部 Agent 数据泄露 | ✅ | https://www.theguardian.com/technology/2026/mar/20/meta-ai-agents-instruction-causes-large-sensitive-data-leak-to-employees |
| V45 | Claude Code 源码泄露+恶意仓库 | ✅ | https://www.zscaler.com/blogs/security-research/anthropic-claude-code-leak |
| V46 | Mercor/LiteLLM 供应链事件 | ✅ | https://www.mercor.com/blog/update-on-mercor-security-incident/ · https://www.wired.com/story/meta-pauses-work-with-mercor-after-data-breach-puts-ai-industry-secrets-at-risk/ |
| V47 | Flowise CVE-2025-59528 在野利用 | ✅（CVSS 10.0，1.2万-1.5万实例） | https://www.bleepingcomputer.com/news/security/max-severity-flowise-rce-vulnerability-now-exploited-in-attacks/ |
| V48 | GrafanaGhost（CVE-2026-27876） | ✅ | https://noma.security/blog/grafana-ghost/ |
| V49 | Meta AI 机器人账号接管 | ✅ | https://simonwillison.net/2026/Jun/1/hackers-simply-asked-meta-ai/ |
| V50 | Word/Copilot 自复制蠕虫（Håkon Måløy） | ✅ | https://simonwillison.net/2026/Jul/29/ai-worming-through-word/ |
| V51 | NVIDIA Chat with RTX 演示 | ❌ 无法证实，已删除 | —（替代：ChatRTX CVE-2024-2624/2625 https://www.securityweek.com/code-execution-flaws-haunt-nvidia-chatrtx-for-windows/） |
| V52 | Anthropic agentic misalignment（16 模型，Opus 4/Gemini 2.5 Flash 96%） | ✅（模拟红队，非真实事件） | https://www.anthropic.com/research/agentic-misalignment |
| V53 | OWASP GenAI Q1'26 Round-up 报告存在且支持"多无 CVE"论断 | ✅ | https://genai.owasp.org/2026/04/14/owasp-genai-exploit-round-up-report-q1-2026/ |

## V-D 厂商/产品类

| # | 声明 | 结论 | 来源链接 |
|---|------|------|---------|
| V54 | Anthropic *How we contain Claude*（三层/沙箱84%/VM token/挂载档位） | ✅（厂商遥测口径） | https://www.anthropic.com/engineering/how-we-contain-claude |
| V55 | sandbox-runtime 开源仓库 | ✅ | https://github.com/anthropic-experimental/sandbox-runtime |
| V56 | Claude Code auto mode（83%拦截/0.4%误拦/93%审批通过） | ✅（厂商口径） | https://www.anthropic.com/engineering/claude-code-auto-mode |
| V57 | Claude for Chrome 三层注入防御（RL+classifier+红队） | ✅（厂商口径，1% ASR 为自测） | https://www.anthropic.com/research/prompt-injection-defenses |
| V58 | MCP Security Best Practices 教程 | ⚠️ URL 为版本化路径 | https://modelcontextprotocol.io/docs/2026-07-28/tutorials/security/security_best_practices |
| V59 | OWASP MCP Security Cheat Sheet | ✅ | https://cheatsheetseries.owasp.org/cheatsheets/MCP_Security_Cheat_Sheet.html |
| V60 | OWASP AI Agent Security Cheat Sheet | ✅ | https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html |
| V61 | OpenAI Guardrails 产品+cookbook+python | ✅ | https://guardrails.openai.com/ · https://developers.openai.com/cookbook/topic/guardrails |
| V62 | Bedrock Guardrails（策略数/88%/99%） | ⚠️ 官方文档为 6 类策略；88%/99% 为厂商营销口径 | https://docs.aws.amazon.com/bedrock/latest/userguide/guardrails.html |
| V63 | Lakera 被收购 | ⚠️ 修正：**Check Point**（2025-09-16），非 Cisco | https://www.lakera.ai/ · https://www.checkpoint.com/（收购新闻稿） |
| V64 | Prompt Security → SentinelOne | ✅ | https://www.sentinelone.com/press/sentinelone-to-acquire-prompt-security-to-advance-genai-security/ |
| V65 | Invariant Labs → Snyk | ✅ | https://snyk.io/news/snyk-acquires-invariant-labs-to-accelerate-agentic-ai-security-innovation/ |
| V66 | NeMo Guardrails 仓库（已迁移） | ✅ | https://github.com/NVIDIA-NeMo/Guardrails |
| V67 | Guardrails AI 仓库 | ✅ | https://github.com/guardrails-ai/guardrails |
| V68 | Rebuff 仓库 | ⚠️ 已归档，不再维护 | https://github.com/protectai/rebuff |
| V69 | Gartner "25% 事件归因 Agent 滥用" | ⚠️ 修正：预测出自 2024-10-22，非 2025-10-07；"<1%"基线无一手来源 | https://www.gartner.com/en/newsroom/press-releases/2024-10-22-gartner-unveils-top-predictions-for-it-organizations-and-users-in-2025-and-beyond |
| V70 | Gartner ">40% Agentic AI 项目取消" | ✅ | https://www.gartner.com/en/newsroom/press-releases/2025-06-25-gartner-predicts-over-40-percent-of-agentic-ai-projects-will-be-canceled-by-end-of-2027 |
| V71 | Willison prompt-injection 档案 + Lethal Trifecta | ✅ | https://simonwillison.net/tags/prompt-injection/ · https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/ |
| V72 | OpenAI Lockdown Mode | ✅ | https://openai.com/index/introducing-lockdown-mode-and-elevated-risk-labels-in-chatgpt/ |
| V73 | Microsoft Azure AI 安全 + Entra AI Gateway + Agent Governance Toolkit | ✅ | https://learn.microsoft.com/en-us/azure/security/fundamentals/ai-security-best-practices · https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-ai-prompt-injection-protection · https://github.com/microsoft/agent-governance-toolkit |
| V74 | Google SAIF | ✅ | https://www.saif.google/secure-ai-framework |
| V75 | 中国电信《AI 智能体安全治理白皮书》 | ✅ | https://www.chinatelecom.com.cn/ct/news/jtxw/161236.html |
| V76 | 奇安信 MCP 威胁情报 | ⚠️ 属实但性质不同：是奇安信自有的 MCP 威胁情报服务，非"MCP 漏洞的威胁情报覆盖" | https://www.qianxin.com/news/detail?news_id=13436 |
| V77 | CVE-2025-6514（mcp-remote RCE，CVSS 9.6） | ✅ | https://jfrog.com/blog/2025-6514-critical-mcp-remote-rce-vulnerability/ |
| V78 | OX Security MCP 架构缺陷（1.5 亿+下载/20 万台服务器） | ✅（披露范围以 OX 报告原文为准） | https://www.ox.security/reports/the-mother-of-all-ai-supply-chains-anthropics-by-design-failure-at-the-heart-of-the-ai-ecosystem/ |
| V79 | Claude web_fetch 外泄（Ayush Paul） | ✅ | https://securityv0.com/intelligence/2026-07-19-claude-web-fetch-memory-heist/ |

## 核验统计

- 79 条声明中：**✅ 完全证实 65 条**；**⚠️ 部分属实 13 条**；**❌ 错误/无法证实 1 条**（NVIDIA Chat with RTX 演示）。统计按表中实际行数计（65/13/1）。
- 核验要点：Greshake 论文正确标题、CyberSecEval 数字归因、ASB 作者归属（ZJU+Rutgers）、EU AI Act 生效时间表（含 Digital Omnibus 更新）、Lakera 收购方（Check Point）、Gartner 预测来源日期、Bedrock Guardrails 策略数（6）、Rebuff 归档状态、NeMo 仓库迁移、Anthropic misalignment 定性（模拟实验）、多起事件细节（包头案被冒充者为熟人、麦当劳案为研究者披露、Skynet 注入未生效等）。

---
