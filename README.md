# tiramitree

![Selected projects and a publication: source, experiments, and verification.](./assets/profile-banner.svg)

## Publication

**[Bayesian Optimization of Lasso and XGBoost Models for Comparative Analysis in Housing Price Prediction](https://doi.org/10.1051/itmconf/20257303005)**  
*ITM Web of Conferences* **73**, 03005 (2025) · IWADI 2024.

## Selected projects

### [BenchHandoff](https://github.com/tiramitree/benchhandoff) · Experiment recovery

Verify declared inputs and completed outputs before resuming an interrupted experiment batch. Records hashes and logs, rechecks completed outputs, and rejects changed evidence before an approval-bound retry.

`Python` · `Go` · `Kubernetes`

[BenchHandoff examples](https://github.com/tiramitree/benchhandoff/tree/main/examples) · [BenchHandoff checks](https://github.com/tiramitree/benchhandoff/actions)

### [DCPInvariant](https://github.com/tiramitree/dcp-invariant) · Checkpoint verification

Check PyTorch checkpoint restoration with fixed single-host CPU scenarios. Covers training-state restoration, process-count changes, asynchronous snapshots, stale publishers, and damaged checkpoint files.

`Python` · `PyTorch` · `Distributed Checkpoint`

[DCPInvariant scenarios](https://github.com/tiramitree/dcp-invariant#what-the-suite-proves) · [DCPInvariant source](https://github.com/tiramitree/dcp-invariant/tree/main/src/dcp_invariant) · [DCPInvariant checks](https://github.com/tiramitree/dcp-invariant/actions)

## Additional projects

- **[EvalFence](https://github.com/tiramitree/evalfence)** — a Rust CLI for checking evaluation metrics, duplicate records, and declared agent inputs.
- **[EffectWitness](https://github.com/tiramitree/effect-witness)** — compares client observations with durable tool effects when a response is lost.
- **[CacheInvariant](https://github.com/tiramitree/cache-invariant)** — checks inference-cache behavior against a pinned CPU fixture.

The project READMEs document the supported scenarios, runtime, and runnable checks.
