# tiramitree

I build auditable AI systems and research-engineering infrastructure:
agent-benchmark metric and provenance auditing, agent/tool-effect evaluation,
distributed-checkpoint restart invariants, and fail-closed recovery.

My three representative owned projects are EvalFence, EffectWitness, and
DCPInvariant; BenchHandoff and CacheInvariant are additional bounded evidence.
Claims are tied to source revisions, public CI, releases, or committed
normalized evidence. Maintainer-operated tests, independent review, external
use, and production validation are different kinds of evidence.

## Current focus

- agent-benchmark metric, provenance, and reproducibility contracts
- agent harnesses and tool-effect semantics under ambiguous failures
- single-host distributed-checkpoint process-count restart invariants
- experiment recovery and process-lifecycle invariants
- version-pinned inference-cache correctness
- Rust and Python, cross-platform CI, fault injection, and systems testing

## EvalFence

[Repository](https://github.com/tiramitree/evalfence) |
[v0.1.0 source-only release](https://github.com/tiramitree/evalfence/releases/tag/v0.1.0) |
[main CI](https://github.com/tiramitree/evalfence/actions/runs/30348232629) |
[tag CI](https://github.com/tiramitree/evalfence/actions/runs/30348374895)

EvalFence is an Apache-2.0 Rust CLI for auditing adapter-declared metric and
evidence-provenance contracts in agent benchmarks. It checks explicit
prediction and gold declarations, prediction-source allowlists, interval and
count consistency, and supplied precision, recall, and F1 formulas.

The annotated v0.1.0 tag resolves to
[`50e221bb011f8ad69b2ed820958a9d4def2b36e0`](https://github.com/tiramitree/evalfence/commit/50e221bb011f8ad69b2ed820958a9d4def2b36e0).
At that commit, main and tag CI each passed four jobs covering Rust quality,
Windows, macOS, and the pinned ContextBench case study. The Release has no
attached binaries or other assets and contains only GitHub-generated source
archives.

The hash-pinned case study simulates an absent-`model_patch` path over 500
public rows. It materializes 421 nonempty fallback cases; 410 have a
per-instance recall field that differs from standard set recall, including 380
whose record field is `1.0` while standard recall is below `1.0`. The separate
upstream aggregation path recomputes standard micro metrics.

EvalFence validates declared adapter inputs, not arbitrary upstream data flow.
The case study does not establish that a real submission omitted
`model_patch`, that aggregate or leaderboard results were affected, or that
the project has independent review, external users, adoption, endorsement, or
production use.

## DCPInvariant

[Repository](https://github.com/tiramitree/dcp-invariant) |
[v0.1.0 release](https://github.com/tiramitree/dcp-invariant/releases/tag/v0.1.0) |
[public CI](https://github.com/tiramitree/dcp-invariant/actions/runs/30314935055)

DCPInvariant is an Apache-2.0, CPU-only evidence harness for exact restart
invariants around PyTorch Distributed Checkpoint. Its fixed fixture checks
model parameters, SGD momentum, an explicit generator state, and a data cursor
at the checkpoint and after the next registered training step.

The normalized v0.1.0 evidence passes ten single-host CPU/Gloo scenarios:
DDP restart at 1-to-1, 1-to-2, 2-to-1, and 2-to-2 processes; DTensor
global-tensor restore at 1-to-2 and 2-to-1 processes; and expected rejection
of a child exit, missing metadata, missing shard, and one-byte shard
corruption. Checkpoints are sealed by ordinary-file inventories and SHA-256
receipts, promoted under the receipt digest, and reverified after load.

The lightweight tag resolves to
[`cad6b94ffe45e5a6821dba6b7a15920d3a40f283`](https://github.com/tiramitree/dcp-invariant/commit/cad6b94ffe45e5a6821dba6b7a15920d3a40f283).
Six live-integration and six quality jobs passed across Windows and Ubuntu
with CPython 3.11-3.13, and the Ubuntu package-boundary job also passed. The
Release contains a wheel, source distribution, normalized evidence archive,
and checksum file. The wheel can verify the evidence offline without PyTorch
or NumPy installed; the evidence archive contains no native checkpoint
payload.

These results are fixture-, version-, topology-, and source-bound. They do not
establish multi-node, GPU/NCCL, FSDP, arbitrary-model, performance,
production-reliability, hostile-checkpoint, independent-review, external-use,
or adoption claims.

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
