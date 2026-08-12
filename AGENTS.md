# Agent workflow rules

For any non-trivial code change, load the **delegated-development** skill
which defines the complete workflow with decision matrix, agent responsibilities,
and verification gates.

## High-level roadmap

1. **Explore** – Quick reconnaissance of unfamiliar code areas (optional).
2. **Analyze** – Delegate to the architect for architecture review (if required by the decision matrix).
3. **Implement** – Follow conventions and the architect's strategy (if architect review was performed).
4. **Review** – Run required specialized reviews (security, performance, tester, reviewer).
5. **Resolve** – Fix findings, re-run tests, re-review.
6. **Gate** – Final quality gate (gatekeeper). PASS required.

## Mandatory rules

- Run linter and type checker before considering work complete.
- Never skip tests. If tests are missing, add regression tests before behavioral changes.

## MCP: context7

When you need current documentation for a library, framework, SDK, API, CLI
tool, or configuration syntax, use the `context7` MCP tools (`context7_*`)
instead of relying on memory or web search — training data may be outdated.

Typical use: API syntax, setup/configuration, version migration, library-specific debugging.

Do not use for: general coding advice, code review, or business logic questions.

Available to the main agent and to the `architect`, `performance`, and `tester`
subagents. The `reviewer`, `security`, and `gatekeeper` subagents have it
disabled.

## MCP: grep-mcp

SearchGitHub code across millions of repositories (via the grep.app API)
using the `grep-mcp` server tools (`grep-mcp_*`).

The main tool is `grep-mcp_grep_query`:

- `query` (required) – the code pattern to search for
- `language` (optional) – filter by programming language (e.g. "Python")
- `repo` (optional) – restrict to a single repository ("owner/repo")
- `path` (optional) – restrict to a directory (e.g. "src/")

Typical use: finding prior art or reference implementations of a pattern or
API, checking established usage of a library across open-source projects,
or verifying that a code pattern is idiomatic.

Do not use for: searching the current project (use local Grep/Glob instead),
code reviews, or general coding advice.

Available to the main agent and to the `architect`, `performance`, and `tester`
subagents. The `reviewer`, `security`, and `gatekeeper` subagents have it
disabled.

