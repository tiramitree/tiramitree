# tiramitree

I build auditable AI systems and research-engineering infrastructure:
agent/tool effect evaluation, failure recovery, version-pinned inference
experiments, and reproducible control planes.

My public work is organized around a small number of owned projects. Claims
are tied to source revisions, public CI, release assets, or committed
normalized evidence. Local tests, public CI, independent reproduction,
external use, and production validation are different kinds of evidence.

## Current focus

- agent harnesses and tool-effect semantics under ambiguous failures
- inference-cache correctness and process-lifecycle invariants
- fail-closed recovery, provenance, and evidence integrity
- Python, Windows/Linux CI, fault injection, and systems-oriented testing

## EffectWitness

[Repository](https://github.com/tiramitree/effect-witness) |
[v0.3.3 pre-release](https://github.com/tiramitree/effect-witness/releases/tag/v0.3.3) |
[public tag CI](https://github.com/tiramitree/effect-witness/actions/runs/30277977090)

EffectWitness is an Apache-2.0 workbench for comparing declared MCP tool
effect hints, client observations, and durable effects under ambiguous
failures. It records declaration, observation, decision, and effect facts
separately instead of treating a successful-looking response as proof of an
external effect.

Version `v0.3.3` adds a LangGraph replay lane pinned to LangGraph 1.2.9,
checkpoint 4.1.1, SQLite checkpoint 3.1.0, sqlite-vec 0.1.9, MCP 1.28.1,
Node 24.18.0, and the official MCP filesystem server 2026.7.10. Four
registered scenarios run for ten rounds each across separate fault and resume
processes. The normalized artifact records 80 worker process facts and 60
mutating-call observations while excluding checkpoint databases, raw tool
arguments and responses, paths, environment values, process identifiers, and
timestamps. No model API or paid service is used.

The same release retains the exact version-pinned stdio lane for five
registered official-filesystem inputs and the synthetic schema-v2 controls
for false effect hints, ambiguous transport outcomes, reconciliation, and
eight-call concurrency. Producers fail closed instead of sealing a partial
artifact when any registered expectation is missed. Public tag CI passed all
11 jobs and separately generated and verified fresh Windows and Ubuntu
filesystem and LangGraph observations.

The lightweight tag resolves to
[`2a1e23df7bd9d1627ea06419053261e49e375d95`](https://github.com/tiramitree/effect-witness/commit/2a1e23df7bd9d1627ea06419053261e49e375d95).
The release contains only a wheel and source distribution. The wheel excludes
`integrations/` metadata and Node/npm/runtime payloads; the source distribution
adds only the exact manifests, locks, constraints, and provenance metadata
needed to prepare and verify external dependencies, not the dependencies or
runtimes themselves.

The observations are source-, version-, input-, and OS-bound. They do not
establish exactly-once execution, arbitrary LangGraph or MCP correctness,
package-wide correctness, official conformance, SQLite crash consistency,
security, performance, production reliability, independent review, external
use, or adoption.

## CacheInvariant

[Repository](https://github.com/tiramitree/cache-invariant) |
[v0.1.0 pre-release](https://github.com/tiramitree/cache-invariant/releases/tag/v0.1.0) |
[public tag CI](https://github.com/tiramitree/cache-invariant/actions/runs/30255550315)

CacheInvariant is an Apache-2.0 lab for version-pinned inference-cache
correctness and slot isolation. It exercises the exact `llama.cpp b10107` CPU
runtime with a tiny pinned fixture and records request registration, prompt
work, cancellation/reuse, state save/restore, and a full local process restart.

The committed Windows reference records 29/29 registered engineering
invariants as true and passes the bundled offline verifier. Public tag CI
separately runs the exact integration on Windows and Ubuntu, plus distribution
and Python 3.11-3.13 quality jobs. The lightweight tag resolves to
[`ab23512b8009de4895e911b4727666bb79d5b5e8`](https://github.com/tiramitree/cache-invariant/commit/ab23512b8009de4895e911b4727666bb79d5b5e8).

The release contains only the wheel and source distribution; it does not
redistribute the runtime, source fixture, or converted model. These controlled
observations do not establish model quality, useful generated text, latency,
throughput, security, production behavior, cross-runtime equivalence,
independent reproduction, external review, or adoption.

## BenchHandoff

[Repository](https://github.com/tiramitree/benchhandoff) |
[v0.1.0 release](https://github.com/tiramitree/benchhandoff/releases/tag/v0.1.0) |
[public tag CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml)

BenchHandoff is an Apache-2.0 local CLI for fail-closed, resumable sequential
experiment batches. It fingerprints suites and declared inputs, preserves
failed attempts, verifies completed outputs before skipping them, and binds an
approved resume to the exact evidence reviewed before mutation.

The recreated v0.1.0 tag resolves to
[`98e7a9e9227f39fee16b9d04c8f68ea89273a4fe`](https://github.com/tiramitree/benchhandoff/commit/98e7a9e9227f39fee16b9d04c8f68ea89273a4fe).
Its public tag CI passed ten jobs across Ubuntu and Windows. The deterministic
synthetic comparison records work-count and recovery behavior, not wall-clock
performance, distributed correctness, production readiness, security, model
quality, or external adoption.

## Engineering principles

- make the protocol and failure boundary inspectable before optimizing;
- preserve failed runs as evidence rather than rewriting the story;
- distinguish tested, simulated, and production behavior;
- prefer a small number of deep, owned projects over disconnected demos.

OpenAI Codex materially assisted implementation, testing, documentation, and
publication workflows. Human identity, legal commitments, independent review,
and external-adoption claims remain human-only.
