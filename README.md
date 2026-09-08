# Canonical Agent Operating Model

This repository is the canonical source for the cross-project engineering
operating model.

- `AGENTS.md` is the canonical portable baseline.
- The local Codex installation uses `~/.codex/AGENTS.md`.
- Repository projects receive a synchronized portable block.
- Project-specific rules remain project-owned.
- Conflicts between the global baseline and intentional project rules require
  an owner decision rather than a silent override.

## Version and maintenance

The portable model version is **1.1.0**, recorded in `VERSION` and the
`AGENTS.md` provenance header. The 7 September 2026 owner-approved amendment
is a MINOR increment from 1.0.0: it refines the role/verification workflow while
preserving repository specialization and promotion, release and deploy safety.

Codex is the mandatory technical proxy translating Owner + ChatGPT's WHAT into
a repository-aware Cursor task. Cursor executes that task; Codex reviews and
controls integration. Task review, product smoke and full release validation
are distinct levels. Full validation remains mandatory before stable promotion;
broad suites are not automatically required after every ordinary task.

This canonical documentation repository currently has one maintained line,
`master`, and no `dev` integration branch. Changes use a short-lived scoped
branch from current `master` and a PR targeting `master`; never direct-push the
canonical line. This is repository maintenance guidance, not an instruction to
remove integration branches from consuming projects. For this amendment, leave
the PR unmerged for the owner's separate ChatGPT independent review.

Keep the canonical `AGENTS.md` itself purely portable. Consumer project rules
belong outside the copied portable block. A consuming PR that copies an
unmerged baseline must link the exact canonical PR/HEAD and remain a dependent
proposal until canonical review resolves; it must not claim the new baseline
is already canonical on `master`. Do not silently install an unreviewed proposal
into the machine-global `~/.codex/AGENTS.md`.
