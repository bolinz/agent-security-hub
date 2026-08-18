# Risk Assessment Scoring Model

> Used to evaluate the **deployment risk of a candidate Agent system / solution**. Extended from Section 1.7 of the research report *AI Agent Security Challenges and Response Methods*.

> **Model version**: 1.3.0 ｜ **Last review**: 2026-08-18 ｜ **Next review deadline**: 2026-11-18
> **Invalidation triggers**: This model must be re-reviewed when a new incident/vulnerability is added to the library (templates include a registration reminder), the calibration baseline (IBM, etc.) is updated, or the model/vendor ecosystem list changes. Before review, assessment conclusions must be labeled "based on an outdated model". Review actions are recorded in `CHANGELOG.md`.

## Applicability Scope (Mandatory Pre-Check)

- **Applicable**: **Deployment risk** assessment of candidate Agent systems (tool invocation, autonomous execution capability); existing organizational Agent deployments.
- **Not applicable**: Safety-critical systems (physical safety/national security), scenarios not dominated by financial loss (reputation/compliance-led), military/critical infrastructure. Out-of-scope use = calibration failure, conclusions have no reference value.
- **Pre-check**: Confirm applicability before assessment; out-of-scope scenarios must declare "outside model applicability" at the top of the assessment output and stop scoring.

## Usage Guide

- **Assessor**: Security engineer / Architect / Procurement evaluator
- **Subject**: Candidate Agent system (tool invocation, autonomous execution) or existing organizational Agent deployments
- **Output**: Risk level (Low/Medium/High/Critical), verification status, remediation recommendation
- **Mandatory gate**: The model may only be used after passing the [Adversarial Test Cases](./adversarial-test-cases.md); if any case fails → mark "failed adversarial testing" and downgrade the assessment conclusion

## Verification Levels (V0-V3)

> Conclusion credibility is gated by **verification level**, decoupled from L/I numeric computation. Conclusions are triple-locked by "most conservative interpretation + verification gate + deterministic rules". See the red-blue confrontation review: `red-blue-confrontation-report.md`.

| Level | Name | Evidence requirement | Conclusion ceiling |
|-------|------|---------------------|--------------------|
| V0 | Unverified | Self-assessment/declaration only, no independent verification | **Medium** ("Accept" prohibited) |
| V1 | Evidence-attached | Each L/I assignment carries an evidence reference (URL/report/in-library link) | High |
| V2 | Spot-checked | Reviewer independent of the assessment team spot-checks raw evidence, coverage ≥50%, high-risk vectors 100% | Critical |
| V3 | Externally verified | Third-party audit of a representative sample; auditor qualifications public and jointly nominated by both parties | Critical |

- **V0 mandatory clause**: Unverified assessments must not give "Low/Accept" conclusions; high-risk/critical conclusions must attach per-item evidence references.
- Every assessment must declare the verification level at the top of the output (mapped to Tier 0/1/2 verification loops below).

### Verification Loop Tiers 0/1/2

| Tier | Use case | Mechanism | Corresponding V |
|------|----------|-----------|-----------------|
| Tier 0 | No external audit (zero-budget minimum safeguard) | Mandatory "unverified" label + conclusion ceiling (V0) + ≥2 named assessors cross-check (high-risk vectors 100%) + falsification condition attached to each assignment | V0-V1 |
| Tier 1 | Organization has a reviewer independent of the assessed team | Reviewer spot-checks **raw evidence** (not summaries), coverage ≥50%, signs per-item verification statement | V2 |
| Tier 2 | Procurement/compliance scenarios | Third-party audit of a representative sample; **anti-lenient-auditor clause**: auditor must disclose public qualifications, disclose conflicts of interest with the audited party, jointly nominated by both parties | V3 |

- **Auditor independence**: The auditor must not be unilaterally appointed by the assessed party; "completion declaration" must attach an evidence list and signatures; spot-check coverage must not fall below the requirements in the table.

## Scoring Dimensions

- **L (Likelihood 1-5)**: Approximate annual probability of occurrence. L1 <1% / L2 1-10% / L3 10-30% / L4 30-70% / L5 >70%
- **I (Impact 1-5)**: Combined ranking using the **dual-factor (technical impact C/I/A + business impact)** method (per OWASP Risk Rating Methodology); USD is used only as a calibration reference (approximate amounts in the I ranking table below).
- **Risk value = L × I** (1-25). Level determination per the "5×5 Risk Matrix" and "Boundary Hysteresis and Tail Coverage Rules". Note: L and I are both 1-5, so the product can only take values in {1,2,3,4,5,6,8,9,10,12,15,16,20,25}.

### Impact I Ranking Table

| I | Technical impact (C/I/A) | Business impact | USD reference (approx.) |
|---|--------------------------|-----------------|--------------------------|
| 1 | No data disclosure, service available | Negligible impact | <$0.1M |
| 2 | Minor disclosure of non-sensitive data | Minor business loss | $0.1-0.5M |
| 3 | Partial disclosure of sensitive data, partial service outage | Slight brand/compliance damage | $0.5-1M |
| 4 | Large-scale PII disclosure, multi-day business outage | Regulatory penalties, customer churn | $1-5M |
| 5 | Comprehensive data exfiltration, core business outage | Physical safety/societal/major compliance | >$5M |

> Ranking principle: first assess technical impact (what was disclosed, how long the outage), then business impact (financial, reputational, compliance, privacy); **when hard-to-price losses such as physical safety/societal harm are present, escalate I or flag separately** — do not under-rate because something is "hard to price".

## 17-Vector Reference Table

| # | Vector | L | I | Reference risk | Level |
|---|--------|---|---|----------------|-------|
| 1 | Direct prompt injection | 5 | 5 | 25 | Critical |
| 2 | Indirect prompt injection | 5 | 5 | 25 | Critical |
| 3 | Jailbreak | 4 | 4 | 16 | High |
| 4 | Tool misuse/poisoning | 3 | 4 | 12 | Medium |
| 5 | Malicious MCP server | 3 | 4 | 12 | Medium |
| 6 | RCE | 3 | 5 | 15 | High |
| 7 | Data exfiltration | 5 | 5 | 25 | Critical |
| 8 | Credential theft | 4 | 4 | 16 | High |
| 9 | Model theft | 3 | 4 | 12 | Medium |
| 10 | DoS/unbounded consumption | 3 | 3 | 9 | Medium |
| 11 | Agent-to-agent attack | 1* | 4 | 4* | Low* |
| 12 | Malicious/misaligned agent | 4 | 5 | 20 | Critical |
| 13 | Supply chain attack | 4 | 4 | 16 | High |
| 14 | RAG/vector database poisoning | 4 | 4 | 16 | High |
| 15 | System prompt leakage | 4 | 3 | 12 | Medium |
| 16 | Excessive agency/autonomy | 5 | 5 | 25 | Critical |
| 17 | Vishing/deepfake | 4 | 5 | 20 | Critical |

> *Data on agent-to-agent attack frequency is scarce; L1 is a conservative placeholder. L×I is a judgmental assessment (not a measurement); organizations should re-estimate I.

## Scope and Chain Pre-registration

- Before assessment, the applicable vector list (with exclusion reasons) and involved attack chains must be **locked** into the assessment output template.
- Any scope/chain adjustment during assessment must be recorded in a **change log**: `vector change | reason | verification level downgrade`.
- Post-hoc chain breaking/scope narrowing causes a verification level downgrade (e.g., V2→V1), preventing "lock first, change the basis later" gaming.

## Usage Steps

1. **Identify applicable vectors**: Select relevant vectors based on the Agent's capabilities (toolset, permissions, data access); **Agents consuming untrusted content must include injection vectors (#1/#2) — they cannot be excluded**
2. **Set L**: Adjust the reference L based on the environment (whether untrusted content is touched, sandbox present); deviations ≥1 point require written justification and evidence reference
3. **Set I**: Re-estimate I based on the organization's asset inventory (data sensitivity, reachable systems); each I assignment must map to a concrete capability (tools/permissions/data reachability)
4. **Consult the matrix**: L×I gives the risk value; apply the boundary hysteresis and tail coverage rules; bounded by the verification-level conclusion ceiling
5. **Chain check**: For outputs involving attack chains, determine the overall conclusion by boolean gating
6. **Summarize**: Output top risks, overall level (conservative dominance), verification status, and remediation recommendation

## Assessment Output Template

> Every assessment must fill in the following metadata block (Tier 0 minimal verification loop):

```markdown
Verification status: Tier [0/1/2] → V[0-3]
Applicability: ✅ applicable (pre-check passed) / ❌ out of scope
Model version: [version] / [review date]
Adversarial testing: [case set version] / [result: passed/failed]
Assessor signature: [name + role]
Falsification condition: [observing X invalidates this estimate]
Covered vectors: [list, including whether mandatory vectors are satisfied]
Overall level: [Low/Medium/High/Critical]
Remediation: [...]
Verification statement (Tier 1+): [reviewer signature + spot-check coverage]
Auditor statement (Tier 2): [qualifications public + conflict-of-interest disclosure + joint nomination]
```

## 5×5 Risk Matrix

> This matrix is a **lookup table** derived from the L×I formula (not manually assigned per cell) for reporting only. Risk level is determined by the formula + boundary hysteresis + tail coverage rules.

| | I1 | I2 | I3 | I4 | I5 |
|---|---|---|---|---|---|
| **L5** | 5 | 10 | 15 | 20 | 25 |
| **L4** | 4 | 8 | 12 | 16 | 20 |
| **L3** | 3 | 6 | 9 | 12 | 15 |
| **L2** | 2 | 4 | 6 | 8 | 10 |
| **L1** | 1 | 2 | 3 | 4 | 5 |

## Boundary Hysteresis and Tail Coverage Rules

- **Boundary hysteresis**: Products within 1 point of a level boundary are always treated as the **higher level**. Since products in {7,13,14,17-19} are unreachable, the effective rules are: **6→Medium, 12→High, 16→Critical**.
- **Tail coverage rule**: Independent of L — any vector with **I≥4 has a minimum remediation level of "Medium"**, and **I=5 has a minimum of "High"**. Eliminates the structural blind spot where "low-frequency, huge-loss" events would be advised for acceptance.
- **Conservative dominance rule**: In multi-vector assessments, overall risk takes the **highest level** among all applicable vectors (worst case dominates); averages or weighted sums are not used.

## Deterministic Adjustment Rules Table

> L/I assignments should first consult the adjustment rules below; where no rule matches and the deviation is ≥1 point, written justification and evidence reference are required (see usage steps 2/3). **Multiple controls adjusting the same vector are capped at -2 for L and -1 for I; L must not be adjusted below 2.**

| Control/environment | Affected vectors | Adjustment | Activation condition |
|---------------------|------------------|-----------|----------------------|
| Consumes untrusted content without input isolation | #1/#2 | L must not be below 4 | Mandatory (cannot be lowered) |
| Sandbox/input isolation present | #1/#2 | L-1 | Deployed with evidence |
| Injection detection present | #1/#2/#3 | L-1 | Deployed with evidence |
| Output filtering present | #4/#15 | L-1 | Deployed with evidence |
| Egress allowlist present | #7 | L-1 | Deployed with evidence |
| Hard-confirm present | #16 | L-1 | Deployed with evidence |
| Least privilege present | #8/#16 | I-1 | Deployed with evidence |

## Threshold Register

> All decision points must be registered; new thresholds must be registered before use. Boundary behavior is handled uniformly by the "Boundary Hysteresis and Tail Coverage Rules".

| Decision point | Threshold/rule | Owner | Boundary behavior |
|----------------|----------------|-------|-------------------|
| Level determination | Low/Medium/High/Critical (consult matrix) | Model maintainer | Hysteresis upgrade |
| Tail coverage | I≥4 minimum "Medium", I=5 minimum "High" | Model maintainer | Overrides product |
| Verification level | V0-V3 | Assessor | V0 ceiling "Medium", "Accept" prohibited |
| Conservative dominance | Overall = highest level | Model maintainer | Worst case dominates |
| Chain gating | Any high/critical in chain → overall | Assessor | Boolean, not averaged |
| Adjustment stacking | L cap -2, I cap -1, L≥2 | Model maintainer | Ineffective without evidence |
| Mandatory vectors | #1/#2/#7/#8/#16 | Assessor | Exclusion requires independent review |

## Attack Chain Boolean Gating

- Attack chains must be declared and locked at the assessment scope pre-registration stage; post-hoc chain breaking must be recorded with reasons and lowers the verification level.
- **Boolean rule**: If any vector in the chain is High/Critical → the overall conclusion is High/Critical (no averaging across chain steps).
- Standard chain examples: injection → tool misuse → data exfiltration; supply chain → RCE → data exfiltration; RAG poisoning → context contamination → tool misuse.

## Remediation Recommendations

> Level determination order: first consult the matrix by product, then apply boundary hysteresis and tail coverage rules, finally bounded by the verification-level conclusion ceiling.

| Level | Remediation | Constraint |
|-------|-------------|-----------|
| Critical | Deployment gate / fix immediately | Conclusions require per-item evidence references |
| High | Prioritized mitigation (least privilege, output filtering, monitoring) | V0 must not claim "sufficiently mitigated" |
| Medium | Monitor / scheduled re-review | Vectors with I≥4 cannot be merely "accepted" |
| Low | Accept (only for I≤3 and V≥1) | V0 must not "accept" |

## Example: Assessing a "read-email + can-send-email" customer service Agent

1. **Applicable vectors**: #1 direct injection, #2 indirect injection, #7 data exfiltration, #8 credentials, #16 excessive agency
2. **L**: #1/#2 = 5 (touches user email = untrusted content), #7 = 5 (continuously touches untrusted content), #8 = 4, #16 = 5 (permission includes sending)
3. **I**: #1/#2 = 5 (injection can directly drive outbound sends), #7 = 4 (medium PII volume), #8 = 4, #16 = 5 (amplifiable)
4. **Result**: injection 25, exfiltration 20 (L5×I4), credentials 16 (High → boundary hysteresis **upgrades to Critical**), excessive agency 25 → verdict **Critical**; requires least privilege + hard-confirm + egress blocking
5. **Verification**: This example is illustrative. A formal assessment output must attach V≥1 evidence references and fill in the assessment output template.

## Data Sources and Limitations

- I ranking method: per [OWASP Risk Rating Methodology](https://owasp.org/www-community/OWASP_Risk_Rating_Methodology) (technical impact C/I/A + business impact), following NIST AI RMF's mixed qualitative/quantitative measurement approach (https://airc.nist.gov/airmf-resources/airmf/)
- USD calibration baseline: [IBM Cost of a Data Breach 2026](https://www.ibm.com/reports/data-breach) ($4.99M global average / prompt injection $5.89M; retrieved 2026-08-06) — magnitude reference for the I level only, not the primary scoring scale
- Limitations: L×I is a judgmental assessment, not a measurement; conclusion credibility is gated by verification level (V0-V3); vectors with "no public data" (e.g., A2A frequency) should be treated as an uncertainty premium and must not be accepted as low probability; when hard-to-price losses such as physical safety/societal harm are present, escalate I or flag separately
- Full data sources: see Section 1.7 and the verification table of the [research report](../../library/reports/ai-agent-security-report.md)