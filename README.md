# Dissemination Control for AI Agents

**An architecture blueprint for governing what AI agents share, with whom, and in which context.**

---

## The Problem

Enterprise AI agents access ticket systems, wikis, CRMs, and internal documents. They communicate across channels with different audiences. Existing security models handle authentication and authorisation — but they don't address a third question:

| Layer | Question | Status |
|---|---|---|
| Authentication | Who is the agent? | Solved |
| Authorisation | What may it access? | Solved |
| **Dissemination Control** | **What may it say where?** | **Open** |

A human employee with access to HR data doesn't post salary information in the public team channel. Not because IAM prevents it — they have read access — but because they understand the social context.

AI agents decide based on **relevance**, not **confidentiality**. The most helpful answer to a harmless question is often the one containing sensitive information. This is not a bug in the model. It is a structural gap in how we govern AI agents.

## What This Blueprint Covers

A vendor-neutral reference architecture for Dissemination Control — the governance layer that ensures AI agents follow context-dependent rules about information sharing. It builds on existing IAM infrastructure and requires no global data classification effort.

**Five governance layers:**

- **Tool Containment** — The agent can only use tools explicitly whitelisted for the current context. What is not enabled does not exist.
- **Behavioural Steering** — Version-controlled prompt policies that control how the agent behaves within its permitted scope.
- **Identity Delegation** — The agent acts with the requesting user's permissions via token exchange, not a service account.
- **Dissemination Policy** — Context-dependent rules: same data, different visibility depending on channel and audience.
- **Compliance Audit** — Complete audit trail of all access, all tool calls, all blocked requests.

**Four adoption tiers** — each adding exactly one capability:

```
Tier 1: Tool Containment          → "The agent can't see it"
Tier 2: + Identity Delegation     → "The agent sees only what you see"
Tier 3: + Dissemination Policy    → "The agent shares only what fits the context"
Tier 4: + Compliance Monitoring   → "Every action is audited and anomalies are flagged"
```

Tier 1 can be implemented in days. No IAM changes needed. Just policy configuration.

## What This Blueprint Does NOT Cover

This is the infrastructure governance layer. It complements — but does not replace — other AI security concerns:

- Prompt injection detection (→ Lakera, Prompt Armor, et al.)
- Output content filtering and toxicity detection
- EU AI Act risk classification
- Responsible AI, bias, and fairness
- LLM model selection and evaluation

The guardrail providers protect the model. This blueprint protects your infrastructure from the model.

## The Blueprint

→ **[dissemination-control-blueprint.md](dissemination-control-blueprint.md)**

Includes: problem statement, design principles, five governance layers, three-tier governance model (admin → user → IAM), component architecture with full request flow, defence-in-depth analysis, knowledge base scoping, context window management, compliance process, adoption tiers, prerequisites, design decisions, known limitations, and a reference implementation mapping.

## Reference Implementation

The architecture has been validated on a live environment with the following stack (details in the blueprint):

| Role | Implementation |
|---|---|
| Communication Platform | Mattermost |
| LLM Provider | Anthropic Claude |
| Custom MCP Server | Spring Boot |
| Identity Provider | Keycloak (Token Exchange) |
| Policy Engine | OPA / Rego |
| Target Systems | YouTrack, Outline, OpenProject, Notion |

The architecture is vendor-neutral. Each component role can be fulfilled by equivalent products (Slack, Teams, Entra ID, Okta, Jira, Confluence, etc.).

## About

This blueprint is maintained by [Jahn Consulting](https://jahnconsulting.io), a consultancy specialising in AI agent governance architecture.

If your organisation is deploying AI agents with tool access in multi-user environments and you need to ensure they operate within your existing governance perimeter — [let's talk](https://jahnconsulting.io).

## License

[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) — share and adapt for any purpose, including commercial use, with attribution.