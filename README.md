# agentic-support-open-elements

A [Claude Code](https://claude.com/claude-code) **plugin** that bundles **Open Elements company knowledge** and the **Open Elements fullstack build conventions**. It gives any Open Elements project the same baseline of company context, brand identity, and stack conventions.

This plugin is a focused extract of skills from [`claude-base`](https://github.com/OpenElementsLabs/claude-base); install it when you want the Open Elements company context and fullstack conventions without the full base configuration.

## What's included

### Company & product knowledge

| Skill | What it does |
| --- | --- |
| `open-elements-info` | Company profile: founder Hendrik Ebbers, team, mission, business areas, foundation memberships, contact details. |
| `open-elements-brand-guidelines` | Brand colors, typography, logos, illustration style, and sample artifacts — including bundled TTF fonts, logo files, and sample decks. |
| `support-and-care-info` | The Support & Care offering: supported Java components, business model, CRA compliance — including the logo and marketing flyer. |

### Fullstack build conventions

| Skill | What it does |
| --- | --- |
| `fullstack-architecture-setup` | Independent backend + frontend in one repo, wired via Docker Compose, with optional OAuth2/OIDC. |
| `java-backend` | Java backend conventions: framework choice, feature-based packages, REST/OpenAPI, JPA/Flyway/PostgreSQL, GDPR, layer-specific testing. |
| `typescript-best-practices` | React/Next.js/Tailwind/shadcn stack, code style, testing, i18n, logging, error handling, and Next.js build pitfalls. |
| `mkdocs-setup` | Project documentation with MkDocs + Material, published to GitHub Pages. |

`.mcp.json` ships two MCP servers used by these skills: **shadcn** (browse/install shadcn/ui components) and **maven-central** (look up Maven dependency versions).

## Installation

Install from inside Claude Code:

```
/plugin marketplace add OpenElementsLabs/agentic-support-open-elements
/plugin install agentic-support-open-elements@open-elements
```

Then restart Claude Code (or run `/reload-plugins`).

Skills are **namespaced** under the plugin, e.g. `/agentic-support-open-elements:java-backend`, `/agentic-support-open-elements:open-elements-brand-guidelines`.

## A note on cross-references

A few of the bundled skills point to companion skills that live in `claude-base` but are **not** shipped here — for example `java-best-practices` (general Java conventions), `project-setup`, `github-actions-setup`, and `eclipse-info`. Those references are intentional prose pointers. If you want the complete, self-referential set, install [`claude-base`](https://github.com/OpenElementsLabs/claude-base) as well.

## Keeping up to date

Because the plugin is versioned, updates arrive when the `version` in `plugin.json` is bumped. Pull the latest release with:

```
/plugin marketplace update open-elements
```

## Repository layout

```
agentic-support-open-elements/
├── .claude-plugin/
│   ├── plugin.json          # plugin manifest
│   └── marketplace.json     # marketplace catalog (this repo is its own marketplace)
├── skills/                  # all skills, flat (Claude Code discovers them here)
├── conventions/             # shared convention docs referenced by skills
├── .mcp.json                # shadcn + maven-central MCP servers
└── CHANGELOG.md
```

## For maintainers

- **Releasing:** bump `version` in **both** `.claude-plugin/plugin.json` and the `agentic-support-open-elements` entry in `.claude-plugin/marketplace.json`, update `CHANGELOG.md`, and tag the release. Validate with `claude plugin validate ./ --strict`.

## License

This project is licensed under the Apache License 2.0 — see [LICENSE](LICENSE) for details.
