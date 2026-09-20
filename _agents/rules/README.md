# Agent Behavioral & Engineering Rules (`_agents/rules/`)

This directory contains the authoritative, non-negotiable governance rules that all autonomous AI agents and developers must strictly follow when operating in this repository.

## Rules Catalog

| Rule File | Rule Title | Core Mandate & Enforcement Scope |
| :--- | :--- | :--- |
| **[`spec_driven_development.md`](./spec_driven_development.md)** | **Spec-Driven Development (SDD), Brownfield Protocol & Plan Tracking** | Spec first, code second. Phase 0 brownfield baseline under `specs/baseline/`. Granular step-by-step implementation plans. Mandatory Unit Tests + Property-Based Tests (PBT) for every step. Continuous progress tracking in `specs/plan/`. Zero spec drift. |
| **[`devops_security_and_quality_standards.md`](./devops_security_and_quality_standards.md)** | **DevOps, Security, Quality & Cloud Run Standards** | 10 enterprise rules: Multi-branch promotion (`main`/`develop` $\rightarrow$ `prod`), pre-build CodeMender SAST (`cm`), automated Cloud Build CI/CD, Cloud Run hosting for web apps/proxies with `/healthz` liveness probes, post-deploy smoke tests, unified `.env` parameter management, Infrastructure Manager Terraform IaC, and Domain Restricted Sharing (zero `allUsers`). |
| **[`google_adk_and_agent_runtime.md`](./google_adk_and_agent_runtime.md)** | **Google ADK, Agent Runtime, Model-Driven Reasoning & Live Evaluation** | Conversational AI agents built with official `google-adk` (`Agent`, `FunctionTool`, `before_agent_callback`) and deployed to the Gemini Enterprise Agent Platform (`agent_runtime`) via `agents-cli deploy`. Purely cognitive model-driven reasoning; zero regex or hardcoded routing. Continuous live evaluation (`agents-cli eval`) requiring $\ge 95\%$ precision and 1.000 groundedness. |
| **[`root_cause_investigation_and_zero_quick_patch.md`](./root_cause_investigation_and_zero_quick_patch.md)** | **Root Cause Investigation & Zero Quick-Patch Standard** | Mandatory 4-step RCA protocol on failing tests or evals. Strict prohibition of quick fixes, mockups, regex workarounds, or assertion weakening. Transparent failure explanation to user, presentation of architectural fix options with trade-offs, and awaiting user approval before coding. |

---

## Runtime Separation Matrix

This project strictly delineates workloads across two execution runtimes:

```
+-------------------------------------------------------------+
|                      Client Workloads                       |
|           (Web UI, Streaming Audio/Video, Mobile)           |
+-------------------------------------------------------------+
                              │
               HTTPS / WSS    ▼
+-------------------------------------------------------------+
|               Google Cloud Run (cloud_run)                  |
|  - React / Vite Web Frontends                               |
|  - Reverse Proxies & Streaming API Gateways                 |
|  - Health Probes (/healthz) & Observability                 |
|  - Deployed via Cloud Build + Terraform IaC                 |
+-------------------------------------------------------------+
                              │
              Session Stream  ▼
+-------------------------------------------------------------+
|      Gemini Enterprise Agent Platform (agent_runtime)       |
|  - ADK Orchestrator & Domain Subagents                      |
|  - Cognitive Model-Driven Reasoning (Zero Regex/Heuristics) |
|  - Model Armor Safety Callbacks                             |
|  - FunctionTool Registries & External Backend Integrations  |
|  - Evaluated via agents-cli eval (>= 95% precision, 1.000 G)|
|  - Deployed via agents-cli deploy                           |
+-------------------------------------------------------------+
```

---

## Enforcement & Compliance
- **Automated Validation:** Rules are enforced by CI/CD quality gates, pre-commit checks, and evaluation suites.
- **Specification Linkage:** Every specification authored in [`specs/features/`](../../specs/features/) must verify compliance against each rule using Section 6 of [`specs/templates/sdd-template.md`](../../specs/templates/sdd-template.md).
