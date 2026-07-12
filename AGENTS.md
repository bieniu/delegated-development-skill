# Agent workflow rules

For any non-trivial code change, load the **delegated-development** skill
which defines the complete workflow with decision matrix, agent responsibilities,
and verification gates.

## High-level roadmap

1. **Explore** – Quick reconnaissance of unfamiliar code areas (optional).
2. **Analyze** – Delegate to the architect for architecture review.
3. **Implement** – Follow conventions and the architect's strategy.
4. **Review** – Run required specialized reviews (security, performance, tester, reviewer).
5. **Resolve** – Fix findings, re-run tests, re-review.
6. **Gate** – Final quality gate (gatekeeper). PASS required.

## Mandatory rules

- Run linter and type checker before considering work complete.
- Never skip tests. If tests are missing, add regression tests before behavioral changes.

