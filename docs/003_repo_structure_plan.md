# Repo Structure Simplification Plan

**Goal:** Simplify the repository structure so developers and LLM agents can find code by intent, not by historical accident. The main objective is to reduce duplicate concepts such as multiple `utils`, `hooks`, and lego entrypoints while preserving behavior and allowing the cleanup to land in small, low-risk phases.

**Date:** April 14, 2026

---

## Status Snapshot

Completed during the current cleanup pass:

- Phase 0 - Guardrails and inventory
- Phase 1 - Remove duplicate and misleading artifacts
- Phase 2 - Unify lego entry points
- Phase 3 - Split shared utils from feature utils
- Phase 4 - Clarify app hooks versus data hooks
- Phase 5 - Introduce feature-based organization in components
- Phase 6 - Normalize app shell naming

Current top-level structure:

```text
src/
  app/
    components/
    hooks/
    layouts/
    routes/
  features/
    dao/
    home/
    member/
    proposal/
    safe/
    settings/
    summon/
  lib/
    abis/
    dao-hooks/
    data-fetch-utils/
    form-builder/
    keychain-utils/
    legos/
    tx-builder/
    ui/
    utils/
```

Notes:

- The old top-level `src/components`, `src/hooks`, `src/layout`, `src/pages`, `src/utils`, `src/legos`, and `src/types` structures have been retired
- `src/lib/dao-hooks` remains the shared DAO data/query layer by design

---

## Problems To Address

### Confirmed issues

1. `src/legos/legoConfig.ts` is separated from the rest of the lego system in `src/lib/legos/`
2. Both `src/utils/` and `src/lib/utils/` exist, but they serve overlapping "helper" roles
3. Both `src/hooks/` and `src/lib/dao-hooks/hooks/` exist, but they represent different layers while using the same name

### Additional opportunities discovered during review

1. Duplicate component names exist at multiple levels:
   - `src/components/ProposalActions.tsx` and `src/components/ProposalActions/ProposalActions.tsx`
   - `src/components/ProposalActionData.tsx` and `src/components/ProposalActionData/ProposalActionData.tsx`
2. Duplicate implementation exists in:
   - `src/lib/form-builder/components/Logger.tsx`
   - `src/lib/form-builder/base/components/Logger.tsx`
3. Duplicate asset exists in:
   - `src/assets/wallet_connect.svg`
   - `src/lib/legos/assets/wallet_connect.svg`
4. `src/types/index.ts` appears to be an unused alias layer over `src/lib/dao-hooks`
5. The repo still uses top-level aliases that encourage duplicate concepts:
   - `@/legos`
   - `@/utils`
   - `@/hooks`
6. `src/components/` is becoming a large mixed folder containing feature components, reusable app components, and route-specific composition

---

## Target Principles

These principles should guide every phase:

1. `src/lib/*` should contain reusable or shared modules
2. App-specific logic should not live in parallel top-level folders when a clearer feature or app location exists
3. Folder names should describe layer or domain consistently
4. Barrels and aliases should reduce ambiguity, not create alternative entrypoints
5. Each phase should be safe to ship independently

---

## Recommended Target Structure

This was the intended direction and is now mostly reflected in the repo:

```text
src/
  app/
    layouts/
    routes/
  features/
    dao/
      hooks/
    home/
      utils/
    proposal/
      components/
      legos/
    summon/
      components/
      utils/
  lib/
    abis/
    dao-hooks/
    form-builder/
    keychain-utils/
    legos/
    tx-builder/
    ui/
    utils/
```

### Interpretation of the target

- `src/lib/*` remains the place for shared modules copied or adapted from DAOhaus libraries
- `src/app/*` becomes the home for application shell concerns like layouts and routes
- `src/features/*` becomes the place for app-specific domains like summon, proposal, and dashboard behavior

This plan did not require moving everything into `features` immediately. The migration was applied incrementally.

---

## Phase 0 - Guardrails And Inventory

**Goal:** Make the cleanup safer before moving files.

**Status:** Completed

### Tasks

1. Create this plan and use it as the migration checklist
2. Record current aliases and import patterns that will be changed
3. Add or update documentation describing folder intent for:
   - `src/lib`
   - `src/components`
   - `src/hooks`
   - `src/utils`
4. Identify all imports using:
   - `@/legos/*`
   - `@/utils/*`
   - `@/hooks/*`
5. Capture current validation commands for each phase:
   - typecheck
   - lint, if available
   - build

### Success criteria

- We have a known list of imports affected by each move
- Each later phase can be validated with repeatable commands

---

## Phase 1 - Remove Duplicate And Misleading Artifacts

**Goal:** Eliminate files that create confusion without needing a broad reorg.

**Status:** Completed

### Tasks

1. Decide whether the root-level files below are obsolete, and remove or replace them if they are not part of active imports:
   - `src/components/ProposalActions.tsx`
   - `src/components/ProposalActionData.tsx`
2. Collapse the duplicated form builder logger implementation into one source of truth:
   - keep either the base logger or the component logger
   - re-export from the other location if needed for compatibility
3. Keep one `wallet_connect.svg` asset and remove the duplicate copy
4. Remove `src/types/index.ts` and the `@/types` alias if it is truly unused
5. Fix small naming paper cuts discovered during cleanup, such as inconsistent file naming that makes navigation harder

### Success criteria

- No duplicate components with the same conceptual name remain unless intentionally documented
- No duplicate assets or identical utility implementations remain
- The alias surface is slightly smaller and clearer

### Risk level

Low

---

## Phase 2 - Unify Lego Entry Points

**Goal:** Make the lego system discoverable from one obvious place.

**Status:** Completed

### Current problem

- `src/legos/legoConfig.ts` is app-specific
- `src/lib/legos/` contains the actual lego library implementation
- The split makes it unclear whether new lego-related work belongs in `src/legos` or `src/lib/legos`

### Recommended direction

Original options:

1. Preferred: move app-specific lego wiring into a feature-specific location such as `src/features/proposal/legos.ts` or `src/features/proposal/legos/index.ts`
2. Minimal-change alternative: move `src/legos/legoConfig.ts` into `src/lib/legos/app.ts` or `src/lib/legos/config.ts`

### Tasks

1. Move `src/legos/legoConfig.ts` to the chosen target location
2. Update all imports currently using `@/legos/legoConfig`
3. Remove the `@/legos` alias from Vite and TypeScript if it is no longer needed
4. Add a single stable import path for app lego usage
5. Document the distinction:
   - shared lego primitives live in `src/lib/legos`
   - app-specific composition lives in feature code or the app-specific lego adapter

### Success criteria

- Developers can find all lego-related code from one primary root
- There is no top-level `src/legos/` folder competing with `src/lib/legos/`

### Risk level

Low to medium

---

## Phase 3 - Split Shared Utils From Feature Utils Clearly

**Goal:** Remove the ambiguous two-utils model.

**Status:** Completed

### Current problem

- `src/lib/utils/` is the shared utility surface used across the app
- `src/utils/` contains app-specific helpers, but its generic name suggests a second general utility home

### Recommended direction

Keep `src/lib/utils/` as the only generic shared utils namespace.

Move app-specific helpers out of `src/utils/` into domain-specific homes:

- `src/utils/chainIds.ts`
  - likely move into `src/lib/keychain-utils/` if it is broadly reusable
- `src/utils/hub.ts`
  - move into `src/features/home/utils/`
- `src/utils/summonCommon.ts`
  - move into `src/features/summon/utils/`
- `src/utils/summonFormKeys.ts`
  - move into `src/features/summon/utils/`
- `src/utils/summonTx.ts`
  - move into `src/features/summon/utils/`

### Tasks

1. Categorize each file in `src/utils/` as either shared or feature-specific
2. Move feature-specific files to `src/features/<feature>/utils/`
3. Move any truly shared cross-domain files into `src/lib/*` where they belong
4. Update imports gradually by domain
5. Remove the `@/utils` alias after the last migration

### Success criteria

- There is only one generic shared utils namespace
- Feature helpers are colocated with the feature they support
- New helper placement is obvious to contributors

### Risk level

Medium

---

## Phase 4 - Clarify App Hooks Versus Data Hooks

**Goal:** Make the hook layer understandable by naming and location.

**Status:** Completed

### Current problem

- `src/lib/dao-hooks/hooks` contains library data hooks
- `src/hooks` contains app wrapper hooks and route-context hooks
- Both are called `hooks`, but they represent different abstraction levels

### Recommended direction

Keep `src/lib/dao-hooks` as the shared data library.

Rename or relocate `src/hooks` so it clearly represents app or domain hooks. Preferred options:

1. `src/features/dao/hooks/`
2. `src/app/hooks/`

The original contents suggested `src/features/dao/hooks/` was the better fit for:

- `useDaoData`
- `useConnectedMember`

Applied result:

- `useCurrentDao` moved to `src/app/hooks/`
- `useDaoData` moved to `src/features/dao/hooks/`
- `useConnectedMember` moved to `src/features/dao/hooks/`
- `useProfile` moved to `src/app/hooks/`
- `useSafeBalances` moved to `src/features/safe/hooks/`

`useProfile` and `useSafeBalances` were evaluated independently:

- if shared, move closer to the consuming feature or a more specific shared module
- if app-level, keep under `src/app/hooks/`

### Tasks

1. Choose the new home for current app hooks
2. Move files from `src/hooks/` to the new location
3. Keep `src/lib/dao-hooks/index.ts` as the public entrypoint for shared data hooks
4. Avoid deep imports from `src/lib/dao-hooks/hooks/*` outside that library
5. Update aliases and imports after the move

### Success criteria

- The difference between app hooks and shared data hooks is visible from file paths alone
- There is no top-level `src/hooks/` competing conceptually with `src/lib/dao-hooks/hooks/`

### Risk level

Medium

---

## Phase 5 - Introduce Feature-Based Organization In `src/components`

**Goal:** Reduce the size and ambiguity of the flat `src/components/` folder.

**Status:** Completed

### Current problem

`src/components/` mixes:

- proposal-related components
- member-related components
- safe-related components
- settings-related components
- home/dashboard components
- summon feature components
- general app components like empty states and boundaries

Some feature grouping already existed, which provided the starting point:

- `src/components/Summon`
- `src/components/ProposalActions`
- `src/components/ProposalActionData`

### Recommended direction

Gradually move toward domain grouping, for example:

```text
src/features/
  home/components/
  member/components/
  proposal/components/
  safe/components/
  settings/components/
  summon/components/
src/app/components/
  EmptyState.tsx
  ErrorBoundary.tsx
  SearchInput.tsx
  SortDropdown.tsx
```

### Tasks

1. Identify true app-level shared components versus domain components
2. Move one domain at a time, starting with the easiest:
   - home
   - proposal
   - member
   - safe
   - settings
3. Keep `src/components/Summon` as a migration model for feature colocation
4. Leave stable re-export barrels behind temporarily if that reduces churn

### Success criteria

- Most components can be found by domain instead of by scanning a long flat folder
- Shared app-level components are clearly separate from feature components

### Risk level

Medium to high

---

## Phase 6 - Normalize App Shell Naming

**Goal:** Make the app shell layer more obvious.

**Status:** Completed

### Current opportunity

`src/layout/` works, but it sits beside `src/lib/ui/components/layouts/`, which creates another naming overlap.

### Recommended direction

Applied result:

- `src/layout/` -> `src/app/layouts/`
- `src/pages/` -> `src/app/routes/`

This phase landed together with the route move because the repo had already converged on the `app` namespace.

### Tasks

1. Move app layout files to `src/app/layouts/`
2. Update aliases and imports
3. Decide whether `src/pages` should also move in the same phase or a later one

### Success criteria

- App shell code has a clearly labeled home
- Contributors can distinguish app layouts from UI library layout primitives immediately

### Risk level

Low to medium

---

## Phase 7 - Simplify Alias Surface

**Goal:** Make aliases reinforce the final structure instead of preserving old topology.

**Status:** Completed

### Recommended end state

Prefer aliases that map to stable, meaningful roots:

- `@/lib/*`
- `@/app/*`
- `@/features/*`
- optionally `@/assets/*`

Avoid aliases that recreate old ambiguity:

- `@/utils/*`
- `@/hooks/*`
- `@/legos/*`
- `@/types`
- `@/components/*`
- `@/pages/*`
- `@/layout/*`
- `@/routes/*`
- `@/layouts/*`

### Tasks

1. Remove deprecated aliases after each migrated area is complete
2. Update `vite.config.ts`
3. Update `tsconfig.app.json`
4. Add a short contributor note on preferred import style

### Success criteria

- Aliases describe architecture clearly
- New files have an obvious import strategy

### Risk level

Low

---

## Execution Strategy

### Recommended order

1. Phase 1 - remove duplicate and misleading artifacts
2. Phase 2 - unify lego entry points
3. Phase 3 - simplify utils
4. Phase 4 - clarify hooks
5. Phase 5 - component domain grouping
6. Phase 6 - normalize app shell naming
7. Phase 7 - simplify aliases and document conventions

### Why this order

1. It starts with low-risk cleanup that improves signal immediately
2. It resolves the most confusing duplicate concepts before broader moves
3. It delays higher-churn component and app-shell reorganization until naming and utility boundaries are clearer

---

## Validation Per Phase

After each phase:

1. Run typecheck
2. Run build
3. Run lint if configured
4. Use ripgrep to confirm old import roots are gone
5. Spot-check key user flows affected by the moved files

### Key flows to validate during the full migration

1. Proposal list and proposal detail pages
2. New proposal flow
3. Update settings flow
4. Rage quit flow
5. Summon flow
6. Home dashboard and DAO list views

---

## Non-Goals

These items should not be bundled into this cleanup unless they directly support the migration:

1. Rewriting business logic without a structure-related reason
2. Replacing shared DAOhaus-derived library code with new custom implementations
3. Large UI redesigns
4. Feature behavior changes

---

## Open Decisions

These should be resolved before or during implementation:

1. Should app-specific lego wiring remain at `src/lib/legos/config.ts`, or eventually move into a proposal feature namespace?
2. Should `src/lib/dao-hooks` keep its current domain-specific name, or only be renamed later as part of a broader shared-data strategy?
3. Where should local `AGENT.md` files live first: `src/`, `src/app/`, or individual feature folders?
4. Do we want compatibility barrels for feature roots, or should imports stay explicit down to `components/`, `hooks/`, and `utils/`?

---

## Recommended First Pull Request

The first PR should be intentionally small:

1. Add this plan
2. Remove duplicate assets and duplicate logger implementation
3. Remove or confirm obsolete root-level `ProposalActions` and `ProposalActionData` files
4. Remove the unused `@/types` alias if validation confirms it is dead

This gives the repo immediate clarity improvements with minimal risk, then creates momentum for the structural phases.
