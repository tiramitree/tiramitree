# tiramitree

I build auditable AI and research-engineering systems: evaluation harnesses,
failure recovery, provenance, and reproducible execution for long-running
experiments.

My current public work focuses on AI systems, agent evaluation infrastructure,
and embodied/3D research engineering. Local tests, public CI, released
artifacts, independent review, and external use are different kinds of
evidence.

## Current focus

- auditable execution, evidence integrity, and failure recovery
- agent evaluation and experiment harnesses, without deployment claims
- embodied-AI simulation and benchmark control planes
- Python, C++, Linux, PyTorch, and systems-oriented testing

## Flagship: BenchHandoff

[Repository](https://github.com/tiramitree/benchhandoff) |
[v0.1.0 release](https://github.com/tiramitree/benchhandoff/releases/tag/v0.1.0) |
[public CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml)

BenchHandoff is an Apache-2.0 local CLI for fail-closed, resumable sequential
experiment batches. It fingerprints suites and declared inputs, preserves
failed attempts, verifies completed outputs before skipping them, and can bind
an approved resume to the exact evidence reviewed before mutation. Cooperating
local writers are serialized, and orphaned lock records require an explicit,
evidence-bound recovery action.

Public, commit-bound evidence for
[`98e7a9e9227f39fee16b9d04c8f68ea89273a4fe`](https://github.com/tiramitree/benchhandoff/commit/98e7a9e9227f39fee16b9d04c8f68ea89273a4fe):

- eight Ubuntu 24.04 / Windows Server 2025 jobs across CPython 3.11-3.14 each
  ran all 158 tests with no failures, errors, or skips;
- the dependent evidence job generated and re-verified a five-file synthetic
  package;
- the package job built, inspected, installed, and smoke-tested the exact
  released wheel and sdist; and
- the deterministic synthetic comparison records 18 child calls for naive
  restart versus 13 for resume, with 5 versus 0 repeated successful tasks and
  equal final output identity.

Those are synthetic work counts and control-plane checks, not wall-clock,
production, security-boundary, distributed-systems, or model-quality results.
The release is GitHub-only: there is no PyPI package, production support or
SLA, independent reproduction, third-party review, or verified external
adoption. The external-evidence ledger keeps those counts at zero until such
evidence exists.

## Engineering principles

- make the protocol inspectable before optimizing the result;
- preserve failed runs as evidence rather than rewriting the story;
- distinguish tested behavior, simulated behavior, and production behavior;
- prefer a small number of deep, owned projects over disconnected demos.

## Embodied-systems experiment

[Personal Genie Sim fork branch](https://github.com/tiramitree/genie_sim/tree/portfolio/resumable-benchmark-batch)

This public branch adds an opt-in, exact, inclusive `--resume-from` anchor to
the sequential benchmark CLI while preserving the default order and aggregate
failure behavior. At exact branch head
[`f50a597502903463101b377465a1d65a8a6abb6f`](https://github.com/tiramitree/genie_sim/commit/f50a597502903463101b377465a1d65a8a6abb6f),
local red-before/green-after validation ran eight tests: the exact upstream
base failed and the public branch head passed. A real-config dry run selected
the expected 9 configurations from a 10-config set with simulator launch mocked.

This is a personal-fork control-plane experiment, not a new upstream
submission, maintainer-requested change, review, acceptance, merge, AgiBot
endorsement, simulator/GPU result, model-quality result, or external-use claim.

## Engineering record

The [status-aware public work log](CONTRIBUTIONS.md) preserves earlier proposed
upstream changes with their actual review state and validation limits. A
submitted or mergeable change is not described as accepted.

OpenAI Codex materially assisted implementation, testing, documentation, and
publication workflows. Human identity, legal commitments, and claims of
independent review remain human-only.
