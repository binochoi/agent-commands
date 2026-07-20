---
description: Actually run the checks instead of assuming they pass
allowed-tools: Bash, Read, Grep, Glob
---

Scope: $ARGUMENTS

Verify that the recent changes actually work. Do not reason about
whether they should work. Execute and observe.

Steps:
- Identify the project's test, lint, type-check, and build commands
  by reading the package manifest and CI configuration.
- Run each one. Capture the real output.
- If a command does not exist, say so rather than substituting a guess.

Rules:
- Do not ask for confirmation before running read-only checks.
- Do not run anything that deploys, publishes, or mutates remote state.
- Paste the actual command and its exit status for each check.
- End with a verdict line: PASS or FAIL, plus the count of failures.
- Never report success for a command you did not run.
