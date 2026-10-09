# tiramitree

I build research tools for reproducible evaluation, experiment recovery, and training-state verification.

## Selected projects

| Project | What it does | Explore |
|---|---|---|
| **[BenchHandoff](https://github.com/tiramitree/benchhandoff)** | Verifies inputs and completed outputs before resuming an interrupted experiment batch. Includes a Python CLI and an optional Go/Kubernetes controller. | [Examples](https://github.com/tiramitree/benchhandoff/tree/main/examples) · [Tests and CI](https://github.com/tiramitree/benchhandoff/actions) |
| **[DCPInvariant](https://github.com/tiramitree/dcp-invariant)** | Checks whether checkpoint restoration preserves model state, optimizer state, data progress, and the next training step in fixed single-host CPU scenarios. | [Source](https://github.com/tiramitree/dcp-invariant/tree/main/src/dcp_invariant) · [Tests and CI](https://github.com/tiramitree/dcp-invariant/actions) |

## Additional work

- **[EvalFence](https://github.com/tiramitree/evalfence)** — a Rust CLI for checking evaluation metrics, duplicate records, and declared agent inputs.
- **[EffectWitness](https://github.com/tiramitree/effect-witness)** — compares client observations with durable tool effects when a response is lost.
- **[CacheInvariant](https://github.com/tiramitree/cache-invariant)** — checks inference-cache behavior against a pinned CPU fixture.

Each repository includes its supported scenarios, runnable checks, and validation evidence.
