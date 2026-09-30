# Spec-Driven Development (SDD) & DevSecOps Platform

An enterprise platform and engineering framework operating under the **3-Phase AI-Driven Software Development Lifecycle (AI-SDLC)**, strict **Spec-Driven Development (SDD)**, Google Agent Development Kit (ADK) standards, Gemini Enterprise Agent Platform runtime, and multi-tier DevOps/Security governance.

---

## 🏛️ Core Architecture & Governance Pillars

This repository is governed by five core pillars codified under [`_agents/rules/`](./_agents/rules/), orchestrated by the **[`ai-sdlc` skill](./_agents/skills/ai_sdlc/SKILL.md)** and [`AGENTS.md`](./AGENTS.md):

```
+=================================================================================================+
|                  3-Phase AI-Driven Software Development Lifecycle (AI-SDLC)                     |
|   Phase 1: Inception (Intent & Arch) -> Phase 2: Execution (SDD) -> Phase 3: Operation (Deploy) |
|   (Proactive ask_question clarification on unknowns & interactive sign-off at every phase gate) |
+=================================================================================================+
                                                  │
                                                  ▼
+-------------------------------------------------------------------------------------------------+
|                                    Spec-Driven Development (SDD)                                |
|  - Spec First, Code Second  - Brownfield Baseline Required  - Unit & Property Tests at Every Step |
+-------------------------------------------------------------------------------------------------+
                                                  │
                 ┌────────────────────────────────┴───────────────────────────────┐
                 ▼                                                                ▼
+--------------------------------------------------+    +--------------------------------------------------+
|           Enterprise DevOps & Security           |    |            Google ADK & Agent Runtime            |
| - Multi-Branch SCM (main -> prod)                |    | - Gemini Enterprise Agent Platform (agent_runtime)|
| - Pre-Build SAST with CodeMender (cm)            |    | - ADK Orchestrator & Domain Subagents            |
| - Google Cloud Build CI/CD                       |    | - Model-Driven Reasoning (Zero Regex/Heuristics) |
| - Cloud Run Web Frontends & Streaming Gateways   |    | - Continuous Live Evaluation (agents-cli eval)   |
| - Infrastructure Manager Terraform IaC           |    | - FunctionTool Registries & Model Armor Hooks    |
| - Domain Restricted Sharing (Zero allUsers)      |    |                                                  |
+--------------------------------------------------+    +--------------------------------------------------+
                                                  │
                                                  ▼
+-------------------------------------------------------------------------------------------------+
|                         Root Cause Investigation & Zero Quick-Patch Standard                    |
|  - Mandatory 4-Step RCA Protocol  - Zero Quick Fixes / Mockups  - Await User Architectural Direction|
+-------------------------------------------------------------------------------------------------+
```

---

## ⚡ Runtime Architecture & Separation of Responsibilities

Workloads in this project are strictly decoupled across two runtime environments:

| Dimension | Conversational AI Agents & Reasoning Engine | Web Frontend, API Gateway & Streaming Proxies |
| :--- | :--- | :--- |
| **Target Runtime** | **Gemini Enterprise Agent Platform (`agent_runtime`)** | **Google Cloud Run (`cloud_run`)** |
| **Deployed Artifacts** | ADK Root Coordinator (`OrchestratorAgent`), Domain Subagents, cognitive system prompts, Model Armor security callbacks, and `FunctionTool` registries. | React/Vite web client, Express/FastAPI proxy, WebSocket/SSE streaming endpoints, and background worker jobs. |
| **Deployment Mechanism** | `agents-cli deploy --deployment-target agent_runtime` | Google Cloud Build (`cloudbuild.yaml`) + Terraform via Google Cloud Infrastructure Manager |
| **Core Responsibilities** | Autonomous multi-turn reasoning, session persistence (`agentengine://`), live tool execution, and trajectory evaluation (`agents-cli eval`). | HTTP/HTTPS ingress, IAP authentication gateway, client UI rendering, health probes (`/healthz`), and thin proxying to the Agent Platform. |
| **Governance Rule** | [`_agents/rules/google_adk_and_agent_runtime.md`](./_agents/rules/google_adk_and_agent_runtime.md) | [`_agents/rules/devops_security_and_quality_standards.md`](./_agents/rules/devops_security_and_quality_standards.md) |

---

## 📁 Repository Structure & Workspace Scaffolding

The template directories for `specs/` and `docs/` are packaged inside [`_agents/skills/ai_sdlc/examples/`](./_agents/skills/ai_sdlc/examples/). When the **`ai-sdlc` skill** is activated on a project (`python3 _agents/skills/ai_sdlc/scripts/validate_sdlc_gate.py --init`), it automatically scaffolds `specs/` and `docs/` into the project root:

```
├── AGENTS.md                      # Authoritative Agent Operating Manual & Executive Governance Router
├── README.md                      # Project root documentation & architecture overview
├── _agents/                       # Agent governance rules and specialized skill toolkits
│   ├── rules/                     # Consolidated governance rules (always_on + model_decision)
│   │   ├── ai_sdlc_and_sdd_standards.md
│   │   ├── google_adk_and_agent_runtime.md
│   │   └── devops_security_and_quality_standards.md
│   └── skills/                    # Agent operational skills
│       ├── ai_sdlc/               # Master 3-Phase AI-SDLC orchestrator (Inception, Execution, Operation)
│       │   ├── SKILL.md           # Workflow instructions & phase-by-phase output map
│       │   ├── scripts/           # validate_sdlc_gate.py (--init scaffolder & phase gate validator)
│       │   └── examples/          # Seed templates for specs/ and docs/ scaffolded on skill activation
│       │       ├── specs/         # SDD templates (baseline/, features/, plan/, templates/sdd-template.md)
│       │       └── docs/          # Operational report index (README.md)
│       ├── architecture_diagram/  # Technical architecture diagrams & standalone HTML assets
│       ├── codemender/            # Pre-build SAST vulnerability discovery, triage, and patching
│       └── gcp_cost_estimator/    # Live GCP Billing API cost estimation & BoM calculation
├── specs/                         # [Created on ai-sdlc activation] Single Source of Truth for SDD
│   ├── README.md                  # Specifications index and SDD registry
│   ├── templates/                 # Reusable SDD templates (sdd-template.md)
│   ├── baseline/                  # Brownfield baseline specifications (as-is state)
│   ├── features/                  # Proposed feature specifications & implementation plans
│   └── plan/                      # Living execution progress reports and milestone tracking
└── docs/                          # [Created on ai-sdlc activation] Operational reports, cost models & diagrams
    ├── README.md                  # Documentation index & naming conventions
    ├── *-architecture.md          # Architecture designs & HTML companion visual assets
    ├── codemender-*.md            # SAST security vulnerability scan & patch reports
    └── gcp_cost_estimate_*.md     # Live cloud cost models & itemized BoMs
```

---

## 🗂️ Phase-by-Phase Output Folder Map (`ai-sdlc`)

| AI-SDLC Phase | Deliverable / Activity | Target Output Folder in Project Root | File Naming Pattern |
| :--- | :--- | :--- | :--- |
| **Phase 0: Activation** | Workspace Scaffolding (`validate_sdlc_gate.py --init`) | `specs/` & `docs/` | Copies seed structure from `_agents/skills/ai_sdlc/examples/{specs,docs}/` |
| **Phase 1: Inception** | Brownfield "As-Is" Discovery *(if brownfield)* | `specs/baseline/` | `specs/baseline/system-overview.md` or `<subsystem>-baseline.md` |
| **Phase 1: Inception** | Intent, Scope & Dual-Runtime Architecture Frame | `specs/features/` | `specs/features/SPEC-<YYYYMMDD>-<FEATURE>.md` *(Sections 1 & 2)* |
| **Phase 1: Inception** | Visual Architecture Diagram (`architecture-diagram`) | `docs/` | `docs/<project>-architecture.md` & `docs/<project>-architecture.html` |
| **Phase 1: Inception** | Cloud Cost Estimate (`gcp-cost-estimator`) | `docs/` | `docs/gcp_cost_estimate_<project>.md` |
| **Phase 2: Execution** | Full SDD Specification & Step-by-Step Test Plan | `specs/features/` | `specs/features/SPEC-<YYYYMMDD>-<FEATURE>.md` *(Sections 1–8)* |
| **Phase 2: Execution** | ADK Agents & Tools (`agent_runtime`) | `app/` (or `agents/`) | `agent.py`, `tools/*.py`, `callbacks/*.py`, `agents-cli-manifest.yaml` |
| **Phase 2: Execution** | Cloud Run Web UI & Streaming Proxy (`cloud_run`) | `src/` & `server/` | React/Vite UI (`src/`), Express/FastAPI proxy + `/healthz` (`server/`) |
| **Phase 2: Execution** | Unit Tests, Property-Based Tests (PBT) & Evals | `tests/` & `evals/` | `tests/unit/`, `tests/property/`, `evals/datasets/*.jsonl` |
| **Phase 2: Execution** | Living Plan Progress Report & RCA Log | `specs/plan/` | `specs/plan/PROGRESS_REPORT_<YYYYMMDD>.md` & `specs/README.md` |
| **Phase 3: Operation** | Pre-Build CodeMender SAST Reports (`codemender`) | `docs/` | `docs/codemender-01-*.md` .. `03-*.md`, `codemender-security-audit-summary.md` |
| **Phase 3: Operation** | CI/CD Pipeline, IaC & Unified Environment Config | Root & `terraform/` | `cloudbuild.yaml`, `.env.example`, `terraform/*.tf` |
| **Phase 3: Operation** | Post-Deploy Verification, Smoke Tests & Live Eval | `specs/plan/` | Final update to `specs/plan/PROGRESS_REPORT_<YYYYMMDD>.md` |

---

## 🔄 3-Phase AI-SDLC & Spec-Driven Development (SDD) Workflow

Every development task is guided by [`_agents/skills/ai_sdlc/SKILL.md`](./_agents/skills/ai_sdlc/SKILL.md) through three gated phases:

```
+-------------------------------------------------------------------------+
| PHASE 1: INCEPTION (Intent Framing & Architecture)                      |
|  - Scaffold specs/ & docs/ in root (validate_sdlc_gate.py --init)       |
|  - Elicit business intent, personas, goals/non-goals via ask_question   |
|  - Identify brownfield vs. greenfield scope (specs/baseline/)           |
|  - Define Dual-Runtime split (agent_runtime vs cloud_run) & IAM pattern |
|  - Offer companion skills: architecture-diagram & gcp-cost-estimator    |
+-------------------------------------------------------------------------+
                                    │
                     [Gate 1: ask_question Sign-Off]
                                    ▼
+-------------------------------------------------------------------------+
| PHASE 2: EXECUTION (The Spec-Driven Development Cycle)                  |
|  - SDD Phase 0: Baseline Discovery (Brownfield -> specs/baseline/)      |
|  - SDD Phase 1: Specification Authoring (specs/features/SPEC-*.md)      |
|  - SDD Phase 2: Detailed Implementation Plan + Test Design (Unit + PBT) |
|  - SDD Phase 3: Stakeholder Alignment Sub-Gate (ask_question Sign-Off)  |
|  - SDD Phase 4: Step-by-Step Implementation + Tests (4-Step RCA on fail)|
|  - SDD Phase 5: Verification, Spec Sync & Living Plan (specs/plan/)     |
+-------------------------------------------------------------------------+
                                    │
                     [Gate 2: ask_question Sign-Off]
                                    ▼
+-------------------------------------------------------------------------+
| PHASE 3: OPERATION (Integrate Code into Repository & Deploy)            |
|  - Pre-Merge Gate: Static Analysis + CodeMender SAST + Unified .env     |
|  - Git Multi-Branch Integration (main/develop -> reviewed PR to prod)   |
|  - Dual-Runtime Deploy: agents-cli deploy + Cloud Build & Terraform IaC |
|  - Post-Deploy Gate: Live /healthz smoke tests + live agents-cli eval   |
+-------------------------------------------------------------------------+
```

### Mandatory Testing Standards for Every Step
- **Unit Tests:** Deterministic boundary, edge-case, and error-handling tests.
- **Property-Based Tests (PBT):** Invariant testing across generative fuzzed inputs using `fast-check` (TypeScript) or `hypothesis` (Python).
- **Live Agent Evaluation:** Trajectory fidelity and tool selection evaluated using `agents-cli eval run` ($\ge 95\%$ tool selection precision, 1.000 groundedness).
- **RCA Protocol on Failure:** Zero quick-patches or mockups; execute the 4-step RCA protocol.

---

## 🛠️ Integrated Skills & Capabilities

- **`ai-sdlc`:** Master 3-Phase AI-SDLC orchestrator guiding developers through Inception, SDD Execution, and Operation with automatic `specs/` & `docs/` workspace scaffolding (`--init`), proactive clarification questions (`ask_question`), and phase gate validation (`validate_sdlc_gate.py`).
- **`codemender`:** Pre-build SAST orchestration discovering vulnerabilities (`cm find`), generating PoC exploit verification (`cm verify`), and producing remediated code diffs (`cm fix`).
- **`gcp_cost_estimator`:** Enterprise cloud cost modeling querying real-time unit pricing strictly from the live Google Cloud Billing API (zero local caching) and calculating itemized BoMs with CUD savings.
- **`architecture_diagram`:** Generates professional, dark-themed technical system diagrams with interactive SVG/HTML companion visualizers.

---

## 📖 Key References
- **Operating Manual:** [`AGENTS.md`](./AGENTS.md)
- **AI-SDLC, SDD & RCA Rule:** [`_agents/rules/ai_sdlc_and_sdd_standards.md`](./_agents/rules/ai_sdlc_and_sdd_standards.md)
- **AI-SDLC Skill:** [`_agents/skills/ai_sdlc/SKILL.md`](./_agents/skills/ai_sdlc/SKILL.md)
- **Specification Registry Template:** [`_agents/skills/ai_sdlc/examples/specs/README.md`](./_agents/skills/ai_sdlc/examples/specs/README.md)
- **Master SDD Template:** [`_agents/skills/ai_sdlc/examples/specs/templates/sdd-template.md`](./_agents/skills/ai_sdlc/examples/specs/templates/sdd-template.md)
- **Operational Reports Template:** [`_agents/skills/ai_sdlc/examples/docs/README.md`](./_agents/skills/ai_sdlc/examples/docs/README.md)
- **Rules Catalog:** [`_agents/rules/README.md`](./_agents/rules/README.md)
- **Skills Catalog:** [`_agents/skills/README.md`](./_agents/skills/README.md)

