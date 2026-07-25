# tiramitree

Research engineer building auditable execution and evaluation harnesses for AI
and embodied-research workflows.

I work at the boundary between technical research and the systems that make
research results trustworthy: evaluation protocols, provenance, fail-closed
execution, recovery, and reproducible long-running experiments.

## Current focus

- experiment harnesses today; agent evaluation is a target application, not a
  claimed deployment
- 3D semantic scene completion and low-label SemanticKITTI protocols
- embodied-AI simulation and benchmark reliability
- experiment infrastructure, exact receipts, replay, and failure analysis
- Python, C++, Linux, PyTorch, and systems-oriented testing

## Selected evidence

- BenchHandoff local, AI-assisted release candidate: a fail-closed CLI for
  auditable, resumable sequential experiments. Its local Windows compatibility
  matrix spans CPython 3.11.15, 3.12.13, 3.13.14, and 3.14.6; each of four
  independent runs covered 122 tests (119 pass, 3 permission skips). This is
  not one 488-test suite, Linux or online CI, or independent reproduction. Its
  content-addressed resume decision binds reviewed evidence, outputs, and next
  inputs to exact digests; after deliberate partial-output drift, a stale
  decision was refused before harness mutation and a refreshed decision
  completed. One-command
  generation and read-only verification produce a five-file, commit-bound
  reproduction package recording 18 versus 13 child calls and 5 versus 0
  repeated successful tasks with the same final output identity; an
  appended-byte tamper copy was rejected with exit 30. The decision is not a
  signature or global lock and assumes one trusted writer. These are local
  synthetic counts, not speed, production, independent reproduction, or
  adoption evidence. A canonical external-evidence ledger currently reports
  zero independent reproductions, users, institutional adopters, and
  third-party reviews; Issue submissions do not count until human-reviewed and
  merged. Public links will replace this text only after the license, first
  online CI run, and exact release artifact are verified.

## Engineering principles

- make the protocol inspectable before optimizing the result;
- preserve failed runs as evidence rather than rewriting the story;
- distinguish tested behavior, simulated behavior, and production behavior;
- prefer one maintained upstream contribution over many disconnected demos.

## Open-source contributions

[Detailed contribution log](https://github.com/tiramitree/tiramitree/blob/main/CONTRIBUTIONS.md)
with commit-bound validation and current review state.

- AI-systems build compatibility: [DeepSeek DeepEP PR
  #699](https://github.com/deepseek-ai/DeepEP/pull/699) removes a hardcoded
  C++17 flag from the hybrid-EP PyTorch extension and adds a CPU-verifiable
  red/green regression. It is open and unreviewed; no CUDA build, GPU run,
  acceptance, or merge is claimed.
- Agent-orchestration reliability: [ByteDance DeerFlow draft PR
  #4455](https://github.com/bytedance/deer-flow/pull/4455) separates launch
  failures from post-launch bookkeeping failures so a confirmed agent run
  keeps its per-task active slot and run identifier instead of permitting a
  duplicate dispatch. A real-SQLite regression went red on the exact base and
  green with the repair; 42 related tests pass. Human line review, the
  contributor license agreement, and upstream review remain pending.
- Agent-harness security: [ByteDance DeerFlow draft PR
  #4451](https://github.com/bytedance/deer-flow/pull/4451) proposes one shared
  executable-file classifier for archive installs and agent-managed skill
  writes, with red/green regressions for code suffixes, extensionless
  shebangs, and nested-`scripts` false positives. It is a public draft pending
  the project's required human line review, contributor license agreement, and
  upstream review; it is not accepted or merged.
- Embodied-AI documentation: the exact correction in [AgiBot Genie Sim PR
  #177](https://github.com/AgibotTech/genie_sim/pull/177) is submitted and
  open; it is not accepted, merged, or an AgiBot endorsement.
