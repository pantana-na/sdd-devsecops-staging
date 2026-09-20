# Baseline Specifications (`specs/baseline/`)

This directory houses **Baseline Specifications** for existing (brownfield) code, reverse-engineered architecture, data contracts, and invariant models.

## Brownfield Baseline Mandate

Under the **Spec-Driven Development (SDD)** protocol ([`_agents/rules/spec_driven_development.md`](../../_agents/rules/spec_driven_development.md)):

1. **Baseline Before Delta:** Before modifying any existing subsystem, adding features to brownfield components, or executing refactorings, an accurate Baseline SDD reflecting the existing "as-is" code must be generated and stored here.
2. **What Must Be Captured:**
   - Subsystem boundaries and runtime assignments (Agent Platform vs Cloud Run)
   - Data models and schemas (TypeScript, Pydantic, SQL)
   - API endpoints, request/response formats, headers, and error codes
   - Business rules, invariants, and edge cases
   - External dependencies (Gemini API, Google Cloud services, external APIs)
3. **Core Invariant Protection:** Invariants documented in the baseline serve as the mathematical properties tested by Property-Based Tests (PBT) to ensure zero regressions during future development.

## Document Naming Convention
- `system-overview.md`: Comprehensive system architecture and data flow.
- `<subsystem>-baseline.md`: Subsystem-specific baseline specification (e.g. `auth-gateway-baseline.md`, `agent-orchestrator-baseline.md`).
