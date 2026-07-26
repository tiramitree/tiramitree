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
[public tag CI](https://github.com/tiramitree/benchhandoff/actions/workflows/ci.yml)

BenchHandoff is an Apache-2.0 local CLI for fail-closed, resumable sequential
experiment batches. It fingerprints suites and declared inputs, preserves
failed attempts, verifies completed outputs before skipping them, and can bind
an approved resume to the exact evidence reviewed before mutation. Cooperating
local writers are serialized, and orphaned lock records require an explicit,
evidence-bound recovery action.

The current source is
[`e5d687d967361ed55751551e9454ce3593a10ffc`](https://github.com/tiramitree/benchhandoff/commit/e5d687d967361ed55751551e9454ce3593a10ffc);
the recreated v0.1.0 tag peels to
[`98e7a9e9227f39fee16b9d04c8f68ea89273a4fe`](https://github.com/tiramitree/benchhandoff/commit/98e7a9e9227f39fee16b9d04c8f68ea89273a4fe).
Verified public evidence includes:

- a successful current-main run and a 10-job tag run, including eight Ubuntu
  and Windows jobs across CPython 3.11-3.14;
- the dependent evidence job generated and re-verified a five-file synthetic
  package;
- all eight recreated Release assets passed server-digest and public-redownload
  name, size, and SHA-256 checks, and the exact wheel passed an isolated
  recovery/resume/verify smoke test; and
- the deterministic synthetic comparison records 18 child calls for naive
  restart versus 13 for resume, with 5 versus 0 repeated successful tasks and
  equal final output identity.

Those are synthetic work counts and control-plane checks, not wall-clock,
production, security-boundary, distributed-systems, or model-quality results.
The release is GitHub-only: there is no PyPI package, production support or
SLA, independent reproduction, third-party review, or verified external
adoption. The external-evidence ledger keeps those counts at zero until such
evidence exists.

## Second owned project: EffectWitness

[Repository](https://github.com/tiramitree/effect-witness) |
[v0.1.0 pre-release](https://github.com/tiramitree/effect-witness/releases/tag/v0.1.0) |
[public tag CI](https://github.com/tiramitree/effect-witness/actions/runs/30216628917)

EffectWitness is an Apache-2.0 controlled workbench for comparing declared MCP
tool-effect hints, client observations, and durable synthetic SQLite effects
under ambiguous failures. It records separate declaration, observation, and
effect facts instead of treating a successful-looking response as proof of an
external effect.

Current `main` and the lightweight v0.1.0 tag both resolve to
[`72474eae59931cfe0be6501cd340d07c34a100ca`](https://github.com/tiramitree/effect-witness/commit/72474eae59931cfe0be6501cd340d07c34a100ca).
Its public evidence includes:

- ten registered loopback scenarios covering clean repeats, response loss,
  process exit, restart/reconciliation, concurrent repetition, and payload
  conflict;
- a declared-contract matrix of 3 `MATCH`, 4 `MISMATCH`, and
  3 `NOT_APPLICABLE`;
- main and tag CI runs that each passed all seven jobs, including Ubuntu and
  Windows tests for Python 3.11-3.13; and
- five public assets with matching GitHub digests and fresh-download
  checksums, including a source-bound reference artifact that passes the
  bundled offline verifier.

The 3/4/3 matrix is not a success rate or model score. This pre-alpha synthetic
fixture does not establish arbitrary-tool exactly-once execution, official MCP
conformance, production or distributed correctness, security, performance,
independent review, external use, adoption, or recruiting outcomes.

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
[`a61287f0260ee4e18689e8e4ce16218a2cb839f5`](https://github.com/tiramitree/genie_sim/commit/a61287f0260ee4e18689e8e4ce16218a2cb839f5),
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
