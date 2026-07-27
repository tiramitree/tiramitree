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
[v0.2.1 pre-release](https://github.com/tiramitree/effect-witness/releases/tag/v0.2.1) |
[public tag CI](https://github.com/tiramitree/effect-witness/actions/runs/30257552654)

EffectWitness is an Apache-2.0 workbench for comparing declared MCP tool
effect hints, client observations, and durable effects under ambiguous
failures. It records declaration, observation, decision, and effect facts
separately instead of treating a successful-looking response as proof of an
external effect.

Version `v0.2.1` carries the exact, version-pinned stdio lane introduced in
`v0.2.0` for the official MCP filesystem server. Five registered inputs are
each called twice and bracketed by fail-closed S0/S1/S2 relative byte-tree
observations. Separately, `v0.2.1` replaces the schema-v2 post-timeout fixed
wait with a successful transport-ready barrier. The committed Windows
reference contains normalized hashes, bounded facts, JUnit, provenance, and a
manifest; public tag CI separately generates and verifies fresh Windows and
Ubuntu observations.

The lightweight tag resolves to
[`e0e9ce9c8fc14ea15534905afd2b1e1b08cc5ac9`](https://github.com/tiramitree/effect-witness/commit/e0e9ce9c8fc14ea15534905afd2b1e1b08cc5ac9).
The wheel excludes `integrations/` metadata and Node/npm/runtime payloads. For
the external dependency, the source distribution adds only the exact package
manifest, lock, and provenance metadata needed to prepare and verify it; it
does not redistribute the dependency or runtime.

The observations are source-, version-, input-, and OS-bound. They do not
establish exactly-once execution, package-wide correctness, official MCP
conformance, security, performance, production reliability, independent
review, external use, or adoption.

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
