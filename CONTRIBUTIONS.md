# Public engineering work log

Updated: 2026-07-27

This page is a status-aware record of public engineering work. A submitted
change is not counted as accepted until the upstream repository merges it.
Material AI assistance is disclosed, and local validation is kept separate
from online CI and independent review.

The current portfolio emphasis is work in repositories owned by
`tiramitree`. The upstream proposals below remain as historical, status-aware
records; this page does not imply a plan to open new upstream pull requests,
issues, or discussions.

## Owned repository: BenchHandoff v0.1.0

- Repository: [tiramitree/benchhandoff](https://github.com/tiramitree/benchhandoff)
- Release:
  [v0.1.0](https://github.com/tiramitree/benchhandoff/releases/tag/v0.1.0)
- Current source: `e5d687d967361ed55751551e9454ce3593a10ffc`
- Recreated tag commit: `98e7a9e9227f39fee16b9d04c8f68ea89273a4fe`
- Current status: Apache-2.0, GitHub-only early release

The current-main run succeeded and the recreated-tag run passed all 10 jobs,
including eight Ubuntu and Windows runtime jobs across CPython 3.11-3.14 plus
the dependent evidence and exact-distribution jobs. All eight recreated
Release assets passed server-digest and public-redownload name, size, and
SHA-256 checks. The exact wheel also passed an isolated install and
recovery/resume/verify smoke test.

The synthetic comparison records 18 versus 13 child calls and 5 versus 0
repeated successful tasks, with equal final output identity. These are
deterministic control-plane work counts, not timing, production, security,
model-quality, independent-review, or adoption evidence. No TestPyPI or PyPI
package was published, and the external-evidence ledger remains zero.

## Owned repository: EffectWitness v0.1.0

- Repository:
  [tiramitree/effect-witness](https://github.com/tiramitree/effect-witness)
- Pre-release:
  [v0.1.0](https://github.com/tiramitree/effect-witness/releases/tag/v0.1.0)
- Evidence source: `f4575f88cf6a17f6c32bd2c7462063142d37c56a`
- Current main and lightweight tag:
  `72474eae59931cfe0be6501cd340d07c34a100ca`
- Main CI:
  [run 30216628502](https://github.com/tiramitree/effect-witness/actions/runs/30216628502)
- Tag CI:
  [run 30216628917](https://github.com/tiramitree/effect-witness/actions/runs/30216628917)
- Current status: Apache-2.0, public pre-alpha GitHub pre-release

EffectWitness compares declared MCP tool-effect hints, client observations, and
durable synthetic SQLite effect facts under ten registered loopback scenarios.
The matrix contains 3 `MATCH`, 4 `MISMATCH`, and 3 `NOT_APPLICABLE`
declared-contract classifications. Main and tag CI each passed all seven jobs,
including Ubuntu and Windows tests for Python 3.11-3.13.

All five public assets passed GitHub digest and fresh-download checksum checks.
The source-bound reference ZIP also passed the bundled schema-v2 offline
verifier. An intermediate history commit can check out its generated JUnit file
with normalized line endings; the current main/tag revision fixes that and is
the only verified release state.

This is controlled synthetic loopback evidence, not a success rate, model
score, arbitrary-tool exactly-once guarantee, official MCP conformance,
production or distributed correctness, security result, independent review,
external use, adoption, or recruiting signal. No PyPI package was published.

## Personal fork: Genie Sim resumable benchmark batch

- Public branch:
  [portfolio/resumable-benchmark-batch](https://github.com/tiramitree/genie_sim/tree/portfolio/resumable-benchmark-batch)
- Exact head: `a61287f0260ee4e18689e8e4ce16218a2cb839f5`
- Current status: personal-fork experiment; not submitted upstream, reviewed,
  accepted, or merged

The branch adds an opt-in, exact, inclusive `--resume-from` anchor after the
existing robot/category selection. In a local red-before/green-after run, the
eight-test suite failed on the exact upstream base and passed at the public
branch head. With simulator launch mocked, a real-config dry run selected the
expected 9 configurations from a 10-config set.

No Isaac Sim, GPU benchmark, episode, scientific metric, external operator, or
maintainer-demand claim is made. This branch is not an AgiBot contribution or
endorsement.

## DeepSeek DeepEP: PyTorch-selected C++ standard for hybrid EP

- Pull request: [deepseek-ai/DeepEP#699](https://github.com/deepseek-ai/DeepEP/pull/699)
- Upstream branch and base: `hybrid-ep` at
  `94a9f8f6b146c07d97ec58f67cd6d303296d6098`
- Current PR head: `7f3d6d8c41a84c481167785bd559688bd50dbc34`
- Current status: open, non-draft, and reported clean by GitHub at the latest
  observation. An automated collaborator review found a Python 3.8 test
  incompatibility; the follow-up commit repaired it and responded to all three
  inline comments. There is no human review, acceptance, or merge.

### Problem and proposed invariant

`hybrid_ep_cpp` forced NVCC to compile with `-std=c++17`, even when current
PyTorch headers require C++20. Its sibling `deep_ep_cpp` already leaves the
standard unset and inherits PyTorch's compatible choice.

The proposed change removes only the extension's hardcoded standard. It leaves
the separate runtime JIT compiler's C++17 setting unchanged.

### Validation

- A new standard-library regression test failed on the exact upstream base
  because the hardcoded standard was present.
- The same test passed after the one-line source change.
- After automated review, the guard was widened to catch appended and `cxx`
  standard flags and was made Python 3.8 compatible.
- The exact test passed under actual Python 3.8.10 and Python 3.12.10.
- Python compilation and `git diff --check`: passed.
- No NVCC/CUDA build, GPU workload, or training run was performed in this
  environment.

This is a submitted build-compatibility proposal with a CPU-verifiable
structural regression, not a hardware validation, performance result, accepted
DeepSeek contribution, or DeepSeek endorsement.

## ByteDance DeerFlow: post-launch scheduler slot preservation

- Pull request: [bytedance/deer-flow#4455](https://github.com/bytedance/deer-flow/pull/4455)
- Upstream base: `3b77a7401b549fa6da4c8e1f8c2c0081d56e3d7a`
- Current PR head: `bbb28277108830b5f0c21ad9c30800b1d00f205f`
- Current status: public draft; required human line review and CLA are pending;
  no upstream review, acceptance, or merge

### Problem

The scheduled-task partial unique index permits only one queued or running row
per task. After `_launch_run` returned a live run, however, a transient failure
in the queued-to-running bookkeeping write fell into the broad launch-failure
handler. That handler marked the row failed, released its unique active slot,
discarded the returned run identifier, and allowed a later dispatch to launch
duplicate work while the first run was still live.

### Proposed invariant

Only failures before a valid run and thread identifier are returned are launch
failures. Later bookkeeping errors keep the task-run row non-terminal, retain
the launched identifiers, and best-effort retry only the idempotent row update;
the non-idempotent parent run-count update is not blindly retried.

### Validation

- The real-SQLite regression failed on the exact base because the first
  dispatch returned `failed`.
- After the repair, the same regression retained `run-1`, rejected the second
  dispatch, and kept exactly one active running row bound to `run-1`.
- Scheduler service, race, repository, and router suites: 42 passed.
- Full backend lint and formatting checks: passed; 960 Python files were
  already formatted.
- The full Windows backend run reported 9,088 passed, 94 skipped, and 98
  failed. Every one of those 98 nodes also failed in an untouched detached
  worktree at the exact base commit under the same locked environment; none
  were scheduler tests. This is baseline parity, not a full-suite pass.

This is a proposed scheduler-invariant repair, not a production-incident,
upstream acceptance, deployment, adoption, or ByteDance endorsement claim.

## ByteDance DeerFlow: executable-scan policy parity

- Pull request: [bytedance/deer-flow#4451](https://github.com/bytedance/deer-flow/pull/4451)
- Upstream base: `3b77a7401b549fa6da4c8e1f8c2c0081d56e3d7a`
- Current PR head: `44e0620d62cda9b71a4f03ccd1232ee7c038a53f`
- Current status: public draft; required human line review and CLA are pending;
  no upstream review or acceptance

### Problem

Archive installs treated top-level `scripts/` files, known code suffixes
anywhere in a skill, and extensionless shebang files as executable for the
stricter LLM security policy. Agent-managed `skill_manage(write_file)` calls
instead tested whether the raw path string contained `scripts/`.

That mismatch produced both directions of error:

1. `references/helper.py` and an extensionless shebang file could be scanned as
   non-executable, allowing an LLM `warn` decision; and
2. `references/scripts/notes.txt` could be treated as executable solely because
   a nested path component was named `scripts`.

### Proposed invariant

One pure classifier is shared by archive installs and agent-managed writes.
Only a top-level `scripts/` directory, a known code suffix, or an extensionless
leading shebang activates the executable policy.

### Validation

- New regression selection on the exact base before the implementation:
  3 failed.
- The same selection after the implementation: 3 passed.
- Skill-management and installer suites: 72 passed.
- Related native SkillScan suite: 132 passed with two deep-AST tests deselected.
- Exact combined run: 204 passed and 2 failed. Both failures are unchanged
  deep-AST tests where Windows CPython 3.12.13 raises `RecursionError` inside
  `ast.parse` before the analyzer runs.
- Ruff formatting, Ruff lint, compileall, and `git diff --check`: passed.

This is a proposed security-policy consistency repair, not a claim of a
critical vulnerability, production incident, upstream acceptance, or ByteDance
endorsement.

## AgiBot Genie Sim: runnable benchmark category examples

- Pull request: [AgibotTech/genie_sim#177](https://github.com/AgibotTech/genie_sim/pull/177)
- Upstream base: `da424345f3a2e851b5f342aeed8e5616fc210f0e`
- Current PR head: `3db1f6835ad88df01bde1a24a3a153727e21f558`
- Current status: open and mergeable at the latest observation; no review,
  acceptance, or merge

The benchmark documentation used
`--category=instruction_following`, while the CLI derives the category from the
second config-name token and recognizes `if`. The old example returned no
matching configurations. The documentation-only patch changes both examples to
`--category=if`; source-package verification returned 10 runnable
`g2op_if_*` configurations.

This is an exact documentation correction, not a runtime feature, Isaac Sim/GPU
execution claim, accepted contribution, or AgiBot endorsement.

## Owned-repository governance: FDE claim boundaries

- Pull request: [tiramitree/fde-ai-systems-portfolio#19](https://github.com/tiramitree/fde-ai-systems-portfolio/pull/19)
- Current PR head: `cf124862b319094997b77b4dbd538ca7914409d4`
- Current status: open; online quality gate passed; protected merge still
  requires a genuine non-author code-owner and last-push approval

The change discloses material AI assistance, labels the three projects as
fictional-data local reference prototypes, and removes unsupported deployment,
production-readiness, adoption, and independent-authorship implications.

This is repository governance on an owned project, not independent upstream
review or external adoption.

## Evidence policy

- Draft, open, mergeable, reviewed, approved, and merged are distinct states.
- Local tests do not become online CI unless GitHub runs them.
- Stars, forks, downloads, and self-authored runs are not adoption.
- No employer, customer, user, performance, or production claim is inferred
  from a pull request.
- OpenAI Codex materially assisted the audits, tests, implementation,
  validation, documentation, and publication workflow. Human-only review,
  approval, and legal commitments remain human-only.
