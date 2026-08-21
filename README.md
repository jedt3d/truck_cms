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
- [Agent instructions](AGENTS.md) — the Codex development, specification-review,
  and pull-request-review process.

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

1. The owner defines and approves work in Project 8 or an explicit task.
2. Codex reads the PRD and product concept, inspects the repository, and works
   on a focused `codex/...` branch.
3. Codex implements, verifies, documents, commits, and pushes that feature
   branch with a proposed pull request summary.
4. The owner creates the pull request and retains approval and merge authority.
5. On request, Codex reviews the owner-authored pull request against the linked
   project item, product specifications, full diff, and test evidence.

See [AGENTS.md](AGENTS.md) for the binding workflow, review criteria, product
invariants, and definition of done.

## License

TruckCMS is available under the [MIT License](LICENSE).
