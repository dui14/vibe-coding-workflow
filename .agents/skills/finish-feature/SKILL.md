---
name: finish-feature
description: Validate, document, and record a completed feature or task.
---

# Finish Feature

## Procedure

1. Review the implementation against the requested specification.
2. Run relevant tests, type checks, builds, and linters.
3. Fix issues caused by the current task.
4. Update relevant documentation.
5. Update `spec/progress.md`.
6. Record important architectural or implementation decisions.
7. Verify that no temporary code, TODOs, debug output, or unrelated changes remain.

## Rules

- Document only verified behavior.
- Do not claim validation that was not actually run.
- Keep documentation synchronized with the implementation.
- Keep `spec/progress.md` concise.
- Do not rewrite unrelated documentation.