# 贡献指南

感谢你愿意为 Agent Security Hub 贡献内容。

## 核心原则

- **纯 Markdown，零依赖**：不引入构建工具、脚本或数据库。
- **事实核验纪律**：所有数据来源可溯、区分事实/估算/建议、标注检索日期。
- **结构约定**：新增内容按各库 `_template.md` 模板填写，保证一致性与可维护性。

## 如何新增条目

### 事件（incidents/）

1. 复制 `library/incidents/_template.md` 为 `library/incidents/YYYY-MM-事件名.md`（kebab-case）。
2. 填写 frontmatter（title/date/type/severity/status/impact/last_updated/tags/related_cves/related_reports）。
3. 填写事件概述 / 经过 / 影响与损失 / 来源。
4. 补充 `library/incidents/已证实事件清单.md` 与 `library/incidents/README.md` 中的对应行。

### 漏洞（vulnerabilities/）

1. 复制 `library/vulnerabilities/_template.md` 为 `library/vulnerabilities/CVE-YYYY-XXXXX.md`。
2. 填写 frontmatter（title/cve/component/type/cvss/affected_versions/fixed_version/status/in_wild/last_updated/tags/related_incidents/related_reports）。
3. 填写漏洞信息 / 漏洞机理 / 影响 / 来源。
4. 补充 `library/vulnerabilities/CVE清单.md` 与 `library/vulnerabilities/README.md` 中的对应行。

### 厂商 / 论文 / 工具

分别复制 `library/vendors/_template.md`、`library/papers/_template.md`、`library/tools/_template.md`，并更新对应清单与 README。

## 数据要求

| 要求 | 说明 |
|------|------|
| 来源 URL | 每个条目必须给出可访问的一手/权威来源链接 |
| 检索日期 | 记录你检索/核验信息的日期 |
| 事实/估算/建议 | 明确区分：事实（有来源）、估算（给出依据与区间）、建议（明确标注为建议） |
| 核验状态 | 已证实 ✅ / 部分证实 ⚠️ / 未证实 ❌，并在报告核验表（06-fact-check.md）登记 |

## 更新报告索引

- 新增事件/漏洞后，若其属于风险值 ≥ 15 的向量或主要主题，同步更新 `docs/index.md` 对应章节。
- 评估模型（`docs/evaluation/`）引用知识库数据时，保持链接有效。

## 提交

- 提交信息使用简洁的中文或英文，说明变更内容。
- 建议每次提交聚焦单一主题（如"新增某事件条目"或"修复某链接"）。