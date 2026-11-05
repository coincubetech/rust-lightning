# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

See [CONTRIBUTING.md](CONTRIBUTING.md) for build commands, testing, code style, and development workflow.

## Workspace Structure

See [README.md](README.md) for the workspace layout and [ARCH.md](ARCH.md) for some additional remark regarding important parts of LDK's architecture.

## Development Rules

- Always ensure tests pass before committing. To this end, you should run
  `cargo +1.75.0 test` for all affected crates and/or features. Upon completion
  of the full task you might prompt the user whether they want you to run the
  full CI tests via `./ci/ci-tests.sh`. Note however that this script will run
  for a very long time, don't timeout when you do.
- Run `cargo +1.75.0 fmt --all` before committing code changes. If rust 1.75.0 is
  not installed, skip this step.
- Never add new dependencies unless explicitly requested.
- Always disclose the use of any AI tools in commit messages and PR descriptions using a `Co-Authored-By:` line.
- When adding new `.rs` files, always add the licensing header as found in other files.
- When adding comments, do not refer to internal logic in other modules, instead
  make sure comments make sense in the context they're in without needing other
  context. Only add comments that aren't trivially obvious from the code.
- Don't add comments or documentation which contrasts the previous state - code
  comments and documentation must only describe the current state of things.
- Try to keep code DRY - if new code you add is duplicate with other code,
  deduplicate it.

## Shared startup and integration branches (owner instruction, 2026-11-04)

This repository belongs to COINCUBE. Before substantive work, read the owning
workspace's AGENTS.md and required company context, then this repository's
instructions. Load `tirith-tech/agent-ops` from one verified current reviewed
`main` commit, reading committed AGENTS.md, README.md, contracts/task.md,
docs/task-routing.md, workflows/delivery.md, workflows/pr-review-repair.md and
workflows/batched-ci.md. Read its owning company profile when available; never
substitute another company's brain. Use an existing verified checkout or fetch
the committed files from GitHub without switching another worker's checkout.
Record the full policy SHA and startup receipt in the task's existing issue/PR.
A link alone does not prove the policy was read. If unavailable, report that
before dependent work.

Robert adopted integration-branch batching here. Verify the current primary
branch (currently `main`). Honor an assigned PR target; otherwise reuse a
matching integration branch only after checking scope and integrator ownership,
or create `feature/<topic>` from current primary for multi-slice work. Create
component task branches/worktrees from it and target their PRs there. Choose
automatically; ask only for ambiguous targets, scope or conflicting ownership.
Small standalone fixes may use one draft PR to primary. Never retarget unrelated
active PRs. Record base/head SHAs, chosen targets and one integration owner.

Component PRs use local checks and independent exact-head review. Final PRs to
`main`, `redesign` stay draft while assembling the batch; local validation,
finding dispositions and independent exact-head acceptance allow ready, which
starts applicable hosted CI. Hosted checks must pass before the existing merge
gate. Missing, skipped or unscheduled CI is not passed. Preserve all company
merge/deployment authority, protection and specialist-review requirements.
This adoption changes branch routing and CI scheduling only. For this workflow
it supersedes older instructions that require CI before the ready transition.

PRs targeting the long-standing `redesign` branch also run CI. Do not rename it
or assume unrelated work belongs there.
