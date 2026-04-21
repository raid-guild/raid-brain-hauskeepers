# LLM Engineer Prompt Guidance

- The guide can be copied into an LLM system/developer prompt as-is.
- The guide references current repo docs and boundaries.
- The guide encourages reading before editing and tracing data/write flows before changing code.

### Suggested Prompt Block

```md
You are working in the HAUS Admin repo, a Vite + React app for DAOhaus Moloch V3 DAOs.

Before editing:

1. Read `README.md`, `docs/ARCHITECTURE.md`, and `src/AGENT.md`.
2. Then read the nearest `AGENT.md` for the area touched by the bug or feature.
3. Use `src/router.tsx` to map URLs to route files.
4. Prefer route files in `src/app/routes` as entrypoints, but keep feature-specific UI and logic in `src/features/*`.
5. Put reusable DAO data fetching in `src/lib/dao-hooks`.
6. Put reusable transaction execution behavior in `src/lib/tx-builder`.
7. Put proposal/form/contract lego definitions in `src/lib/legos`.
8. Put generic form rendering behavior in `src/lib/form-builder`.
9. Put chain/network metadata in `src/lib/keychain-utils`.
10. Avoid feature-to-feature imports unless there is already an established pattern.
11. Prefer public barrel imports such as `@/lib/dao-hooks`, `@/lib/tx-builder`, and `@/lib/legos`.

When fixing a bug:

1. Start from the user-visible route or feature.
2. Trace data flow through hooks before changing rendering code.
3. Trace write flows through feature utils, legos, and `TXBuilder`.
4. Make the smallest focused change that matches existing patterns.
5. Run `npm run lint` and `npm run build` unless the change is docs-only.
6. Report what changed, what was verified, and any remaining risk.
```
