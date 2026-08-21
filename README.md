# TruckCMS

TruckCMS is professional editorial content management built for Rails—native
to Rails models and views, and ready for API delivery when a website needs it.

## Project status

TruckCMS is in the specification and repository-bootstrap phase. The v0.1
product boundary is defined, but the Rails engine and starter application have
not yet been implemented.

The v0.1 promise is:

> A Rails developer can start a new TruckCMS website where an administrator
> composes structured pages, previews drafts, publishes complete revisions,
> and delivers the same live content through Rails views and a versioned API.

## Product documentation

- [Product Requirements Document](docs/PRD.md) — mandatory v0.1 requirements,
  exclusions, launch gates, and delivery sequence.
- [Product Concept](docs/PRODUCT_CONCEPT.md) — vision, audience, product
  rationale, confirmed decisions, and open strategic questions.
- [Agent instructions](AGENTS.md) — the ticket-driven implementation and human
  pull-request-review process.

Work is planned in
[GitHub Project 8](https://github.com/users/jedt3d/projects/8).

## v0.1 scope

TruckCMS v0.1 targets new Rails 8.1+ content websites. It will provide an
isolated Rails engine and supported starter with:

- developer-defined Active Record content models and a supplied `Page` model;
- typed BlockStream content with heading, rich-text, image, and call-to-action
  blocks;
- immutable revisions, draft-safe preview, publish, and unpublish;
- public Rails rendering and a versioned read-only REST API that expose the
  same published revision;
- a Rails, Hotwire, and Tailwind CSS v4 administration interface; and
- portable behavior across SQLite, PostgreSQL, and MySQL/MariaDB.

See the [PRD](docs/PRD.md) for the complete release boundary. Features absent
from its mandatory requirements are not v0.1 work.

## GitHub development workflow

TruckCMS uses ticket-driven GitHub Flow:

1. A human creates or approves a GitHub issue and adds it to Project 8 with
   scope, acceptance criteria, and applicable PRD requirements.
2. Codex creates an issue-linked branch from the latest `main`, implements the
   ticket, adds tests and documentation, and runs the required checks.
3. Codex self-reviews the full diff, pushes the branch, and opens a pull request
   that closes the issue.
4. A human reviews the pull request and CI evidence. Codex addresses requested
   changes on the same branch.
5. Only the human approves and merges into `main`; the merged branch is then
   deleted and the project item is completed.

Direct development and force pushes on `main` are prohibited. See
[AGENTS.md](AGENTS.md) for branch naming, review criteria, product invariants,
and the definition of done.

## License

TruckCMS is available under the [MIT License](LICENSE).
