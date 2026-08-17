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
