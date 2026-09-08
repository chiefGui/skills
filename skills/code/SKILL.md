---
name: code
description: Code design practices.
---

# Code

- Prefer the simplest design that satisfies known requirements.
- Resolve competing principles in favor of correctness and understandability.

## Design

- Keep related logic and knowledge together.
- Keep dependencies explicit.
- Prefer simple interfaces that hide substantial implementation complexity. (Deep Modules)
- Encapsulate decisions so callers do not need to understand or repeat them.
- Avoid splitting modules when doing so exposes details or increases coordination.
- Prefer existing capabilities over parallel implementations.
- Introduce abstractions when they simplify the current implementation
  or isolate a concrete source of variation.
- Allow similar code to remain separate when it represents different
  rules or reasons to change.
- Eliminate abstractions whose removal reduces complexity.
- Retain abstractions that prevent complexity from spreading into callers.
- Minimize the knowledge and coordination required from callers.
- Optimize for understandable code and localized changes.

## Extensibility

- Prefer composition.
- Accept replaceable dependencies.
- Remove unnecessary coupling that blocks extension.
- When adding a variant of an existing capability, prefer extending through its contract over adding concrete-type branches to consumers.
- Introduce or adjust the contract when it represents a coherent capability; do not preserve an abstraction that no longer fits.
- Keep core rules independent of integration details where those details would otherwise spread.
- Centralize wiring when multiple implementations need selection.
- Require every interface, factory, and layer to provide a concrete capability needed by the task.

## Implementation

- Represent each fact once; derive values instead of duplicating state.
- Make invalid states difficult to represent.
- Validate at boundaries; rely on enforced contracts internally.
- Handle failures explicitly; do not disguise them as successful results.
- Add dependencies only when their benefit justifies their cost.
- Explain non-obvious constraints and decisions in comments.
- Avoid compatibility paths unless compatibility is required.