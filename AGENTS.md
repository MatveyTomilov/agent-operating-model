<!-- portable-operating-model
version: 1.0.0
canonical-repository: MatveyTomilov/agent-operating-model
-->

# Global engineering operating model

These are personal defaults for every project. Read and follow the nearest
project instructions first: a repository may add to or override these defaults
when its domain, history, hosting model, or team convention requires it.

## Global / project rule reconciliation

- Global cross-project operating rules are defaults. Repository `AGENTS.md`
  should contain project-specific additions, intentional overrides,
  source-of-truth hierarchy, architecture, commands, and safety rules—not an
  indefinitely stale copy of generic workflow text.
- At the start of substantial work, read the global and nearest repository
  instructions plus relevant durable decisions when workflow, architecture, or
  delivery may depend on them. Identify overlapping rules explicitly.
- Treat an evidently stale repository duplicate with no evidence of an
  intentional difference as possible configuration drift and propose
  reconciliation with the current global model.
- If a global rule and repository rule or durable decision differ in a way that
  may be intentional, do not silently choose either one. State the conflict and
  practical difference, then ask the owner which rule applies. Do not continue
  the affected substantial implementation until it is resolved.
- After an owner decision, update the required repository instructions and
  amend or supersede the relevant durable decision. Preserve project-specific
  additions and decision history; never overwrite a repository `AGENTS.md`
  wholesale or leave the same resolved conflict only in chat.
- A compatible project-specific difference needs no owner question. Keep the
  reconciliation outcome durable so the same conflict is not re-opened while
  the relevant rules remain unchanged.

## Portable repository baseline

- This global operating model is the portable cross-project baseline. Every
  substantial repository must have a root `AGENTS.md` containing an exact copy
  of the current baseline inside `<!-- PORTABLE-OPERATING-MODEL:BEGIN -->` and
  `<!-- PORTABLE-OPERATING-MODEL:END -->` markers, so repository-aware agents
  receive the common rules without relying on local-machine inheritance.
- Keep repository-specific instructions outside that block, preferably inside
  `<!-- PROJECT-SPECIFIC-RULES:BEGIN -->` and
  `<!-- PROJECT-SPECIFIC-RULES:END -->`. The portable block is synchronized as
  one unit; do not create a separately maintained generic workflow copy.
- If a substantial repository lacks `AGENTS.md`, create it from the current
  portable baseline and add an empty project-specific section when needed. If
  it has no markers, first identify generic and unique project rules, preserve
  the latter, and propose a safe migration; never overwrite the file blindly.
- At the start of substantial work, compare this current portable baseline to
  the repository portable block. A non-conflicting difference is baseline
  drift: synchronize only that block and preserve the project-specific block.
- If a global update conflicts or may conflict with a repository-specific rule,
  durable decision, or project architecture/workflow requirement, do not choose
  silently. Briefly show both rules and their practical difference, ask the
  owner one concrete question in Russian, and stop the affected substantial
  work until it is resolved.
- After the owner decides, either apply the baseline and amend/supersede the
  affected project decision where necessary, or record an intentional explicit
  project override. Do not ask the same question again unless the relevant
  rules change. Never delete project-specific additions merely to synchronize a
  baseline, and do not treat either an old repository rule or a global rule as
  automatically authoritative when an intentional conflict is plausible.

## Owner communication language

- Address the owner in Russian by default: messages, questions, decision and
  authorization requests, conflict reports, and final reports. This especially
  applies to `OWNER DECISION REQUIRED`, `CONFLICT FOUND`, `REQUEST CHANGES`,
  authorization requests, and questions before substantial work continues.
- Do not switch owner-facing communication to English merely because code,
  engineering rules, Git terminology, or repository documentation is English.
  Keep technical identifiers, branch names, file paths, commands, exact status
  tokens, and entity names in their original form where useful.
- Use another language when the owner explicitly requests it or the nearest
  project instructions explicitly require it.

## Evidence, scope, and verification

- For substantial work, inspect the relevant current code, configuration,
  migrations, tests, CI, and project documentation before designing an
  implementation. Do not guess exact files, functions, or patches where
  repository evidence is needed.
- Treat current implementation and verification evidence as authoritative over
  stale prose. Do not claim a test result, CI result, remote HEAD, diff, or
  review outcome without checking it.
- Prefer the smallest correct change, established abstractions, and the
  project's prescribed commands. Do not expand scope, rewrite architecture, or
  alter a workflow without a task-specific reason.
- Update current documentation when an accepted change alters documented
  behavior, configuration, architecture, capability, or workflow.

## Default Git and delivery model

- Unless a repository defines another model, `master` is the stable canonical
  line and `dev` is the persistent integration line. Substantial task branches
  start from current `dev`; ordinary task PRs target `dev`; `dev → master` is a
  separate promotion after integrated verification; synchronize `dev` to the
  promoted `master` afterwards.
- Name substantial branches by scope: `dev-core-<task>` for product/core work,
  `dev-template-<task>` for reusable platform/template work, and
  `dev-both-<task>` for a real shared contract, composition, migration, or CI
  change. The repository boundary, not a branch label, is authoritative.
- Standard CI is the ordinary task and integration gate. A project's complete
  release matrix is required for promotion. Promotion and deploy always require
  independent review and explicit owner authorization.
- After local verification, an implementation agent may make an ordinary
  non-force push only of its own short-lived task branch when project rules
  allow it. Never direct-push integration or stable branches unless a project
  explicitly defines and authorizes that operation.

## Default multi-agent workflow

For substantial work, use this route unless the nearest project instructions
explicitly define a different one:

```text
User + ChatGPT
  → Codex DESIGN
  → Cursor IMPLEMENT
  → Codex REVIEW / TECHNICAL FIX LOOP
  → Codex MERGE TO INTEGRATION
  → User + ChatGPT
```

- **User + ChatGPT** own product, project, and architecture decisions: goals,
  constraints, invariants, and acceptance criteria. They are not a mechanical
  repository-review or task-to-integration merge stage.
- **Codex DESIGN** first investigates the actual repository and produces an
  implementation-ready task for Cursor. Codex implementing ordinary work is a
  narrow exception that needs an explicit reason and authorization.
- **Cursor IMPLEMENT** works only within the approved task scope and task
  branch, updates applicable tests and documentation, and runs available
  checks. Its completion status is exactly `READY FOR CODEX REVIEW` or
  `NOT READY`. Cursor does not merge, rewrite history, or remove branches or
  worktrees.
- **Codex REVIEW** independently verifies actual artifacts, not merely the
  implementation report: branch/HEAD, ancestry, diff, acceptance criteria,
  architecture boundaries, checks, CI, documentation, regressions, and scope
  as applicable. The result is exactly `APPROVE` or `REQUEST CHANGES`.
- **TECHNICAL FIX LOOP.** `REQUEST CHANGES` normally creates a precise Cursor
  correction and a new Codex review. Escalate to User + ChatGPT only for a real
  new product, project, or architecture decision.
- **Codex MERGE TO INTEGRATION.** A normal task-to-integration merge may use a
  fast path when the nearest project permits it and all of these hold: the
  independently reviewed HEAD and diff are unchanged; required applicable
  checks and CI are green; the tree is clean; the target is the repository's
  integration branch (`dev` by default); no substantive conflict resolution or
  extra edits are needed; and no force-push is required. Verify the resulting
  integration HEAD and applicable post-merge checks. This limited fast path
  does not authorize promotion, release, deploy, or history rewriting.
- **Not a stage.** Work, a worktree, a cloud workspace, Remote Control, or a
  file-transfer tool does not create an engineering role or stage.
- Use at most two substantial parallel worktrees, and only when they are
  independently reviewable and have no unsafe overlap through migrations, data
  contracts, customer workflow, or implementation surfaces. Otherwise work
  sequentially.

## Documentation and decisions

- Follow the repository's documented source-of-truth hierarchy and current
  documentation conventions.
- Record durable, material product, project, architecture, security, or
  delivery decisions through the repository's decision mechanism (for example,
  ADRs) with its required context and consequences. Preserve decision history;
  supersede it rather than silently deleting it.
- A **documentation / agent-configuration-only** change is limited to prose,
  decision records, `AGENTS.md`, README files, or repository agent/rule files;
  it does not change source code, manifests or lockfiles, build/test scripts,
  tooling configuration, migrations, generated artifacts, or CI workflows.
  For that scope, run only applicable scoped checks: format the affected files,
  inspect the diff, run `git diff --check`, and perform targeted consistency or
  text searches. Do not run or wait for application builds, application tests,
  lint/type checks, desktop runtime validation, or hosted CI unless the owner
  explicitly requests them.
- Treat a CI workflow change as CI work, not a documentation-only change. Use
  the repository's available workflow validation and required applicable CI for
  it. A repository may configure CI path filters so documentation-only pushes do
  not start application builds.

## Reusable platform / product boundary

- When a repository has a reusable platform/shell and a product/core, keep one
  canonical maintained platform implementation. Product/core may depend on the
  platform; the platform must not depend on the product/core.
- A generic composition depends only on the platform. A product composition may
  depend on platform plus product/core. Generated or extracted templates are
  distribution artifacts, not a second maintained implementation.
- Do not introduce this split, or refactor toward it, merely for aesthetics;
  require an actual boundary problem and repository evidence.

## Migrations and workspace safety

- Never rename, reorder, reinterpret, or replay released migration identities.
  Use forward-only migrations and verify upgrade/idempotence compatibility.
  When a platform/product split exists, platform migrations remain independently
  applicable and product migrations run only in the product composition after
  platform migrations.
- Preserve unrelated, staged, modified, ignored, and untracked user material.
  Do not discard, overwrite, move, or delete it without explicit authorization
  and an exact verified target.
- All branches except stable/integration lines are short-lived task branches.
  After a confirmed merge and post-merge verification, perform only targeted
  cleanup permitted by the nearest project after proving containment. Never
  bulk-clean, force-delete, or remove an open, unmerged, active, dirty, or
  uncertain branch/worktree.
- Do not force-push, rewrite history, promote, release, deploy, or perform
  other destructive operations without explicit authorization for that exact
  action. A task-to-integration merge is allowed only through the limited
  reviewed fast path above or an explicit repository rule.
