# TruckCMS Agent Instructions

## Scope

These instructions apply to the entire repository. More specific `AGENTS.md`
files may add directory-level rules but may not weaken the product, safety, or
review requirements in this file.

## Project ownership

- The project owner controls product decisions, acceptance criteria, pull
  request creation, approval, and merge decisions.
- GitHub Project 8 is the planning board for approved work:
  <https://github.com/users/jedt3d/projects/8>
- Codex may analyze, plan, implement, test, document, and review work requested
  by the owner.
- Codex must not open or merge a pull request, push directly to `main`, change
  Project 8, resolve review threads, or publish a GitHub review unless the owner
  explicitly authorizes that specific remote action.
- The owner creates pull requests. Codex prepares a pushed feature branch and a
  proposed pull request title, description, and verification summary.

## Required product context

Before reviewing a specification, planning a feature, changing behavior, or
reviewing a pull request, read these files in order:

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

## Development workflow

1. Identify the approved Project 8 item or owner request and its acceptance
   criteria. Do not enlarge the task silently.
2. Read the required product context and map the work to applicable PRD
   requirements and launch gates.
3. Inspect the relevant source, configuration, tests, logs, and nearby code.
   Diagnose the root cause before proposing or making a change.
4. Post a short, auditable plan before multi-step work. Identify uncertainties
   and decisions that require the owner.
5. Start from the latest `origin/main` and create a focused branch named
   `codex/<project-item-or-issue>-<short-slug>`. Never develop on `main`.
6. Make the smallest complete change. Preserve existing architecture and user
   work; do not mix refactors, dependency upgrades, or formatting unrelated to
   the task.
7. Add or update tests for changed behavior. Run the narrowest relevant checks
   first, then the repository's required full checks. Discover commands from
   repository configuration; do not invent commands or flags.
8. Re-read the diff against `origin/main`. Check security, migrations,
   compatibility, documentation, and accidental files before committing.
9. Commit only task files in focused commits and push only the feature branch.
   Report the commit, checks run, known limitations, and proposed PR text to
   the owner.
10. The owner opens the pull request, makes the final product decision, and
    decides when to merge.

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

## Pull request review

Codex reviews pull requests authored by the owner only when requested. For each
review:

1. Fetch the current base and head and inspect the complete diff against the
   pull request base, not only the latest commit.
2. Read the linked Project 8 item, pull request description, affected product
   documents, implementation, tests, migrations, and configuration.
3. Verify scope and acceptance criteria, then prioritize correctness, data
   safety, authentication and authorization, draft isolation, revision parity,
   route precedence, database portability, accessibility, and regression risk.
4. Run relevant checks and distinguish observed failures from untested risk.
5. Report actionable findings first, ordered as `blocking`, `major`, or `minor`,
   using `path:line` references and explaining the user-visible or operational
   consequence. Avoid style-only comments unless a repository rule requires
   them.
6. If there are no findings, state that explicitly and list residual risks or
   checks that could not be run.
7. Keep the review local unless the owner explicitly authorizes posting it to
   GitHub. Posting comments, submitting a review, or resolving threads are
   separate remote actions and require separate authorization.

## Definition of done

Work is ready for the owner to open a pull request only when:

- the approved acceptance criteria and affected PRD requirements are met;
- tests cover the change and required checks pass, or limitations are clearly
  reported;
- security, data, database, route, API, accessibility, and documentation
  effects have been considered where relevant;
- documentation reflects changed public behavior or developer workflow;
- the branch contains no unrelated changes or generated secrets; and
- Codex has reviewed the final diff against `origin/main` and supplied a concise
  pull request summary and verification record.
