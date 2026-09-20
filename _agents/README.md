# Agent Governance, Rules & Skills Framework (`_agents/`)

This directory houses the foundational rules, operational guidelines, and specialized skills governing autonomous AI agents and human developers operating within this repository.

## Directory Structure

```
_agents/
├── README.md                      # Index and framework overview
├── rules/                         # Repository governance and engineering rules
│   ├── README.md                  # Rules catalog and enforcement summary
│   ├── spec_driven_development.md # Spec-Driven Development, baseline protocol & plan tracking
│   ├── devops_security_and_quality_standards.md # 10 DevOps, CI/CD, CodeMender SAST & IaC standards
│   ├── google_adk_and_agent_runtime.md # Google ADK, Agent Runtime, Model-Driven Reasoning & Live Eval
│   └── root_cause_investigation_and_zero_quick_patch.md # 4-step RCA protocol & zero quick-patch standard
└── skills/                        # Specialized agent skill toolkits
    ├── README.md                  # Skills catalog and operational workflows
    ├── architecture_diagram/      # Professional technical/cloud architecture diagrams & HTML assets
    ├── codemender/                # Pre-build SAST vulnerability discovery, triage, and patching
    └── gcp_cost_estimator/        # Real-time GCP cloud cost estimation using live Billing API rates
```

---

## The Four Governance Rule Pillars

All agent and developer workflows must comply strictly with the four rule pillars codified in [`_agents/rules/`](./rules/):

1. **Spec-Driven Development (SDD):** Spec first, code second. Brownfield baseline required under `specs/baseline/` before delta authoring. Granular step-by-step implementation plans with Unit and Property-Based Tests (PBT) at every step. Continuous progress tracking in `specs/plan/` ([`_agents/rules/spec_driven_development.md`](./rules/spec_driven_development.md)).
2. **DevOps, Security & Cloud Run Services:** Single GitHub repository with multi-branch promotion. Pre-build SAST with CodeMender. Cloud Build CI/CD, Cloud Run hosting for web frontends and streaming API proxies with `/healthz` liveness probes, unified single-file `.env` parameter management, Infrastructure Manager Terraform IaC, and Domain Restricted Sharing (zero `allUsers`) ([`_agents/rules/devops_security_and_quality_standards.md`](./rules/devops_security_and_quality_standards.md)).
3. **Google ADK & Agent Platform Runtime:** Conversational AI agents and reasoning engines built with official Google ADK (`google-adk`) and deployed exclusively to the Gemini Enterprise Agent Platform (`agent_runtime`) via `agents-cli deploy`. Strictly cognitive model-driven reasoning and structured FunctionTools; zero hardcoded keywords or regex routing. Live evaluation via `agents-cli eval` ($\ge 95\%$ tool selection precision, 1.000 groundedness) ([`_agents/rules/google_adk_and_agent_runtime.md`](./rules/google_adk_and_agent_runtime.md)).
4. **Root Cause Investigation & Zero Quick-Patch Standard:** Mandatory 4-step RCA protocol when tests or evals fail. Zero quick fixes, mockups, regex workarounds, or assertion weakening. Deep RCA, transparent explanation to user, viable architectural fix options with trade-offs, and awaiting explicit user instruction before coding ([`_agents/rules/root_cause_investigation_and_zero_quick_patch.md`](./rules/root_cause_investigation_and_zero_quick_patch.md)).

---

## Runtime Separation Architecture

| Workload Dimension | Conversational AI Agents & Reasoning Engine | Web Frontend, API Gateway & Streaming Proxies |
| :--- | :--- | :--- |
| **Target Runtime** | **Gemini Enterprise Agent Platform (`agent_runtime`)** | **Google Cloud Run (`cloud_run`)** |
| **Artifacts** | ADK Root Coordinator, Subagents, Model Armor hooks, `FunctionTool` registries. | React/Vite UI, Express/FastAPI proxy, WebSocket/SSE endpoints. |
| **Deployment** | `agents-cli deploy --deployment-target agent_runtime` | Cloud Build (`cloudbuild.yaml`) + Terraform via Infrastructure Manager |
| **Governance Rule** | [`_agents/rules/google_adk_and_agent_runtime.md`](./rules/google_adk_and_agent_runtime.md) | [`_agents/rules/devops_security_and_quality_standards.md`](./rules/devops_security_and_quality_standards.md) |

---

## Related Documentation
- **Operating Manual:** [`AGENTS.md`](../AGENTS.md)
- **Specifications Registry:** [`specs/README.md`](../specs/README.md)
- **Operational Reports:** [`docs/README.md`](../docs/README.md)
