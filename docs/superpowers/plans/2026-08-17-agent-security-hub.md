# Agent Security Hub Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 在 `~/Projects/agent-security-hub/` 搭建纯 Markdown 的 Agent 安全知识库（六库结构 + 双评估模型 + 30 分钟分享文档），将现有研究报告拆解为种子内容。

**Architecture:** 纯 Markdown 文档项目，零依赖、无构建。按对象类型分为 reports/incidents/vulnerabilities/vendors/papers/tools 六库，每库带 `_template.md` 新增模板；评估模型独立于 `docs/evaluation/`；分享文档在 `docs/presentation-30min.md`。内容延续事实核验纪律（来源可溯、区分事实/估算/建议）。

**Tech Stack:** Markdown。源数据来自 `~/Projects/research/topics/ai-agent-security/`（8 章研究报告）。

**源文件映射（种子内容来源）：**
- 报告 01-08 章 → `library/reports/ai-agent-security-report.md`
- 报告 04 章 4.1/4.2 → `library/incidents/`
- 报告 01 章 1.3/1.4 CVE + 02 章 2.9 IOC → `library/vulnerabilities/`
- 报告 04 章 4.3/4.6 → `library/vendors/`
- 报告 04 章 4.2 + 03 章 3.5 → `library/papers/`
- 报告 02 章 2.8/2.9/2.10 → `library/tools/`

---

### Task 1: 项目骨架（README + CLAUDE.md + 目录结构）

**Files:**
- Create: `~/Projects/agent-security-hub/README.md`
- Create: `~/Projects/agent-security-hub/CLAUDE.md`
- Create: 目录 `docs/evaluation/`、`library/{reports,incidents,vulnerabilities,vendors,papers,tools}/`

- [ ] **Step 1: 创建目录结构**

```bash
mkdir -p ~/Projects/agent-security-hub/docs/evaluation ~/Projects/agent-security-hub/docs/superpowers/plans ~/Projects/agent-security-hub/library/{reports,incidents,vulnerabilities,vendors,papers,tools}
```

- [ ] **Step 2: 写 README.md**

```markdown
# Agent Security Hub

Agent 安全知识库与分享项目。收录 Agent 安全的事件、漏洞、厂商、论文、工具与深度报告，并提供风险评分与成熟度评估模型。

## 导航

- **知识库** `library/`：按对象类型分类（见下方）
- **评估模型** `docs/evaluation/`：风险打分 + 成熟度模型
- **分享文档** `docs/presentation-30min.md`：30 分钟演讲材料

## 知识库结构

| 库 | 内容 | 说明 |
|----|------|------|
| `reports/` | 深度报告 | 完整研究报告（种子内容） |
| `incidents/` | 事件库 | 已证实安全事件 + 新增模板 |
| `vulnerabilities/` | 漏洞库 | CVE 与漏洞条目 + 新增模板 |
| `vendors/` | 厂商库 | 厂商生态/并购/融资/定位 + 新增模板 |
| `papers/` | 论文库 | 研究论文与基准 + 新增模板 |
| `tools/` | 工具库 | 检测/防护/红队工具 + 新增模板 |

## 原则

- 纯 Markdown，零依赖
- 数据延续事实核验纪律：来源可溯、区分事实/估算/建议、标注检索日期
- 新增信息按各库 `_template.md` 模板填入
```

- [ ] **Step 3: 写 CLAUDE.md**（仿 agent-design 风格，说明项目结构与维护约定）

```markdown
# CLAUDE.md

## 项目概述

纯 Markdown 文档知识库，收集 Agent 安全信息并做分享。无构建、无测试、无代码。

## 仓库结构

```
agent-security-hub/
├── README.md                # 入口 + 导航
├── CLAUDE.md                # 本文件
├── docs/
│   ├── presentation-30min.md # 30分钟分享文档
│   └── evaluation/           # 评估模型（risk-score / maturity-model）
└── library/
    ├── README.md             # 各库导航
    ├── reports/              # 深度报告
    ├── incidents/            # 事件库（+_template.md）
    ├── vulnerabilities/      # 漏洞库（+_template.md）
    ├── vendors/              # 厂商库（+_template.md）
    ├── papers/               # 论文库（+_template.md）
    └── tools/                # 工具库（+_template.md）
```

## 维护约定

- 新增事件/漏洞/厂商/论文/工具：复制对应 `_template.md` 填写，文件名用 kebab-case
- 数据要求：来源 URL、检索日期、区分事实/估算/建议
- 评估模型引用知识库数据时保持链接有效
```

- [ ] **Step 4: 写 library/README.md（各库导航）**

```markdown
# 知识库

按对象类型分类。每库首个文件为导航说明 + 内容清单，并附 `_template.md` 供新增收录。

| 库 | 收录内容 | 种子条目数 |
|----|---------|-----------|
| [reports](reports/) | 深度研究报告 | 1 |
| [incidents](incidents/) | 已证实安全事件 | 18 |
| [vulnerabilities](vulnerabilities/) | CVE 与漏洞 | 5+ |
| [vendors](vendors/) | 厂商生态 | 16+ |
| [papers](papers/) | 论文与基准 | 10+ |
| [tools](tools/) | 检测/防护工具 | 15+ |

> 内容延续事实核验纪律。种子数据来自《AI Agent 领域安全挑战与应对方法调研》（见 reports/）。
```

- [ ] **Step 5: 验证骨架**

```bash
find ~/Projects/agent-security-hub -type d | sort
```
Expected: 目录结构符合 Task 1 Step 1。

---

### Task 2: reports 库 — 研究报告入库

**Files:**
- Create: `library/reports/ai-agent-security-report.md`

- [ ] **Step 1: 生成合并报告**

将源报告 8 章 + 概览合并为单一文档。用脚本拼接（保留章节标题层级，去掉各章"所属报告/上一章/下一章"页脚与重复 boilerplate）：

```bash
cd ~/Projects/research/topics/ai-agent-security
python3 - <<'EOF'
import re
from pathlib import Path
out = Path("/Users/zhangbolin/Projects/agent-security-hub/library/reports/ai-agent-security-report.md")

header = """# AI Agent 领域安全挑战与应对方法调研

> 来源：research 项目（2026-08 核验版）· 检索日期 2026-08-06
>
> 本报告系统调研 AI Agent 安全挑战与应对。关键声明经逐条来源核验（79 条：65 证实 / 13 部分属实 / 1 删除），核验明细见文末核验表。

## 目录

1. [一、攻击面与威胁分类](#一攻击面与威胁分类security-threats)
2. [二、防御方法与最佳实践](#二防御方法与最佳实践defense--mitigations)
3. [三、安全标准、框架与合规](#三安全标准框架与合规standards--frameworks)
4. [四、真实事件案例与生态格局](#四真实事件案例与生态格局incidents--ecosystem)
5. [五、结论与行动建议](#五结论与行动建议)
6. [六、信息来源核验表](#六信息来源核验表fact-check-appendix)

---
"""

files = ["01-威胁分类与攻击面.md","02-防御方法与最佳实践.md","03-标准框架与合规.md",
         "04-真实事件与生态格局.md","05-结论与行动建议.md","06-来源核验表.md"]

parts = [header]
for f in files:
    text = Path(f).read_text()
    lines = text.split("\n")
    # 去掉文件头所属报告/检索日期 blockquote 与页脚
    body = []
    skip_quote = False
    for i, line in enumerate(lines):
        if i == 0:  # 跳过 H1 标题
            continue
        if line.startswith("> 所属报告") or line.startswith("> 检索日期") or line.startswith("> 本文档") or line.startswith("> 关键声明") or line.startswith("> 所有声明"):
            continue
        if line.startswith("---") and i > len(lines) - 6:
            break
        if line.startswith("上一章") or line.startswith("[返回总览]"):
            continue
        body.append(line)
    parts.append("\n".join(body))

out.write_text("\n".join(parts).rstrip() + "\n")
print("written", out)
EOF
```

- [ ] **Step 2: 校验合并报告无缺失**

```bash
wc -l ~/Projects/agent-security-hub/library/reports/ai-agent-security-report.md
grep -c "核验表\|攻击向量\|风险登记表\|安全基准" ~/Projects/agent-security-hub/library/reports/ai-agent-security-report.md
```
Expected: 行数 >1500，关键章节关键词均出现。

---

### Task 3: incidents + vulnerabilities 库

**Files:**
- Create: `library/incidents/README.md`
- Create: `library/incidents/_template.md`
- Create: `library/incidents/已证实事件清单.md`
- Create: `library/vulnerabilities/README.md`
- Create: `library/vulnerabilities/_template.md`
- Create: `library/vulnerabilities/CVE清单.md`

- [ ] **Step 1: incidents/README.md + 已证实事件清单.md**

从报告 04 章 4.1 提取 18 起已证实事件。每起含：时间/事件/类型/影响/来源。清单为表格 + 每起事件的简短条目。

```markdown
# 事件库

已证实的 Agent 安全事件。种子数据来自研究报告 4.1（18 起已证实）。

## 已证实事件清单

| 时间 | 事件 | 类型 | 影响 |
|------|------|------|------|
| 2023.02–03 | Bing Chat/Sydney 间接提示注入 | 间接注入 | PoC |
| 2023.05 | 包头 AI 换脸视频诈骗案 | Deepfake 欺诈 | 约 430 万元 |
| 2024.01 | 香港 Deepfake CFO 诈骗（Arup） | Deepfake 欺诈 | 2 亿港元 |
| 2025.01–03 | DeepSeek 云数据库泄露 | 云配置错误 | 100 万+ 日志行 |
| 2025.03 | 香港 Deepfake 语音银行诈骗（细节待证实） | Deepfake 语音 | ~$2500 万（二手） |
| 2025.04 | DeepSeek 未经同意传输韩国用户数据 | 数据跨境 | 监管处罚 |
| 2025.06 | 麦当劳 McHire 弱口令 | 弱认证 | 6400 万记录（研究者披露） |
| 2025.06 | M365 Copilot EchoLeak（CVE-2025-32711） | 注入+外泄 | CVSS 9.3 |
| 2025.06 | Skynet 注入型恶意软件 | 对抗检测 | 注入未生效 |
| 2025.12–2026.02 | 墨西哥政府数据泄露（Claude 辅助） | AI 辅助攻击 | 150GB |
| 2026.02 | OpenClaw 邮箱删除事故 | 自主代理失控 | 真实事故 |
| 2026.03 | Meta 内部 Agent 数据泄露 | Agent 错误建议 | 约 2 小时暴露 |
| 2026.03–04 | Claude Code 源码泄露+恶意仓库 | 供应链 | 51.3 万行 |
| 2026.03–04 | Mercor/LiteLLM 供应链事件 | 供应链 | 波及多家实验室 |
| 2026.04 | Flowise CVE-2025-59528 在野利用 | RCE | 1.2-1.5 万实例 |
| 2026.04 | GrafanaGhost（CVE-2026-27876） | 注入+外泄 | 已修复 |
| 2026.06 | Meta AI 账号接管 | AI 客服社工 | 真实接管 |
| 2026.07 | Word/Copilot 自复制蠕虫 | 自复制注入 | 研究披露 |

> 来源：研究报告 4.1，核验明细见 reports/ 报告第六章。
```

- [ ] **Step 2: incidents/_template.md**

```markdown
# 事件新增模板

> 复制本文件为 `YYYY-MM-事件名.md` 填写。

## 事件概述
- **时间**：
- **类型**：间接注入 / Deepfake / 供应链 / RCE / 数据外泄 / 自主代理失控 / 其他
- **影响对象**：
- **影响**：
- **状态**：已证实 / 部分证实 / 研究披露

## 经过
（叙述攻击链/事件过程）

## 影响与损失
（数据量、金额、监管后果）

## 来源
- 一手来源 URL：
- 核验状态：✅ 证实 / ⚠️ 部分 / ❌ 未证实
```

- [ ] **Step 3: vulnerabilities/README.md + CVE清单.md + _template.md**

从报告 01 章 1.3/1.4 + 02 章 2.9 提取 CVE。清单表格 + 每 CVE 条目。模板含：CVE 号/组件/类型/CVSS/受影响版本/影响/来源。

```markdown
# 漏洞库

Agent 相关漏洞（CVE 为主）。

## CVE 清单

| CVE | 组件 | 类型 | CVSS | 说明 |
|-----|------|------|------|------|
| CVE-2025-6514 | mcp-remote | RCE（OAuth 注入） | 9.6 | 连接不可信 MCP 服务器触发任意命令执行 |
| CVE-2025-32711 | M365 Copilot | 注入+数据外泄 | 9.3 | EchoLeak 零点击注入 |
| CVE-2025-59528 | Flowise | RCE（CustomMCP JS） | 10.0 | 在野利用，1.2-1.5 万实例 |
| CVE-2026-27876 | Grafana | 注入+外泄 | — | GrafanaGhost 图片渲染外泄 |
| CVE-2025-53773 | GitHub Copilot | RCE（注入 PR 描述） | 9.6 | — |
| CVE-2025-59536 | Claude Code | RCE（注入→代码执行） | 8.7 | — |

> 来源：研究报告 01 章 1.3/1.4、02 章 2.9；核验见核验表 V77 等。
```

- [ ] **Step 4: vulnerabilities/_template.md**

```markdown
# 漏洞新增模板

> 复制为 `CVE-YYYY-XXXXX.md` 填写。

## 漏洞信息
- **CVE 编号**：
- **组件**：
- **类型**：RCE / 注入 / SSRF / 供应链 / 其他
- **CVSS 评分**：
- **受影响版本**：
- **修复版本**：

## 漏洞机理
（攻击链描述）

## 影响
（是否在野利用、受影响实例数）

## 来源
- NVD / 官方公告 URL：
- 核验状态：
```

- [ ] **Step 5: 校验模板与清单一致**

```bash
grep -c "CVE-" ~/Projects/agent-security-hub/library/vulnerabilities/CVE清单.md
ls ~/Projects/agent-security-hub/library/{incidents,vulnerabilities}
```
Expected: CVE 清单含 6 条；两库含 README + _template + 清单。

---

### Task 4: vendors + papers + tools 库

**Files:**
- Create: `library/vendors/README.md`、`library/vendors/_template.md`、`library/vendors/厂商生态清单.md`
- Create: `library/papers/README.md`、`library/papers/_template.md`、`library/papers/论文与基准清单.md`
- Create: `library/tools/README.md`、`library/tools/_template.md`、`library/tools/工具清单.md`

- [ ] **Step 1: vendors 库**（从报告 4.3/4.6 提取）

厂商清单含：名称/品类/买家/并购状态/来源。模板字段：名称/品类/定位/并购/融资/来源。

```markdown
# 厂商库

Agent 安全厂商生态。种子数据来自研究报告 4.3/4.6。

## 厂商清单

| 厂商 | 品类 | 并购状态 | 备注 |
|------|------|---------|------|
| Lakera | LLM 防火墙 | → Check Point（2025-09） | 实时注入防御 |
| Prompt Security | GenAI 安全平台 | → SentinelOne（2025-08） | $250M/300M 媒体价 |
| Invariant Labs | Agentic 安全 | → Snyk（2025-06） | MCP 扫描 |
| Robust Intelligence | 模型验证 | → Cisco（2024-08） | — |
| Protect AI | AI-SPM | → Palo Alto（2025-04） | — |
| Aim Security | GenAI/agentic 安全 | → Cato（2025-09） | — |
| Securiti AI | 数据安全+AI 治理 | → Veeam（2025-10） | $1.7B |
| TrojAI | 模型风险 | → A10（2026-06） | — |
| Noma Security | AI 应用安全 | 未收购 | — |
| Lasso Security | GenAI 数据保护 | 未收购 | — |
| HiddenLayer | AI 安全/模型保护 | 未收购 | — |
| Wiz | CSPM+AI-SPM | 平台 | — |
| Zscaler | SASE+AI 保护 | 平台 | — |
| Wiz Research / Zscaler ThreatLabz 等 | 事件驱动 | — | — |

> 来源：研究报告 4.3/4.6；M&A 价格为媒体价，官方多未披露。
```

- [ ] **Step 2: vendors/_template.md**

```markdown
# 厂商新增模板

> 复制为 `厂商名.md` 填写。

## 厂商信息
- **名称**：
- **品类**：LLM 防火墙 / AI-SPM / Agentic 安全 / 模型验证 / 其他
- **定位**：
- **宣称买家**：

## 商业动态
- **融资**（金额/轮次/日期）：
- **并购**（收购方/日期/价格）：
- **来源**：

## 能力评估
（覆盖哪些风险向量、与哪些基准相关的客观信息）
```

- [ ] **Step 3: papers 库**（从报告 4.2/3.5 提取）

论文清单含：标题/要点/来源(arXiv)/核验。模板：标题/作者/要点/基准数据/来源。

```markdown
# 论文库

Agent 安全研究论文与基准。种子数据来自研究报告 4.2/3.5。

## 论文清单

| 论文 | 要点 | 来源 |
|------|------|------|
| Greshake et al. IPI | 首次系统化间接注入 | arXiv:2302.12173 |
| AgentPoison | <0.1% 投毒率 >80% ASR | arXiv:2407.12784 |
| AgentDojo | 97 任务/629 用例 | arXiv:2406.13352 |
| HouYi | 36 应用 31 可注入 | arXiv:2306.05499 |
| CyberSecEval | 模型不安全代码 ~30% | arXiv:2312.04724 |
| MCPTox | MCP 工具投毒基准 | arXiv:2508.14925 |
| ASB | 最高 ASR 84.3% | arXiv:2410.02644 |
| AgentLeak | 多 Agent 隐私泄露基准 | arXiv:2602.11510 |
| CAIN/PARASITE | 定向提示劫持 | arXiv:2505.16888 |
| MCP 纵深防御框架 | AWS+Intuit | arXiv:2504.08623 |

> 来源：研究报告 4.2/3.5；核验见 reports/ 核验表。
```

- [ ] **Step 4: papers/_template.md**

```markdown
# 论文新增模板

> 复制为 `论文简称.md` 填写。

## 论文信息
- **标题**：
- **作者/机构**：
- **来源**（arXiv/会议/URL）：
- **日期**：

## 要点
（研究问题、方法、结论）

## 关键数据
（ASR/投毒率/用例数等，标注与原文核对状态）

## 与知识库关联
（对应风险向量/防御/事件）
```

- [ ] **Step 5: tools 库**（从报告 2.8/2.9/2.10 提取）

工具清单：名称/类别/开源/状态/用途。模板：名称/类别/开源自托管/维护状态/用途/来源。

```markdown
# 工具库

Agent 安全工具：检测、防护、红队。种子数据来自研究报告 2.8/2.9/2.10。

## 工具清单

| 工具 | 类别 | 开源 | 状态 |
|------|------|------|------|
| 检测与响应资产包（Sigma 规则×10） | 检测 | 是（库内） | 02 章 2.9 |
| MCP 安全实操包（硬化清单/JSON/代码） | 防护 | 是（库内） | 02 章 2.10 |
| NVIDIA NeMo Guardrails | 护栏 | 是 | github.com/NVIDIA-NeMo/Guardrails |
| Guardrails AI | 护栏 | 是 | guardrails-ai/guardrails |
| Meta LlamaGuard / Prompt Guard | 护栏 | 是 | — |
| Anthropic Sandbox Runtime | 隔离 | 是 | anthropic-experimental/sandbox-runtime |
| Microsoft Agent Governance Toolkit | 治理 | 是 | microsoft/agent-governance-toolkit |
| Rebuff | 注入检测 | 是（已归档） | protectai/rebuff |
| garak / PyRIT / Promptfoo | 红队 | 是 | — |

> 来源：研究报告 2.8-2.10。
```

- [ ] **Step 6: tools/_template.md**

```markdown
# 工具新增模板

> 复制为 `工具名.md` 填写。

## 工具信息
- **名称**：
- **类别**：检测 / 防护 / 护栏 / 红队 / 治理
- **开源/自托管**：
- **维护状态**（最后更新/是否归档）：
- **用途**：

## 使用
（部署要点、适用场景）

## 来源
- 仓库/官网 URL：
- 检索日期：
```

- [ ] **Step 7: 校验三库**

```bash
ls ~/Projects/agent-security-hub/library/{vendors,papers,tools}
grep -c "|" ~/Projects/agent-security-hub/library/vendors/厂商生态清单.md
```
Expected: 三库各含 README + _template + 清单；厂商清单含 >12 行表格。

---

### Task 5: 风险打分模型

**Files:**
- Create: `docs/evaluation/risk-score.md`

- [ ] **Step 1: 写风险打分模型文档**

基于报告 1.7 的 L×I 矩阵，扩展为可复用评估框架。含：使用指引、17 向量清单（带 L/I 参考值）、5×5 矩阵表、使用步骤、示例、数据来源。

```markdown
# 风险评估打分模型

> 用于评估**候选 Agent 系统/方案的部署风险**。基于《AI Agent 领域安全挑战与应对方法调研》1.7 风险登记表扩展。

## 使用指引

- **评估者**：安全工程师 / 架构师 / 采购评估人员
- **评估对象**：候选 Agent 系统（工具调用、自主执行能力）或组织现有 Agent 部署
- **评估产出**：风险值（1-25）与处置建议

## 评分维度

- **L（可能性 1-5）**：约年发生概率。L1 <1% / L2 1-10% / L3 10-30% / L4 30-70% / L5 >70%
- **I（影响 1-5）**：财务+数据损失锚点。I1 <$0.1M / I2 $0.1-0.5M / I3 $0.5-1M / I4 $1-5M / I5 >$5M
- **风险值 = L × I**（1-25）：1-6 低 / 8-12 中 / 15-20 高 / 20-25 极危

## 17 向量参考表

| # | 向量 | L | I | 参考风险 | 等级 |
|---|------|---|---|---------|------|
| 1 | 直接提示注入 | 5 | 5 | 25 | 极危 |
| 2 | 间接提示注入 | 5 | 5 | 25 | 极危 |
| 3 | 越狱 | 4 | 4 | 16 | 高 |
| 4 | 工具滥用/投毒 | 3 | 4 | 12 | 中 |
| 5 | 恶意 MCP 服务器 | 3 | 4 | 12 | 中 |
| 6 | RCE | 3 | 5 | 15 | 高 |
| 7 | 数据外泄 | 5 | 5 | 25 | 极危 |
| 8 | 凭证盗窃 | 4 | 4 | 16 | 高 |
| 9 | 模型窃取 | 3 | 4 | 12 | 中 |
| 10 | DoS/无界消耗 | 3 | 3 | 9 | 中 |
| 11 | 智能体间攻击 | 1* | 4 | 4* | 低* |
| 12 | 恶意/错位智能体 | 4 | 5 | 20 | 极危 |
| 13 | 供应链攻击 | 4 | 4 | 16 | 高 |
| 14 | RAG/向量投毒 | 4 | 4 | 16 | 高 |
| 15 | 系统提示泄露 | 4 | 3 | 12 | 中 |
| 16 | 过度授权/自治 | 5 | 5 | 25 | 极危 |
| 17 | Vishing/深伪 | 4 | 5 | 20 | 极危 |

> *智能体间攻击频率数据稀缺，L1 为保守占位。L×I 为判断性评估，组织应重估 I。

## 使用步骤

1. **识别适用向量**：针对待评估 Agent 的功能（工具集、权限、数据访问）圈定相关向量
2. **定 L**：结合环境（是否接触不可信内容、有无沙箱）修正参考 L
3. **定 I**：按组织的资产清单（数据敏感度、可达系统）重估 I
4. **查矩阵**：L×I 得风险值，查处置建议
5. **汇总**：输出 Top 风险与优先级

## 5×5 风险矩阵

| | I1 | I2 | I3 | I4 | I5 |
|---|---|---|---|---|---|
| **L5** | 5 | 10 | 15 | 20 | 25 |
| **L4** | 4 | 8 | 12 | 16 | 20 |
| **L3** | 3 | 6 | 9 | 12 | 15 |
| **L2** | 2 | 4 | 6 | 8 | 10 |
| **L1** | 1 | 2 | 3 | 4 | 5 |

## 处置建议

- 极危（20-25）：不部署门禁 / 立即修复
- 高（15-16）：优先缓解（最小权限、输出过滤、监控）
- 中（8-12）：接受或监控，定期复查
- 低（1-6）：接受（注意数据缺失项需重估）

## 示例：评估"可读邮箱 + 可发邮件的客服 Agent"

1. 适用向量：#1 直接注入、#2 间接注入、#7 数据外泄、#8 凭证、#16 过度授权
2. L：#1/#2 = 5（接触用户邮件=不可信内容），#16 = 5（权限含发信）
3. I：#7 = 4（PII 量级中等），#16 = 5（可放大）
4. 结果：注入 25、外泄 20、过度授权 25 → 判定极危，需最小权限 + hard-confirm + egress 阻断

## 数据来源与局限

- 校准基线：IBM Cost of a Data Breach 2026（$4.99M 全球平均 / 提示注入 $5.89M）
- 局限：L×I 为判断性评估非测量；"无公开数据"向量（如 A2A 频率）取值保守
- 完整数据来源见 reports/ 报告 1.7 与核验表
```

---

### Task 6: 安全成熟度模型

**Files:**
- Create: `docs/evaluation/maturity-model.md`

- [ ] **Step 1: 写成熟度模型文档**

CMMI 风格 0-5 级 × 5 维度（治理/架构/护栏/监控/供应链）。每级含行为描述 + 证据要求 + 使用指引。

```markdown
# Agent 安全成熟度模型

> 评估**组织**的 Agent 安全能力阶段（非单个系统）。CMMI 风格 0-5 级 × 5 维度。

## 使用指引

- **评估者**：安全负责人 / 合规 / 架构
- **评估对象**：组织整体（Agent 部署、流程、治理）
- **产出**：每维度等级 + 总体等级（取最低维度为瓶颈）

## 五个维度

1. **治理**：策略、责任、审批流程、风险登记
2. **架构**：最小权限、沙箱/隔离、身份管理
3. **护栏**：注入防御、输出过滤、HITL
4. **监控**：检测规则、日志审计、响应流程
5. **供应链**：MCP/依赖治理、SBOM、来源验证

## 等级定义（每维度）

| 级 | 名称 | 行为描述 | 证据要求 |
|----|------|---------|---------|
| 0 | 缺失 | 无 Agent 安全实践，Agent 随意接入 | 无 |
| 1 | 初始 | 有零散意识，无标准；个别项目自发起 | 零散文档/口头约定 |
| 2 | 已管理 | 有基础策略与权限控制；Agent 需审批接入 | 策略文档、审批记录 |
| 3 | 已定义 | 纵深防御制度化；护栏/监控/供应链有标准流程 | 制度文件、检测规则、审计日志 |
| 4 | 量化 | 有安全指标（注入 ASR、审批率、覆盖度）并度量 | 指标看板、趋势报告 |
| 5 | 优化 | 持续改进，红队/基准评测常态化 | 红队报告、改进记录 |

## 评估流程

1. 逐维度定位当前等级（对照行为描述）
2. 收集证据（政策文件、日志、规则、指标）
3. 定位差距：目标等级 vs 当前等级
4. 制定路线图：按维度逐级推进（瓶颈维度优先）

## 示例：某团队评估

| 维度 | 当前级 | 目标级 | 差距行动 |
|------|--------|--------|---------|
| 治理 | 2 | 3 | 制定 Agent 接入审批制度与风险登记表 |
| 架构 | 2 | 3 | 为高权限 Agent 引入沙箱与最小权限 |
| 护栏 | 1 | 3 | 部署注入检测 + 输出过滤 + HITL |
| 监控 | 1 | 3 | 落地 Sigma 规则与审计日志 |
| 供应链 | 1 | 2 | 建立 MCP/依赖白名单与来源验证 |

总体等级 = 最低维度 = 1 → 优先提升护栏/监控/供应链。

## 与风险模型的配合

- 成熟度模型评估**组织能力**；风险模型评估**单个系统风险**
- 建议：先做成熟度定位（找差距），再用风险模型对高危 Agent 打分（排优先级）
- 工具资产见 `library/tools/`，评估数据参考 `library/incidents|vulnerabilities/`
```

---

### Task 7: 30 分钟分享会文档

**Files:**
- Create: `docs/presentation-30min.md`

- [ ] **Step 1: 写分享文档**

混合受众（技术+管理），6 节分时结构 + 讲者备注。

```markdown
# Agent 安全 30 分钟分享

> 受众：技术团队 + 管理层混合。总时长约 30 分钟，含讲者备注（以 "🎤" 开头）。

## 0. 开场（2 min）

**一句话**：AI Agent 正在进入企业，但它引入的安全风险比传统软件更特殊——**攻击者不需要攻破代码，只要操纵 Agent 的"大脑"**。

🎤 讲者：开场不深入技术，先建立"这跟普通安全不同"的认知。可用趋势数据：Gartner 预测 2028 年 25% 企业安全事件将归因 Agent 滥用。

## 1. 风险全景（6 min）

- Agent 的三类核心风险：
  1. **被操纵**（提示注入）：网页/邮件/文档里的隐藏指令可让 Agent 执行未授权动作
  2. **权限过大**（过度授权）：Agent 拥有超出任务的工具与权限
  3. **泄密通道**（数据外泄）：三者齐备 = 数据泄露几乎必然（"致命三角"）
- 一句话类比：Agent 像一个"很能干但容易轻信的实习生"

🎤 讲者：用"致命三角"比喻（私密数据+不可信内容+外泄通道），管理层能立刻理解为什么这不仅是技术问题。

## 2. 真实案例（6 min）

选 3-4 起（对应知识库 incidents/）：
- 香港 Deepfake CFO：视频会议全 AI 换脸，转出 2 亿港元
- OpenClaw：Agent 无视"停止"批量删邮件
- Flowise：Agent 平台 RCE，1.2-1.5 万实例在野利用
- Meta AI 客服：被要求"改绑定邮箱"即账号接管

🎤 讲者：每起 1-2 分钟，强调"影响+为什么发生"。金额数据点对管理层有冲击力。

## 3. 防御框架（6 min）

- 纵深防御四层：权限最小化 → 沙箱隔离 → 注入防御 → 监控响应
- 关键原则：**确定性边界**优先于概率性防御（环境隔离 > 更好的提示词）
- 管理视角：这不是"加个杀毒软件"，是权限与流程的重新设计

🎤 讲者：用"最小权限 + 人工审批 + 网络隔离"三个词总结，管理层可带走。

## 4. 评估模型（6 min）

- 两个工具：
  1. **风险打分**：17 个风险向量 L×I 评分（给单个 Agent 方案打分）
  2. **成熟度模型**：0-5 级 × 5 维度（评估组织整体能力）
- 演示：用一个"读邮件客服 Agent"打分示例说明"为什么判定极危"

🎤 讲者：现场走一遍打分示例（见 evaluation/risk-score.md），让听众看到模型可用。

## 5. 行动建议（4 min）

- 短期（1 周）：Agent 接入审批、权限最小化、开启审批
- 中期（1 月）：沙箱隔离、检测规则、日志审计
- 长期（1 季）：成熟度评估、红队基准、供应链治理

## 6. 资源（Q&A 备料）

- 完整知识库：Agent Security Hub（本仓库）
- 研究报告：library/reports/ai-agent-security-report.md
- 评估模型：docs/evaluation/

🎤 讲者：预告"我们已整理成知识库，可持续收录"，引导后续使用。
```

---

### Task 8: 最终验证

**Files:**
- 校验全部文件

- [ ] **Step 1: 链接与结构检查**

```bash
cd ~/Projects/agent-security-hub
echo "=== 文件树 ==="
find . -type f -name "*.md" | sort
echo "=== 缺失模板检查 ==="
for d in incidents vulnerabilities vendors papers tools; do
  [ -f "library/$d/_template.md" ] || echo "MISSING template: library/$d/_template.md"
done
echo "=== 关键文件 ==="
ls docs/evaluation/ docs/presentation-30min.md library/reports/ai-agent-security-report.md
```

- [ ] **Step 2: 内容抽查（事实纪律）**

```bash
cd ~/Projects/agent-security-hub
echo "=== 来源 URL 检查 ==="
grep -r "http" library/incidents/已证实事件清单.md | wc -l
echo "=== 模板字段检查 ==="
for d in incidents vulnerabilities vendors papers tools; do
  echo "--- $d ---"
  head -5 library/$d/_template.md
done
```

- [ ] **Step 3: 验收核对**

对照设计文档验收标准逐条检查：
1. ✅ 项目结构完整，README 导航清晰
2. ✅ 双评估模型可用（有指引+示例）
3. ✅ 知识库六库齐全，种子内容入库，每库有新增模板
4. ✅ 分享文档可支撑 30 分钟（分节+讲者备注）
5. ✅ 内容延续事实核验纪律

---

## Self-Review 记录

- **Spec 覆盖**：六库（Task1-4）、双模型（Task5-6）、分享文档（Task7）、导航/README（Task1）、验收（Task8）—— 全部覆盖。
- **占位符**：无 TBD/TODO；所有文档给出完整内容框架。
- **一致性**：源文件映射与 Task 内提取内容一致；评估模型引用 reports/incidents/vendors 等链接路径统一。
