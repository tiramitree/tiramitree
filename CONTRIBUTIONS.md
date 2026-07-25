# Open-source contribution log

Updated: 2026-07-25

This page is a status-aware record of public engineering work. A submitted
change is not counted as accepted until the upstream repository merges it.
Material AI assistance is disclosed, and local validation is kept separate
from online CI and independent review.

## ByteDance DeerFlow: executable-scan policy parity

- Pull request: [bytedance/deer-flow#4451](https://github.com/bytedance/deer-flow/pull/4451)
- Upstream base: `3b77a7401b549fa6da4c8e1f8c2c0081d56e3d7a`
- Proposed commit: `ffc62e8367daa0b0f52a4562ca9bef1906d51514`
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
- Proposed commit: `e068d1fb049e32a36a34398d9c1b163855736f35`
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
- Commit: `35deb82a327df6e51e173cc3c5ab115363b553d0`
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
