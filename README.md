# tiramitree

I build auditable AI systems and research-engineering infrastructure:
agent-benchmark metric, provenance, and keyed-manifest auditing,
agent/tool-effect evaluation, distributed-checkpoint restart invariants, and
fail-closed recovery.

My three representative owned projects are EvalFence, EffectWitness, and
DCPInvariant; BenchHandoff and CacheInvariant are additional bounded evidence.
Claims are tied to source revisions, public CI, releases, or committed
normalized evidence. Maintainer-operated tests, independent review, external
use, and production validation are different kinds of evidence.

## Current focus

- agent-benchmark metric, manifest-integrity, and reproducibility contracts
- agent harnesses and tool-effect semantics under ambiguous failures
- single-host distributed-checkpoint process-count restart invariants
- experiment recovery and process-lifecycle invariants
- version-pinned inference-cache correctness
- Rust and Python, cross-platform CI, fault injection, and systems testing

## EvalFence

[Repository](https://github.com/tiramitree/evalfence) |
[v0.2.0 source-only release](https://github.com/tiramitree/evalfence/releases/tag/v0.2.0) |
[main CI](https://github.com/tiramitree/evalfence/actions/runs/30355886136) |
[main SWE-bench control](https://github.com/tiramitree/evalfence/actions/runs/30355885891) |
[tag CI](https://github.com/tiramitree/evalfence/actions/runs/30356013022) |
[tag SWE-bench control](https://github.com/tiramitree/evalfence/actions/runs/30356011144)

EvalFence is an Apache-2.0 Rust CLI with two independent fail-closed contracts
for agent-benchmark evidence. The interval and metric lane checks explicit
prediction and gold declarations, prediction-source allowlists, interval and
count consistency, and supplied precision, recall, and F1 formulas. The
keyed-manifest lane checks exact IDs and payload-digest syntax, duplicate and
conflicting records, allowlisted and required coverage, declared counts, and
order-dependent last-write-wins collapse before records become a map.

The annotated v0.2.0 tag resolves to
[`ebb91ec8eaf5e0c7a494e36491cf20985bb551aa`](https://github.com/tiramitree/evalfence/commit/ebb91ec8eaf5e0c7a494e36491cf20985bb551aa).
At that commit, main and tag validation each passed five public jobs across the
CI and SWE-bench-control workflows: Rust formatting and Clippy, Linux,
Windows, and macOS tests, a release build, both source-bound case studies, and
generated-evidence privacy gates. The Release has no attached binaries or
other uploaded assets and contains only GitHub-generated source archives.

The ContextBench control remains hash-pinned to one exact upstream revision.
It simulates an absent-`model_patch` path over 500 public rows, materializes
421 nonempty fallback cases, and records the bounded per-instance formula
observations without claiming aggregate or leaderboard impact.

The separate SWE-bench control is pinned to
[`f7bbbb2ccdf479001d6467c9e34af59e44a840f9`](https://github.com/SWE-bench/SWE-bench/commit/f7bbbb2ccdf479001d6467c9e34af59e44a840f9).
It verifies exact public file hashes, prediction-key constants, and registered
loader and consumer AST shapes. Reversing two synthetic same-ID records with
different payload digests changes the simulated last-write-wins survivor while
retaining the registered duplicate, conflict, and order-dependence findings.
Generated findings and witnesses use group ordinals instead of serializing
manifest record or policy IDs; caller-controlled `case_id` is still copied to
the report and requires its own privacy review.

EvalFence validates declared adapter inputs and frozen source relationships,
not arbitrary upstream data flow or adapter-selected payload bytes. The
controls do not establish that a real prediction file contains duplicates,
that a published score changed, or that either upstream is defective or
nonconforming. They are not model- or harness-quality benchmarks, sandboxes,
production validation, independent review, external use, adoption,
endorsement, or recruiting signals.

## DCPInvariant

[Repository](https://github.com/tiramitree/dcp-invariant) |
[v0.3.0 release](https://github.com/tiramitree/dcp-invariant/releases/tag/v0.3.0) |
[public tag CI](https://github.com/tiramitree/dcp-invariant/actions/runs/30391057534)

DCPInvariant is an Apache-2.0, CPU-only evidence harness for exact restart
invariants around PyTorch Distributed Checkpoint. Its fixed fixture checks
model parameters, SGD momentum, an explicit generator state, and a data cursor
at the checkpoint and after the next registered training step.

The normalized schema-v3 evidence passes twelve single-host CPU/Gloo
scenarios: four DDP restart topologies, two DTensor global-tensor restore
topologies, one fixed real two-worker `torch.distributed.run` restart, and
expected rejection of a rank exit without promotion, missing metadata,
missing shard, and one-byte shard corruption. It adds one fixed two-rank
asynchronous snapshot witness using
`torchvision.models.resnet18(weights=None)`, synthetic input, and public
writer gates. The loaded candidate matches the staged pre-mutation state and
differs from the post-mutation state before receipt-bound promotion.

The exact compatibility contract binds PyTorch 2.11, torchvision 0.26,
Pillow 12.3, and NumPy 2.4.6. It does not infer an operating system or
general TorchElastic compatibility. Schema v3 has 28 ordinary files; the
preserved v0.1.0 and v0.2.0 releases remain the verifiers for their historical
schemas.

The annotated tag targets
[`c82a3d57719f2fcba8d39ec7e52d842e9e871f1b`](https://github.com/tiramitree/dcp-invariant/commit/c82a3d57719f2fcba8d39ec7e52d842e9e871f1b).
Candidate, main, and tag CI each passed six integration jobs, six quality
jobs, and one package-boundary job across Windows and Ubuntu with CPython
3.11-3.13. The Release contains a wheel, source distribution, normalized
evidence archive, and checksum file; all four passed GitHub-digest and public-
download hash parity. The wheel verifies the evidence offline without
PyTorch, torchvision, Pillow, or NumPy installed.

These results are fixture-, version-, topology-, failure-point-, and
source-bound. They do not establish arbitrary TorchElastic recovery, elastic
membership, multi-node, GPU/NCCL, FSDP, arbitrary-model snapshot semantics,
performance, production-reliability, hostile-checkpoint, independent-review,
external-use, or adoption claims.

## EffectWitness

[Repository](https://github.com/tiramitree/effect-witness) |
[v0.4.0 pre-release](https://github.com/tiramitree/effect-witness/releases/tag/v0.4.0) |
[public tag CI](https://github.com/tiramitree/effect-witness/actions/runs/30320989049)

EffectWitness is an Apache-2.0 workbench for comparing declared MCP tool
effect hints, client observations, and durable effects under ambiguous
failures. It records declaration, observation, decision, and effect facts
separately instead of treating a successful-looking response as proof of an
external effect.

Version `v0.4.0` adds a separate schema-v5 lane using mini-swe-agent 2.4.6
against one fixed synthetic Git patch. Four registered scenarios run for three
rounds each: clean execution, an application-level first trajectory-save
fault followed by blind restart, journal-based reconciliation, and a tampered
reconciliation control that must fail closed. The evidence binds registered
pre/post byte-tree hashes, the patch, command result, journal transitions, and
the durable effect without publishing raw trajectories, workspaces, commands,
paths, environment values, process identifiers, or timestamps.

The bundled Windows reference contains eight files, 21 completed worker
records, and 15 registered command executions. An independent offline verifier
recomputes the schema-v5 relationships without importing or running
mini-swe-agent. The release retains the exact version-pinned official
filesystem, synthetic schema-v2, and LangGraph replay lanes. Public main and
tag CI each passed all 13 jobs across Windows, Ubuntu, and Python 3.11-3.13.
No model API or paid service is used.

The lightweight tag resolves to
[`a6ca1c447752df90f72e200eb4536a1976186d5a`](https://github.com/tiramitree/effect-witness/commit/a6ca1c447752df90f72e200eb4536a1976186d5a).
The release contains only a wheel and source distribution. The wheel excludes
`integrations/` metadata and Node/npm/runtime payloads; the source distribution
adds only the exact manifests, locks, constraints, and provenance metadata
needed to prepare and verify external dependencies, not the dependencies or
runtimes themselves.

The observations are source-, version-, input-, and OS-bound. They do not
establish native mini-swe-agent resume, hard-machine-crash recovery,
exactly-once execution, arbitrary patch or command correctness, coding-agent
or model quality, benchmark performance, sandboxing, arbitrary LangGraph or
MCP correctness, package-wide correctness, official conformance, SQLite crash
consistency, security, production reliability, independent review, external
use, or adoption.

## Additional bounded evidence: CacheInvariant

[Repository](https://github.com/tiramitree/cache-invariant) |
[v0.3.0 pre-release](https://github.com/tiramitree/cache-invariant/releases/tag/v0.3.0) |
[public main CI](https://github.com/tiramitree/cache-invariant/actions/runs/30293701488) |
[public tag CI](https://github.com/tiramitree/cache-invariant/actions/runs/30293833809)

CacheInvariant is an Apache-2.0 lab for exact-version inference-cache
correctness. Its v0.3.0 reference records 77/77 registered invariants for a
pinned `llama.cpp b10107` CPU fixture, including direct-token exact replay,
shared-prefix reuse, first-token divergence controls, restart, cancellation,
and reuse. Public main and tag CI each passed all nine jobs on Windows and
Ubuntu.

The runtime and model fixture are not redistributed. The observations are
bounded server counters, not model-quality, generated-output, performance,
production, cross-runtime, independent-review, external-use, or adoption
evidence.

## Additional bounded evidence: BenchHandoff

[Repository](https://github.com/tiramitree/benchhandoff) |
[v0.3.0 release](https://github.com/tiramitree/benchhandoff/releases/tag/v0.3.0) |
[release-commit CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml) |
[tag CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml)

BenchHandoff is an Apache-2.0 local CLI for fail-closed, resumable sequential
experiment batches. It fingerprints suites and declared inputs, preserves
failed attempts, verifies completed outputs before skipping them, and binds an
approved resume to the exact evidence reviewed before mutation.

Version `v0.3.0` adds opt-in suite schema v3 for one dedicated, reviewed
workspace. It binds bounded directory topology and ordinary-file
primary-stream bytes at preflight, launch, post-exit, recovery, bundle, and
verification checkpoints; rejects linked, reparse, hard-linked, cross-device,
aliased, unstable, and unsupported entries; and preserves version 1 and
version 2 compatibility.

The annotated tag resolves to
[`e85c565a6600d92c1a929109d02d477682375b31`](https://github.com/tiramitree/benchhandoff/commit/e85c565a6600d92c1a929109d02d477682375b31).
Both the release-commit and tag runs passed all ten jobs. Each of the eight
Ubuntu 24.04 and Windows Server 2025 jobs across CPython 3.11-3.14 ran 211
tests with no failures, errors, or skips; the dependent jobs verified the
canonical synthetic evidence and built, inspected, installed, and smoke-tested
the exact distribution.

The Release contains the exact CI-built wheel, source distribution, and
checksum file. Workspace checks are discrete observations, not continuous
monitoring, a sandbox, or a hostile-writer boundary; they do not bind mode,
ownership, timestamps, ACLs, extended attributes, NTFS alternate data streams,
sparse layout, or unlisted metadata. These are maintainer-operated synthetic
checks, not production reliability, independent reproduction or review,
external use, or adoption.

## Engineering principles

- make the protocol and failure boundary inspectable before optimizing;
- preserve failed runs as evidence rather than rewriting the story;
- distinguish tested, simulated, and production behavior;
- prefer a small number of deep, owned projects over disconnected demos.

OpenAI Codex materially assisted implementation, testing, documentation, and
publication workflows. Human identity, legal commitments, independent review,
and external-adoption claims remain human-only.
