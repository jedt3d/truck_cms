# TruckCMS Agent Instructions

## Scope

These instructions apply to the entire repository. More specific `AGENTS.md`
files may add directory-level rules but may not weaken the product, safety, or
review requirements in this file.

## Project ownership

- The project owner controls product decisions, ticket approval, acceptance
  criteria, pull request review, approval, and merge decisions.
- GitHub Project 8 is the planning board for approved work:
  <https://github.com/users/jedt3d/projects/8>
- The human creates or approves the GitHub issue, reviews the completed pull
  request, and decides whether it may merge.
- Codex is the implementer. For an approved, assigned ticket, Codex may analyze,
  plan, implement, test, document, commit, push the ticket branch, and open or
  update its pull request.
- Codex must not approve its own work, merge a pull request, push directly to
  `main`, force-push a shared branch, or weaken branch protection.
- Codex may keep the assigned Project 8 item synchronized with the board's
  existing workflow states. It must not create or rename project fields,
  statuses, or automations unless the owner explicitly requests that change.

## Required product context

Before reviewing a specification, planning a feature, or changing behavior,
read these files in order:

1. [`docs/PRD.md`](docs/PRD.md) — the mandatory v0.1 execution baseline.
2. [`docs/PRODUCT_CONCEPT.md`](docs/PRODUCT_CONCEPT.md) — product rationale,
   positioning, confirmed decisions, and open strategic questions.

Use the PRD requirement identifiers (`REQ-01` through `REQ-48`) in plans, pull
request descriptions, tests, and reviews whenever a change implements or
affects one of them.

The current owner request and its approved GitHub Project item define the task.
The PRD defines the allowed v0.1 product boundary. The product concept explains
intent but does not add requirements absent from the PRD. If these sources
conflict or leave a product decision open, stop before making an irreversible
or architectural choice and ask the owner to resolve it.

Do not implement features listed as out of scope in `docs/PRD.md`. A change to
the primary user, product promise, included capabilities, or release gates
requires an owner-approved PRD revision before implementation.

## Project management during development

Project management and implementation are one lifecycle, not two parallel jobs.
Tracking preserves the reason for a change, its approved boundary, its current
state, and the evidence needed for a human to review it. Update management
artifacts when engineering state changes; do not create duplicate status reports
or update the board for every commit.

Use one authoritative artifact for each kind of information:

| Information | Source of truth |
|---|---|
| Product promise, v0.1 scope, and requirements | `docs/PRD.md` |
| Product reasoning and confirmed direction | `docs/PRODUCT_CONCEPT.md` |
| Feature problem, scope, acceptance criteria, decisions, and open questions | GitHub issue |
| Priority and current workflow state | GitHub Project 8 |
| Implementation, review evidence, and discussion | Branch and pull request |
| Current behavior and developer usage | Code, tests, and repository documentation |

Keep management synchronized at these transition points:

| Engineering event | Project-management action |
|---|---|
| Idea becomes approved work | Create or approve the issue, define acceptance criteria and non-goals, link affected PRD requirements, and add it to Project 8. |
| Implementation starts | Move the item to the board's in-progress equivalent and create the issue-linked branch. |
| New evidence changes scope or a product rule | Pause the affected work, record the fact, decision, assumption, or open question in the issue, update canonical product documentation when required, and obtain human approval before continuing. |
| Implementation and verification finish | Open the linked PR, attach test and validation evidence, report documentation and release-note impact, and move the item to the board's review equivalent. |
| Human requests changes | Keep the same issue, branch, and PR; implement the agreed feedback and refresh verification evidence. |
| Human approves and merges | Merge through GitHub, close the linked issue, delete the branch, and move the item to the board's completed equivalent. |
| Follow-up work is discovered | Create a separate issue instead of silently expanding the completed feature. |

Do not mark a feature complete while code, tests, the issue, or affected
documentation disagree. Record material accepted decisions and their rationale
in the issue or pull request and synchronize durable decisions into the relevant
repository document.

## Development workflow

TruckCMS uses ticket-driven GitHub Flow. Every production change follows this
sequence:

1. **Ticket:** The human creates or approves a GitHub issue, adds it to Project
   8, and provides a clear problem, scope, acceptance criteria, and applicable
   PRD requirement identifiers. Do not implement an unapproved draft item.
2. **Start:** Codex reads the ticket and required product context, inspects the
   relevant source, configuration, tests, logs, and nearby code, and maps the
   work to affected requirements and launch gates. It diagnoses before changing
   and posts a short plan for multi-step work.
3. **Branch:** From the latest `origin/main`, Codex creates one short-lived
   branch named `<type>/<issue-number>-<short-slug>`, where `type` is `feature`,
   `fix`, `docs`, `test`, or `chore`. Never develop directly on `main`.
4. **Implementation:** Codex makes the smallest complete change, adds or updates
   tests and documentation, and keeps unrelated refactors, dependency upgrades,
   formatting, and user work out of the branch.
5. **Verification:** Codex runs the narrowest relevant checks first and then the
   repository's required full checks. Commands must come from repository
   configuration; do not invent commands or flags. Failures must be fixed or
   reported explicitly.
6. **Self-review:** Codex reviews the complete diff against `origin/main` for
   acceptance coverage, correctness, security, migrations, database and API
   compatibility, accessibility, documentation, and accidental files.
7. **Pull request:** Codex commits only ticket files, pushes the ticket branch,
   and opens a pull request linked with `Closes #<issue-number>`. The PR must
   summarize the change, map affected PRD requirements, report verification,
   identify risk, and contain no unrelated changes.
8. **Human review:** A human reviews the pull request and CI evidence. Codex
   addresses requested changes on the same branch, reruns affected checks, and
   updates the PR. Codex never approves its own work.
9. **Merge:** Only the human may approve and merge. Prefer squash merge unless
   preserving the branch's individual commits has explicit value. Delete the
   merged branch and move the Project 8 item to the board's completed state.

Keep the ticket synchronized with the board's existing equivalents of ready,
in progress, in review, and done. Do not assume or create exact status names.

Until executable project tooling exists, documentation validation consists at
minimum of reviewing rendered structure, checking relative links and assets,
running `git diff --check`, and inspecting the complete staged diff.

## TruckCMS invariants

Every implementation and review must preserve these v0.1 constraints:

- TruckCMS is an isolated `TruckCMS` Rails engine for new Rails 8.1+ sites.
- Developer-defined Active Record models remain the content models.
- Rails views and REST API v1 resolve the same published revision.
- Draft and unpublished content are denied by default on public Rails and API
  delivery; preview requires separate, revision-scoped, time-limited access.
- Publishing selects a complete immutable revision atomically.
- Rails routing remains authoritative, with explicit precedence and collision
  handling for CMS content routes.
- The portable core must support SQLite, PostgreSQL, and MySQL/MariaDB without
  database-specific behavior.
- Administration uses Rails views, Hotwire, and Tailwind CSS v4 and must support
  the complete editing workflow at 768 by 1024 CSS pixels.
- Authentication, CSRF protection, rich-text sanitization, accessibility, and
  deterministic versioned API output are release requirements, not optional
  hardening.

## Specification review

When asked to review a specification:

1. Compare it with every affected PRD requirement, the v0.1 exclusions, launch
   gates, confirmed product decisions, and open questions.
2. Identify contradictions, missing acceptance criteria, ambiguous ownership,
   unverifiable claims, unstated migrations or compatibility effects, and
   security or draft-exposure risks.
3. Separate known facts from open decisions. Do not fill product gaps by
   assumption.
4. Report findings first, ordered by severity, with precise document locations.
   Then list questions and a short coverage summary.
5. Do not edit an approved specification during a review unless the owner also
   asks for changes.

## Human pull request review

A pull request is not complete when Codex finishes implementation. It is ready
for human review only when the definition of done below is satisfied.

The human reviewer should compare the complete diff with the linked issue,
acceptance criteria, affected PRD requirements, product boundaries, tests,
migrations, configuration, and verification evidence. Review should prioritize
correctness, data safety, authentication and authorization, draft isolation,
revision parity, route precedence, database portability, accessibility, and
regression risk.

Human-requested changes remain part of the same ticket and pull request. Codex
must inspect each current review thread, implement only the agreed changes,
rerun relevant checks, and report what changed. The human reviewer re-reviews
the updated diff and is the only party that may approve it.

## Main branch policy

- All changes to `main` arrive through pull requests linked to approved tickets.
- Direct pushes, force pushes, and branch deletion are prohibited on `main`.
- Require at least one human approval and resolution of review conversations.
- Require repository CI checks once executable checks are available.
- Stale approval should be re-evaluated after material changes to an approved
  pull request.
- Merge only when the branch is current enough to satisfy repository rules and
  all required checks pass.

## Definition of done

Work is ready for a human-reviewed pull request only when:

- the approved acceptance criteria and affected PRD requirements are met;
- tests cover the change and required checks pass, or limitations are clearly
  reported;
- security, data, database, route, API, accessibility, and documentation
  effects have been considered where relevant;
- documentation reflects changed public behavior or developer workflow;
- the issue, code, tests, and affected documentation describe the same behavior;
- the branch contains no unrelated changes or generated secrets; and
- Codex has reviewed the final diff against `origin/main` and the pull request
  links its ticket, explains risks, and includes a concise verification record.
