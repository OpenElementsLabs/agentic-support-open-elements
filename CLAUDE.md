# Agentic Support Open Elements — Project Rules

This repository **is** a Claude Code plugin: it bundles Open Elements company knowledge and the Open Elements fullstack build conventions as reusable skills, and distributes them through its own marketplace.

## Purpose of this project

The goal is to give any Open Elements project a ready-made base of company/brand knowledge and stack conventions. This plugin is a focused extract of skills from [`claude-base`](https://github.com/OpenElementsLabs/claude-base); install it when you want the Open Elements company context and fullstack conventions without the full base configuration. When working on this repository, keep in mind that every skill you write here will be used across many different projects.

## Repository Structure

The repository root is the plugin root (and the marketplace root).

- `.claude-plugin/plugin.json` — plugin manifest (name, version, metadata)
- `.claude-plugin/marketplace.json` — marketplace catalog (lists this plugin, `source: "./"`)
- `skills/` — reusable Claude Code skills, flat (`skills/<name>/SKILL.md`); discovered automatically
- `conventions/` — shared convention documents referenced by skills via `${CLAUDE_PLUGIN_ROOT}/conventions/…`
- `.mcp.json` — MCP servers shipped with the plugin
- `README.md` — public-facing documentation for users of this plugin
- `CHANGELOG.md` — release history

## Skills

**Company & product knowledge:**

- `open-elements-info` — company profile, founder, business areas, foundation memberships, contact details.
- `open-elements-brand-guidelines` — brand colors, typography, logos, illustration style, and sample artifacts.
- `support-and-care-info` — the Support & Care offering: supported Java components, business model, CRA compliance.

**Stack & build conventions:**

- `project-setup` — set up or review a project's baseline: project type, `.editorconfig`, repository setup, routing to the right stack skill.
- `fullstack-architecture-setup` — independent backend + frontend in one repo, wired via Docker Compose, optional OAuth2/OIDC.
- `java-backend` — Java backend conventions: frameworks, package structure, REST/OpenAPI, JPA/Flyway, GDPR, testing.
- `java-best-practices` — general Java conventions: code style, build tools, testing, logging, null handling, immutability, modules, SPI, async.
- `typescript-best-practices` — React/Next.js/Tailwind/shadcn stack, code style, testing, i18n, error handling.
- `mkdocs-setup` — project documentation with MkDocs + Material, published to GitHub Pages.
- `github-actions-setup` — CI/CD workflows (`build.yml`, `docs.yml`, `release-drafter.yml`) for Java, TypeScript, and fullstack projects.

The `project-setup` skill references `frontend-design`, which lives in `claude-base` but is **not** bundled here. That reference is an intentional prose pointer; install `claude-base` for the full set.

## Distribution

The plugin is installed from inside Claude Code:

```
/plugin marketplace add OpenElementsLabs/agentic-support-open-elements
/plugin install agentic-support-open-elements@open-elements-public
```

Skills are namespaced under the plugin, e.g. `/agentic-support-open-elements:java-backend`.

**Releasing:** bump `version` in **both** `.claude-plugin/plugin.json` and the `agentic-support-open-elements` entry in `.claude-plugin/marketplace.json`, update `CHANGELOG.md`, tag the release, and validate with `claude plugin validate ./ --strict`. Users only receive an update when the version is bumped.

A plugin-root `CLAUDE.md` is not loaded as context, so ship guidance as skills or `conventions/` — not in this file.

## Writing Guidelines

### For skills (`skills/<name>/SKILL.md`)

- Each skill must have valid frontmatter with a `name` (kebab-case, matching its directory) and a `description`, plus a clear H1 title.
- Keep skills focused on a single task. Do not combine unrelated actions into one skill.
- Reference bundled files (conventions, assets) with `${CLAUDE_PLUGIN_ROOT}/…`, never with `../` traversal or absolute paths — the plugin is copied to a cache on install.
- Preserve the `metadata` frontmatter block (`source`, `author`) so provenance tooling keeps working.

## Quality Standards

- All files must be valid Markdown with no formatting errors.
- Use consistent heading levels (H1 for title, H2 for sections, H3 for subsections).
- No trailing whitespace, no tabs for indentation in Markdown files.
- Run `claude plugin validate ./ --strict` after structural changes.

## What NOT to include

- No project-specific configurations (build scripts, CI pipelines, IDE settings).
- No absolute file paths or machine-specific references.
- No secrets, credentials, or environment-specific values.
