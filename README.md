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

The proposed portable model version is **1.2.0**, recorded in `VERSION` and the
`AGENTS.md` provenance header. The 24 September 2026 amendment adds local
Codex-to-Cursor CLI orchestration while preserving distinct implementation and
review roles and the existing Git, promotion, release, and deploy gates.

Codex is the mandatory technical proxy translating Owner + ChatGPT's WHAT into
a repository-aware Cursor task. Cursor executes that task; Codex reviews and
controls integration. Task review, product smoke and full release validation
are distinct levels. Full validation remains mandatory before stable promotion;
broad suites are not automatically required after every ordinary task.
When the local Cursor CLI works, Codex launches an explicit approved model in
the verified task worktree, waits for process exit without repeated model-driven
polling, and independently reviews the resulting artifact. A manual owner
copy/paste handoff is not the normal route.

This canonical documentation repository currently has one maintained line,
`master`, and no `dev` integration branch. Changes use a short-lived scoped
branch from current `master` and a PR targeting `master`; never direct-push the
canonical line. This is repository maintenance guidance, not an instruction to
remove integration branches from consuming projects. Leave a PR unmerged when
its required independent review has not been completed.

Keep the canonical `AGENTS.md` itself purely portable. Consumer project rules
belong outside the copied portable block. A consuming PR that copies an
unmerged baseline must link the exact canonical PR/HEAD and remain a dependent
proposal until canonical review resolves; it must not claim the new baseline
is already canonical on `master`. A machine-global `~/.codex/AGENTS.md` may
track such a candidate only with explicit owner authorization and an exact
candidate reference.

## New project bootstrap

After a baseline is merged, copy the complete `AGENTS.md` from canonical
`master` between `<!-- PORTABLE-OPERATING-MODEL:BEGIN -->` and
`<!-- PORTABLE-OPERATING-MODEL:END -->` in the new repository's root
`AGENTS.md`. Put project-specific rules outside those markers. Before merge,
identify a candidate by its exact PR and commit instead of calling it the
published canonical baseline. Reconcile any intentional project override with
the owner before substantial implementation.
