# Agent workflow rules

## Delegation requirements

Before implementing any non-trivial change:

1. Analyze whether the task benefits from independent review.
2. Delegate investigation to a sub-agent when:
   - the change affects multiple files,
   - the architecture is unclear,
   - the change introduces a new feature,
   - the change modifies security-sensitive code,
   - tests are missing.

## Implementation workflow

For every significant code change:

1. Ask an analysis sub-agent to inspect the repository and identify risks.
2. Implement the change only after understanding the existing design.
3. After implementation, always ask a review sub-agent to verify:
   - correctness,
   - edge cases,
   - regression risks,
   - performance implications,
   - test coverage.

## Verification policy

Never consider a task complete after editing files.

Completion requires:

- running relevant tests,
- reviewing changed files,
- receiving feedback from a reviewer sub-agent,
- fixing all valid findings.

If reviewer feedback identifies issues, repeat the verification cycle.
