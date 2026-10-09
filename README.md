# tiramitree

![Research engineering: experiment recovery, checkpoint verification, and evaluation.](./assets/profile-banner.svg)

I build research tools for reproducible evaluation, experiment recovery, and training-state verification.

## Selected projects

### [BenchHandoff](https://github.com/tiramitree/benchhandoff) · Experiment recovery

Verify declared inputs and completed outputs before resuming an interrupted experiment batch. A local Python CLI, with an optional early Kubernetes controller.

`Python` · `Go` · `Kubernetes`

[BenchHandoff examples](https://github.com/tiramitree/benchhandoff/tree/main/examples) · [BenchHandoff checks](https://github.com/tiramitree/benchhandoff/actions)

### [DCPInvariant](https://github.com/tiramitree/dcp-invariant) · Training-state verification

Check that checkpoint restoration preserves model state, optimizer state, data progress, and the next training step. The documented scenarios use single-host CPU execution.

`Python` · `PyTorch` · `Distributed Checkpoint`

[DCPInvariant source](https://github.com/tiramitree/dcp-invariant/tree/main/src/dcp_invariant) · [DCPInvariant checks](https://github.com/tiramitree/dcp-invariant/actions)

## Additional work

- **[EvalFence](https://github.com/tiramitree/evalfence)** — a Rust CLI for checking evaluation metrics, duplicate records, and declared agent inputs.
- **[EffectWitness](https://github.com/tiramitree/effect-witness)** — compares client observations with durable tool effects when a response is lost.
- **[CacheInvariant](https://github.com/tiramitree/cache-invariant)** — checks inference-cache behavior against a pinned CPU fixture.

The project READMEs document the supported scenarios, runtime, and runnable checks.
