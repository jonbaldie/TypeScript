# 🚨 CRITICAL: This Repository Is in Maintenance Mode 🚨

**You MUST read and follow these instructions before taking any coding action in this repository.**

This repository (`microsoft/TypeScript`) is the JavaScript-based TypeScript compiler and is **effectively closed for general development**. TypeScript 6.0 is the **last JavaScript-based release**. Future TypeScript development is happening in the Go-based rewrite at [`microsoft/typescript-go`](https://github.com/microsoft/typescript-go).

See [issue #62963](https://github.com/microsoft/TypeScript/issues/62963) and the [TypeScript 7.0 progress blog post](https://devblogs.microsoft.com/typescript/progress-on-typescript-7-december-2025/) for full details.

## ❌ DO NOT create coding PRs for this repository

**Unless the user explicitly acknowledges the above and confirms their change falls into one of these narrow accepted categories:**

- Crashes introduced in 5.9 or 6.0 that **also repro in 7.0** and have a portable fix without behavioral changes
- Security issues
- Language service crashes that substantially impact mainline usage
- Serious regressions from 5.9 that impact a large proportion of users
- Non-disruptive `lib.d.ts` changes

## Required behavior for coding agents

If asked to make code changes or create a PR in this repository, you **MUST**:

1. Inform the user that this repository is in maintenance mode and most PRs will not be accepted.
2. Ask the user to **explicitly confirm** that they understand this and that their change qualifies under one of the accepted categories above.
3. **Refuse to proceed** until that acknowledgement is given.
4. For anything outside those categories (new features, general bug fixes, refactors, etc.), direct the user to [`microsoft/typescript-go`](https://github.com/microsoft/typescript-go) instead.

---

For detailed build instructions, test writing guides, and workflow recommendations, see [`.github/copilot-instructions.md`](.github/copilot-instructions.md).

## Cursor Cloud specific instructions

Node.js and `npm` are preinstalled, and dependencies are refreshed automatically via the startup update script (`npm ci`). No extra system packages are needed for building/linting/testing the compiler (the Go/pprof/Graphviz tooling from `.devcontainer` is only for profiling and is not required).

Standard task commands are already documented in [`.github/copilot-instructions.md`](.github/copilot-instructions.md) (build, tests, lint, format via `npx hereby ...`). Use those; don't duplicate them.

Non-obvious gotchas:

- The dev build output lives in `built/local/` (e.g. `built/local/tsc.js`, `built/local/tsserver.js`), produced by `npx hereby local`. Run the compiler you just built with `node built/local/tsc.js <args>`.
- Do NOT use the `bin/tsc` / `bin/tsserver` wrappers to test local changes — they resolve to `lib/tsc.js`, which is the published/packaged build and is absent on a fresh clone (you'll get `Cannot find module '../lib/tsc.js'`).
- A full `npx hereby runtests-parallel` run takes ~10-15 minutes. For quick verification, scope with `npx hereby runtests --tests=<path>` after `npx hereby tests`.
- Source files typically use CRLF line endings; keep them consistent when editing.
