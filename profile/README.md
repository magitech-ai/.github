# Magitech AI

Magitech AI builds high-assurance, event-driven agent infrastructure and runtime substrates for autonomous systems.

## Architecture & Ecosystem

```mermaid
graph TD
    classDef core fill:#2d3748,stroke:#4a5568,stroke-width:2px,color:#fff;
    classDef harness fill:#1a365d,stroke:#2b6cb0,stroke-width:2px,color:#fff;
    classDef plugins fill:#1c4532,stroke:#2f855a,stroke-width:2px,color:#fff;

    subgraph Core ["anima (Micro-Kernel)"]
        A1[Event Waterfalls]:::core
        A2[Hierarchical Contexts & DI]:::core
        A3[Dynamic Plugin Lifecycle]:::core
    end

    subgraph Harness ["magitech-harness (Agent Turn Engine)"]
        H1[Agent Turn Loop]:::harness
        H2[Append-Only Session Event Log]:::harness
        H3[Tool-Pairing Integrity & Compaction]:::harness
        H4[Cooperative Cancellation]:::harness
    end

    subgraph Plugins ["mth-plugins (Extensible Marketplace)"]
        P1[Model Providers: OpenRouter, Pollinations]:::plugins
        P2[Domain Tools: fs, bash]:::plugins
        P3[Guardrails: Compaction, Truncation]:::plugins
    end

    Core --> Harness
    Plugins -.->|Registered into| Harness
```

### Repositories

- **[`anima`](https://github.com/magitech-ai/anima)**: Foundational asynchronous micro-kernel and event pipeline engine providing waterfall interceptors, context propagation, and effect disposers.
- **[`magitech-harness`](https://github.com/magitech-ai/magitech-harness)**: Composable host runtime substrate and agent turn engine. Contains zero built-in domain tools and zero built-in model providers.
- **[`mth-plugins`](https://github.com/magitech-ai/mth-plugins)**: Official portable plugins and marketplace catalog providing pluggable model providers, domain tools, and compaction guardrails.

---

## Core Invariants

1. **Capability Seam Symmetry**: Every extensible feature consists of a **Service Definition** (protocol), **Service Provider** (plugin implementation), and **Consumer** (turn loop or REPL).
2. **Session Event-Sourcing**: Model-visible data is strictly isomorphic to logged events. Raw session logs are immutable and append-only. Compaction folds historical context while preserving the full event trace.
3. **Tool-Pairing Integrity**: Turn cuts and compaction boundaries never sever an assistant tool call from its matching tool result.
4. **Registrations are Effects**: Every contribution returns an explicit disposer closure; teardown cleanly unwinds without side effects.
5. **Fail-Loud Configuration**: Misconfiguration fails loud at initialization rather than silently falling back or skipping referents.
6. **Strict Quality Gates**: Every package enforces strict `mypy` static typing (`disallow_untyped_defs = true`), formatting with `ruff`, and a mandatory 100% statement and branch coverage floor (`pytest --cov-fail-under=100`).

---

## Issue Tracking & Triage

All repositories in `@magitech-ai` use GitHub Issues and the `gh` CLI with a canonical five-role triage vocabulary:

| Label | Meaning |
| :--- | :--- |
| `needs-triage` | Maintainer needs to evaluate this issue |
| `needs-info` | Waiting on reporter for more information |
| `ready-for-agent` | Fully specified, ready for autonomous agent execution |
| `ready-for-human` | Requires human implementation or review |
| `wontfix` | Out of scope or will not be actioned |