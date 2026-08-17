---
name: red-blue-confrontation
description: Adversarial security analysis for AI agent systems using red team (attacker) and blue team (defender) subagents. Use when evaluating security of code, configurations, or architecture; assessing prompt injection risks; reviewing tool permissions; validating defense mechanisms; or conducting pre-deployment security audits.
---

# Red-Blue Confrontation

Adversarial security analysis for AI agent systems using red team (attacker) and blue team (defender) subagents.

## Purpose

Deep-dive security risk assessment through turn-based adversarial analysis. The Red Team finds vulnerabilities while the Blue Team proposes defenses, iterating until consensus is reached.

## When to Use

- Evaluating security of AI agent code, configurations, or architecture
- Assessing prompt injection risks
- Reviewing tool permissions and access controls
- Validating defense mechanisms
- Pre-deployment security audits

## Workflow

```
User Input (code/config/architecture)
        |
    Round 1: Red Team analyzes -> finds vulnerabilities
        |
    Round 1: Blue Team responds -> proposes defenses
        |
    Round 2: Red Team validates -> checks defense effectiveness
        |
    Round 2: Blue Team optimizes -> refines defenses
        |
    Round 3: Final consensus check
        |
    Generate structured report
```

## How to Execute

### Step 1: Gather Input

Ask the user what content they want to evaluate:
- Source code files
- Configuration files (YAML, JSON, TOML)
- Architecture diagrams or descriptions
- Agent permission settings
- MCP server configurations

### Step 2: Red Team Analysis (Round 1)

Use the Task tool to launch the Red Team subagent:

```
Task with subagent_type: "explore"

Prompt: Read the file .opencode/skills/red-blue-confrontation/red-team-agent.md for your role definition.

Analyze the following content for security vulnerabilities:

[paste content here]

Follow the output format specified in your role definition.
```

### Step 3: Blue Team Analysis (Round 1)

Use the Task tool to launch the Blue Team subagent:

```
Task with subagent_type: "explore"

Prompt: Read the file .opencode/skills/red-blue-confrontation/blue-team-agent.md for your role definition.

The Red Team has identified the following vulnerabilities:

[insert Red Team findings]

Follow the output format specified in your role definition.
```

### Step 4: Red Team Validation (Round 2)

Launch Red Team again to validate Blue Team's defenses:

```
Task with subagent_type: "explore"

Prompt: Read the file .opencode/skills/red-blue-confrontation/red-team-agent.md for your role definition.

The Blue Team has proposed the following defenses:

[insert Blue Team recommendations]

For each defense, evaluate:
1. Is it sufficient to mitigate the vulnerability?
2. Are there bypass techniques?
3. What gaps remain?

Output format:
## Validation Results
| Vuln # | Defense | Status (Effective/Partial/Ineffective) | Bypass Risk | Remaining Gaps |
|--------|---------|----------------------------------------|-------------|----------------|

## Unresolved Vulnerabilities
- [List any vulnerabilities not adequately addressed]
```

### Step 5: Blue Team Optimization (Round 2)

Launch Blue Team again to address gaps:

```
Task with subagent_type: "explore"

Prompt: Read the file .opencode/skills/red-blue-confrontation/blue-team-agent.md for your role definition.

The Red Team found gaps in your defenses:

[insert Red Team validation results]

Optimize the defense recommendations to address these gaps.

Output format:
## Optimized Defenses
| # | Original Defense | Enhancement | New Effectiveness |
|---|------------------|-------------|-------------------|

## Additional Controls
- [Any new controls needed]
```

### Step 6: Final Consensus (Round 3)

Launch Red Team one final time for consensus check:

```
Task with subagent_type: "explore"

Prompt: Read the file .opencode/skills/red-blue-confrontation/red-team-agent.md for your role definition.

Blue Team has optimized their defenses:
[insert optimized defenses]

Confirm:
1. All critical vulnerabilities are addressed
2. Defenses are practical to implement
3. Residual risk is acceptable

Output:
## Final Verdict
- Consensus reached: [Yes/No]
- Residual risk level: [Low/Medium/High]
- Remaining concerns: [list]
```

### Step 7: Generate Report

Compile all findings into a structured Markdown report and save to the project:

```markdown
# Red-Blue Confrontation Report

## Summary
- **Target**: [file/content evaluated]
- **Date**: [date]
- **Rounds**: 3
- **Final Status**: [Consensus reached / Not reached]
- **Residual Risk**: [Low/Medium/High]

## Vulnerabilities Found (Red Team - Round 1)

| # | Type | Severity | Attack Vector | Potential Impact |
|---|------|----------|---------------|------------------|
| 1 | [type] | [severity] | [vector] | [impact] |

## Defense Recommendations (Blue Team - Round 1)

| # | Defense | Difficulty | Effectiveness | Priority |
|---|---------|------------|---------------|----------|
| 1 | [defense] | [difficulty] | [effectiveness] | [priority] |

## Validation Results (Round 2)

| Vuln # | Defense | Status | Bypass Risk | Remaining Gaps |
|--------|---------|--------|-------------|----------------|
| 1 | [defense] | [status] | [risk] | [gaps] |

## Optimized Defenses (Round 2)

| # | Original | Enhancement | New Effectiveness |
|---|----------|-------------|-------------------|
| 1 | [original] | [enhancement] | [effectiveness] |

## Final Consensus (Round 3)

- **All critical vulnerabilities addressed**: [Yes/No]
- **Defenses practical to implement**: [Yes/No]
- **Residual risk acceptable**: [Yes/No]

## Action Items

| # | Action | Priority | Owner |
|---|--------|----------|-------|
| 1 | [action] | [priority] | [owner] |

## References

- MITRE ATLAS: https://atlas.mitre.org/
- OWASP Agentic Top 10: https://genai.owasp.org/
- NIST AI RMF: https://www.nist.gov/itl/ai-risk-management-framework
```

## Key Principles

1. **Adversarial mindset**: Red Team thinks like an attacker, Blue Team thinks like a defender
2. **Evidence-based**: All findings must reference specific code/config sections
3. **Actionable**: Every vulnerability must have a corresponding defense
4. **Iterative**: Multiple rounds ensure completeness
5. **Consensus-driven**: Final report only when both teams agree

## Limitations

- Analysis is based on static review (no live testing)
- Effectiveness depends on subagent's knowledge of attack patterns
- Should be complemented with actual penetration testing for critical systems
