---
name: principle-outcome-oriented-execution
description: "Apply during planned rewrites and migrations with explicit phase boundaries. Converge on the target architecture; don't preserve smooth intermediate states with throwaway compatibility code, and don't keep legacy APIs alive for callers you could just migrate."
disable-model-invocation: true
---

# Outcome-Oriented Execution

Optimize for the intended, verifiable end state rather than preserving smooth intermediate states. Use this during planned rewrites and migrations with explicit phase boundaries.

**Why:** Keeping every intermediate step fully stable often creates temporary compatibility code that becomes long-lived debt. Converge on the target architecture and prove correctness at explicit verification boundaries.

**Core rule:**
- Prioritize end-state integrity over transitional stability
- Intermediate breakage is acceptable when it is planned, scoped, and reversible
- Always run final verification before declaring done

**Example: legacy API migrations.** When a new internal API is the right design and old callers still exist, migrate the callers and delete the old API in the same refactor wave instead of preserving a compatibility layer:
- Do not keep legacy API paths alive only because internal callers still exist
- Inventory callers, migrate them, and delete the old API immediately
- Treat temporary adapters as exceptional and time-boxed, not default architecture
- Update tests to assert the new contract, and delete tests that only protect pre-refactor implementation details

This applies when no external users depend on backward compatibility, the project can absorb coordinated breaking changes, and the new API is part of a simplification or refactor initiative. Keeping both old and new APIs creates dual-path complexity, slows cleanup, and makes the codebase feel append-only.

**Guardrails:**
- Declare where temporary breakage is acceptable
- Keep high-signal checks for actively touched areas while migrating
- Require full static and runtime verification at plan completion
- Intermediate breakage means the phase-boundary level, not skipping per-unit verification within a phase. See **principle-sequence-verifiable-units** for the discipline that still applies inside each phase.
