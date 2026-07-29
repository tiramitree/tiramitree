# tiramitree

I build auditable AI systems and research-engineering infrastructure:
agent-benchmark metric, manifest, provenance, and custom-agent boundary
auditing; agent/tool-effect evaluation; distributed-checkpoint restart
invariants; and fail-closed recovery.

My three representative owned projects are BenchHandoff, EvalFence, and
DCPInvariant; EffectWitness and CacheInvariant are additional bounded evidence.
Claims are tied to source revisions, public CI, releases, or committed
normalized evidence. Maintainer-operated tests, independent review, external
use, and production validation are different kinds of evidence.

## Current focus

- agent-benchmark metric, manifest-integrity, boundary, and reproducibility contracts
- agent harnesses and tool-effect semantics under ambiguous failures
- single-host distributed-checkpoint process-count restart invariants
- experiment recovery and process-lifecycle invariants
- version-pinned inference-cache correctness
- Go, Rust, and Python; Kubernetes, cross-platform CI, fault injection, and
  systems testing

## EvalFence

[Repository](https://github.com/tiramitree/evalfence) |
[v0.3.0 source-only release](https://github.com/tiramitree/evalfence/releases/tag/v0.3.0) |
[main CI](https://github.com/tiramitree/evalfence/actions/runs/30401556015) |
[main SWE-bench control](https://github.com/tiramitree/evalfence/actions/runs/30401556000) |
[main STATE-Bench control](https://github.com/tiramitree/evalfence/actions/runs/30401556102) |
[tag CI](https://github.com/tiramitree/evalfence/actions/runs/30401692397) |
[tag SWE-bench control](https://github.com/tiramitree/evalfence/actions/runs/30401692383) |
[tag STATE-Bench control](https://github.com/tiramitree/evalfence/actions/runs/30401692378)

EvalFence is an Apache-2.0 Rust CLI with three independent fail-closed
contracts for agent-benchmark evidence. The interval/metric lane checks
explicit prediction and gold declarations, prediction-source allowlists,
interval and count consistency, and supplied precision, recall, and F1
formulas. The keyed-manifest lane checks exact IDs and payload-digest syntax,
duplicate and conflicting records, coverage, declared counts, and
order-dependent last-write-wins collapse before records become a map. The
custom-agent boundary lane checks declared input classes and allowlists,
mutable aliases, exposed read/write capability groups, callable and mediated
counts, and custom-agent construction versus baseline-snapshot order.

The annotated v0.3.0 tag resolves to
[`de3c49e6a6960fbafea59381a69439558a239e0e`](https://github.com/tiramitree/evalfence/commit/de3c49e6a6960fbafea59381a69439558a239e0e).
At that commit, main and tag validation each passed six public jobs across the
CI and two independent control workflows: Rust formatting and Clippy, Linux,
Windows, and macOS tests, a release build, all three source-bound case studies,
and generated-evidence privacy gates. The Release has no attached binaries or
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

The STATE-Bench control is pinned to
[`4efcbf2d4fe60df04878859b692d9391f3d5b33a`](https://github.com/microsoft/STATE-Bench/commit/4efcbf2d4fe60df04878859b692d9391f3d5b33a).
Exact source and AST guards plus an offline runtime probe cover one public test
task in each registered domain. The declared custom-agent boundary receives 14
state-requirement items, nine task-requirement items, and 20 callable write
handlers. A bounded shopping control reaches deterministic state score `1`
with two harness-executed tool calls; removing only `state_requirements`
produces score `0`, no calls or errors, and an empty state diff. This is not a
protocol-compliant or official score.

EvalFence validates declared adapter inputs and frozen source/runtime
relationships, not arbitrary upstream data flow or physical isolation. Input
and oracle classes remain adapter declarations. These controls do not establish
that a submitted agent used the declared fields or callables, that a real
prediction file contains duplicates, that a published score changed, or that
an upstream is defective or nonconforming. Removing one context field does not
isolate arbitrary same-process Python; filesystem access, task-ID lookup, and
other same-process hooks remain outside the control. The project is not a
model- or harness-quality benchmark, sandbox, production validation,
independent review, external use, adoption, endorsement, or recruiting signal.

## DCPInvariant

[Repository](https://github.com/tiramitree/dcp-invariant) |
[v0.4.0 release](https://github.com/tiramitree/dcp-invariant/releases/tag/v0.4.0) |
[public tag CI](https://github.com/tiramitree/dcp-invariant/actions/runs/30431967133)

DCPInvariant is an Apache-2.0, CPU-only evidence harness for exact restart
and generation-lineage invariants around PyTorch Distributed Checkpoint. Its
fixed fixture checks model parameters, SGD momentum, an explicit generator
state, and a data cursor at the checkpoint and after the next registered
training step.

The normalized schema-v4 evidence passes thirteen single-host CPU/Gloo
scenarios: four DDP restart topologies, two DTensor global-tensor restore
topologies, one fixed real two-worker `torch.distributed.run` restart, one
fixed two-rank asynchronous snapshot witness using
`torchvision.models.resnet18(weights=None)`, synthetic input, and public
writer gates. The loaded candidate matches the staged pre-mutation state and
differs from the post-mutation state before receipt-bound promotion. Four
fault cases still fail closed.

The added generation-lineage scenario commits two immutable children from the
same selected parent. Under one registered local interleaving, conditional
publication selects the first child and rejects the second as `stale_parent`
without deleting either committed generation. It also checks one exit after
commit and one exit after verified publication and lock release. This is a
cooperating-process, ordinary-local-filesystem witness, not distributed
compare-and-swap, hostile-writer containment, network-filesystem correctness,
or power-loss durability.

The exact compatibility contract binds PyTorch 2.11, torchvision 0.26,
Pillow 12.3, and NumPy 2.4.6. It does not infer an operating system or
general TorchElastic compatibility. Schema v4 has 30 ordinary files; the
preserved v0.1.0 through v0.3.0 releases remain the verifiers for their
historical schemas.

The annotated tag targets
[`7bb325704d196ebbfcbc5a9dd5fab0d5acd76fc4`](https://github.com/tiramitree/dcp-invariant/commit/7bb325704d196ebbfcbc5a9dd5fab0d5acd76fc4).
Candidate, main, and tag CI each passed six integration jobs, six quality
jobs, and one package-boundary job across Windows and Ubuntu with CPython
3.11-3.13. The Release contains a wheel, source distribution, normalized
evidence archive, and checksum file; all four passed GitHub-digest and fresh-
download hash parity. The wheel verifies the evidence offline without
PyTorch, torchvision, Pillow, or NumPy installed.

These results are fixture-, version-, topology-, failure-point-, and
source-bound. They do not establish arbitrary TorchElastic recovery, elastic
membership, multi-node, GPU/NCCL, FSDP, arbitrary-model snapshot semantics,
performance, production reliability, hostile-checkpoint safety, independent
review, external use, adoption, endorsement, or recruiting outcomes.

## Additional bounded evidence: EffectWitness

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

## BenchHandoff

[Repository](https://github.com/tiramitree/benchhandoff) |
[v0.4.0 release](https://github.com/tiramitree/benchhandoff/releases/tag/v0.4.0) |
[main CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml) |
[main AgentRun kind E2E](https://github.com/tiramitree/benchhandoff/actions/workflows/agentrun-kind.yml) |
[tag CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml) |
[tag AgentRun kind E2E](https://github.com/tiramitree/benchhandoff/actions/workflows/agentrun-kind.yml)

BenchHandoff is an Apache-2.0 local CLI for fail-closed, resumable sequential
experiment batches. It fingerprints suites and declared inputs, preserves
failed attempts, verifies completed outputs before skipping them, and binds an
approved resume to the exact evidence reviewed before mutation.

Version `v0.4.0` retains the strict suite schema v3 workspace contract and
adds an optional early-alpha Kubernetes `AgentRun` controller. An immutable
execution specification binds an existing PVC, normalized suite path and
SHA-256, digest-pinned runner image, and bounded deadline.

The controller creates one deterministic start, resume, or verify Job at a
time. A failed start enters `AwaitingApproval`; only the exact write-once
approval digest permits resume, followed by fresh bundle verification. It
also binds the owner UID, execution-spec hash, Job template, live Job UID, and
one owned Pod, and fails closed on registered digest, approval, ownership,
template, Pod-cardinality, and result mismatches.

The annotated tag resolves to
[`c893f635076b57dfc830539ae5e17bb05b368813`](https://github.com/tiramitree/benchhandoff/commit/c893f635076b57dfc830539ae5e17bb05b368813).
Main and annotated-tag CI each passed all ten jobs across Ubuntu 24.04 and
Windows Server 2025 with CPython 3.11-3.14, canonical synthetic evidence, and
one inspected and installed distribution build. Separate main and tag
AgentRun workflows passed the pinned real-kind gate with Go 1.26.5, kind
v0.32.0, and Kubernetes/kubectl v1.36.1 on one manager and one node.

The registered gate covers deliberate failure, exact approval, resume, fresh
verification, manager restart/adoption, declared suite-digest mismatch, wrong
approval, duplicate-Pod rejection, and bounded cleanup. The Release contains
only the CI-built Python wheel, source distribution, and checksum file. The Go
manager, CRD, and reference manifests remain source-only; no controller image,
Helm chart, production installer, or compatibility matrix is published.

The reference E2E manifest uses a cluster-wide role and binding and requires
deployment-specific review and narrowing. These owner-operated synthetic
checks do not establish high availability, exactly-once execution, workload
isolation, arbitrary Kubernetes compatibility, performance, production
reliability, independent reproduction or review, external use, or adoption.

## Engineering principles

- make the protocol and failure boundary inspectable before optimizing;
- preserve failed runs as evidence rather than rewriting the story;
- distinguish tested, simulated, and production behavior;
- prefer a small number of deep, owned projects over disconnected demos.

OpenAI Codex materially assisted implementation, testing, documentation, and
publication workflows. Human identity, legal commitments, independent review,
and external-adoption claims remain human-only.
