# Agent Security Maturity Model

> Assesses the **stage of an organization's Agent security capability** (not individual systems). CMMI-style levels 0-5 × 5 dimensions.

> **Model version**: 1.3.0 ｜ **Last review**: 2026-08-18 ｜ **Next review deadline**: 2026-11-18
> **Invalidation triggers**: This model must be re-reviewed when a new incident/vulnerability is added to the library, the calibration baseline is updated, or the model/vendor ecosystem list changes. Before review, assessment conclusions must be labeled "based on an outdated model".

## Usage Guide

- **Assessor**: Security lead / Compliance / Architecture
- **Subject**: Organization as a whole (Agent deployments, processes, governance)
- **Output**: Level per dimension + overall level (bottleneck = lowest dimension) + verification status

## Five Dimensions

1. **Governance**: Policy, accountability, approval process, risk register
2. **Architecture**: Least privilege, sandboxing/isolation, identity management
3. **Guardrails**: Injection defense, output filtering, HITL
4. **Monitoring**: Detection rules, log auditing, response process
5. **Supply chain**: MCP/dependency governance, SBOM, provenance verification

## Level Definitions (per dimension)

| Level | Name | Behavioral description | Evidence requirement |
|-------|------|------------------------|----------------------|
| 0 | None | No Agent security practices; Agents connect freely | None |
| 1 | Initial | Scattered awareness, no standard; ad hoc in individual projects | Scattered documents / verbal conventions |
| 2 | Managed | Basic policy and permission control; Agents require approval to connect | Policy documents, approval records |
| 3 | Defined | Defense-in-depth institutionalized; standard processes for guardrails/monitoring/supply chain | Institutional documents, detection rules, audit logs |
| 4 | Quantitatively managed | Security metrics (injection ASR, rejection rate, coverage) exist and are measured; metrics must be extracted from logs/system measurement with clear direction | Metric dashboards, trend reports (derived from log measurement, not self-reported) |
| 5 | Optimizing | Continuous improvement; red-team/benchmark exercises are routine; discovered issues have closed-loop remediation records | Red-team reports, improvement records (with issue → remediation → re-test loop) |

## Assessment Process

1. Locate the current level per dimension (against the behavioral descriptions)
2. Collect evidence (policy documents, logs, rules, metrics)
3. Identify gaps: target level vs. current level
4. Build a roadmap: advance per dimension level by level (bottleneck dimension first)

### Verification Requirements

- Every assessment must fill in a **verification status metadata block** (verification level, assessor signature, falsification condition, model version; defined in [risk-score.md](./risk-score.md) "Verification Levels V0-V3").
- Self-assessment evidence must be graded: **declaration / document / measurement / independent audit**. Without measurement or independent verification, the conclusion is labeled **"nominal level (unverified)"** and must not be used as an external assurance signal.
- **Conservative dominance rule**: The overall level takes the **lowest dimension (bottleneck)**; if any dimension is level 0, a dedicated risk re-review is mandatory regardless of how high the other dimensions are.

### Metric Evidence Standards (L4/L5)

- Metrics must be extracted from **logs/system measurement**; self-reported tables are prohibited.
- Each metric must be registered with: **direction** (higher/lower is better), **calculation formula**, **data source**.
- Outcome-type metrics are preferred: injection blocking rate, incident response p90, mean time to repair (MTTR), red-team escape rate; avoid ambiguous-direction metrics such as "approval rate" (substitute "rejection rate + approval latency p90 + share of approvals without justification").
- L5 red-team/benchmark reports must include the **improvement loop**: previously found issue → remediation action → re-test result.

## Example: A Team Assessment

| Dimension | Current level | Target level | Gap action |
|-----------|--------------|--------------|------------|
| Governance | 2 | 3 | Establish Agent connection approval policy and risk register |
| Architecture | 2 | 3 | Introduce sandboxing and least privilege for high-privilege Agents |
| Guardrails | 1 | 3 | Deploy injection detection + output filtering + HITL |
| Monitoring | 1 | 3 | Implement Sigma rules and audit logging |
| Supply chain | 1 | 2 | Establish MCP/dependency allowlist and provenance verification |

Overall level = lowest dimension = 1 → prioritize guardrails/monitoring/supply chain.

## Cooperation with the Risk Model

- **Maturity model** assesses organizational capability; **risk model** assesses individual system risk
- Recommendation: first do maturity positioning (find gaps), then use the risk model to score high-risk Agents (prioritize)
- Tool assets: see [library/tools](../../library/tools/README.md); assessment data references: [library/incidents](../../library/incidents/README.md) and [library/vulnerabilities](../../library/vulnerabilities/README.md)