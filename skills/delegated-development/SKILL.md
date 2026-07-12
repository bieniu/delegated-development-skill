---

name: delegated-development
description: Multi-stage software development workflow using specialized sub-agents for architecture, security, performance, testing and independent review.
------------------------------------------------------------------------------------------------------------------------------------------------------------

# Delegated Development Workflow

Use this workflow whenever a task requires writing or modifying code beyond a trivial change.

The objective is to improve implementation quality through independent analysis and verification by specialized sub-agents.

---

# Agent Responsibilities

## architect

Analyzes the existing codebase before implementation.

Responsible for:

* understanding the current architecture
* identifying affected components
* identifying implementation risks
* recommending the safest implementation strategy

Never modifies code.

---

## explore

Fast codebase exploration for quick reconnaissance.

Use when:

* the change affects an unfamiliar area of the codebase
* you need to quickly find relevant files before deeper analysis
* the change is small and may not warrant full architect analysis

Has access to read and search tools only – never modifies code.

---

## security

Reviews the implementation from a security perspective.

Focus areas:

* authentication
* authorization
* input validation
* output encoding
* injection vulnerabilities (SQL, command, NoSQL)
* secret management
* cryptography misuse
* insecure defaults
* unsafe APIs
* dependency risks
* privilege escalation

---

## performance

Reviews runtime efficiency and scalability.

Focus areas:

* algorithm complexity
* CPU usage
* memory allocations
* unnecessary object creation
* repeated computations
* disk I/O
* database efficiency
* network efficiency
* caching opportunities
* concurrency
* scalability
* locking contention

Avoid premature optimization.

---

## tester

Evaluates the quality of automated testing.

Focus areas:

* unit tests
* integration tests
* regression protection
* edge cases
* boundary conditions
* negative scenarios
* maintainability of tests

---

## reviewer

Performs an independent software engineering review.

Focus areas:

* implementation correctness
* maintainability
* readability
* repository conventions
* API compatibility
* documentation
* simplicity
* code duplication

Assume test quality has already been reviewed by the tester.

---

## gatekeeper

Performs the final quality gate.

Does **not** repeat previous reviews.

Verifies that:

* required reviews were completed
* blocking issues were resolved
* tests were executed
* the implementation is ready to deliver

Returns only:

* PASS
* FAIL

with explanation.

---

# Workflow

## Phase 1 – Determine Required Reviews

Determine which specialized reviews are required using the following decision matrix.

| Change Type                          | Architect | Security      | Performance   | Tester | Reviewer | Gatekeeper |
| ------------------------------------ | --------- | ------------- | ------------- | ------------- | -------- | ---------- |
| Documentation only                   | No        | No            | No            | No            | Yes      | Yes        |
| Small refactoring                    | Yes       | No            | Yes           | Yes           | Yes      | Yes        |
| Bug fix                              | Yes       | If applicable | If applicable | Yes           | Yes      | Yes        |
| New feature                          | Yes       | Yes           | Yes           | Yes           | Yes      | Yes        |
| Public API change                    | Yes       | Yes           | Yes           | Yes           | Yes      | Yes        |
| Dependency updates                   | Yes       | Yes           | No            | Yes           | Yes      | Yes        |
| Infrastructure / CI / Docker / Cloud | Yes       | Yes           | If applicable | Yes           | Yes      | Yes        |

If uncertain, perform the review.

---

## Phase 1a – Optional Codebase Exploration

If the change affects an unfamiliar area, delegate to **explore** for quick reconnaissance.

explore can:

* locate relevant files and modules
* identify existing patterns and conventions
* provide enough context to plan the next steps

Skip this step if the codebase is already well understood.

Proceed directly to Phase 2 (or to implementation for trivial changes).

---

## Phase 2 – Architecture Analysis

If required by the decision matrix:

Delegate to the **architect**.

Do not begin implementation until the existing architecture has been understood.

Review:

* affected modules
* dependencies
* existing design
* implementation risks
* recommended approach

---

## Phase 3 – Implementation

Implement the solution by following:

* repository conventions
* project architecture
* existing design patterns
* coding standards

Avoid unnecessary refactoring.

---

## Phase 4 – Specialized Reviews

Invoke each required reviewer independently.

### Security Review

Delegate to **security**.

Review:

* authentication
* authorization
* input validation
* output encoding
* injection vulnerabilities (SQL, command, NoSQL)
* secret management
* cryptography misuse
* insecure defaults
* unsafe APIs
* dependency risks
* privilege escalation

---

### Performance Review

Delegate to **performance**.

Review:

* algorithm complexity
* CPU usage
* memory allocations
* unnecessary object creation
* repeated computations
* disk I/O
* database efficiency
* network efficiency
* caching opportunities
* concurrency
* scalability
* locking contention

Only report issues with practical impact.

---

### Testing Review

Delegate to **tester**.

Review:

* test coverage
* regression protection
* missing unit tests
* missing integration tests
* edge cases
* boundary conditions
* negative scenarios
* maintainability of tests

Recommend the minimum additional tests necessary to reduce regression risk.

---

### Code Review

Delegate to **reviewer**.

Review:

* correctness
* maintainability
* readability
* repository conventions
* API compatibility
* documentation
* code duplication
* simplicity

---

## Phase 5 – Resolve Findings

For every valid finding:

1. Fix the implementation.
2. Update or add tests if necessary.
3. Re-run relevant tests.
4. Ask the corresponding reviewer to verify the fix.

Repeat until all blocking findings are resolved.

---

## Phase 6 – Execute Tests

Before completion:

* run all relevant automated tests
* ensure newly added functionality is covered by tests
* ensure regression tests pass

If existing code is modified and is not covered by tests, create regression tests before implementing behavioral changes whenever practical.

---

## Phase 7 – Final Quality Gate

Delegate to **gatekeeper**.

The gatekeeper must verify that:

* architecture review completed (when required)
* security review completed (when required)
* performance review completed (when required)
* testing review completed (when required)
* code review completed
* tests executed successfully
* blocking findings resolved

The task is complete only if the gatekeeper returns:

PASS

Otherwise, continue resolving findings until PASS is achieved.

