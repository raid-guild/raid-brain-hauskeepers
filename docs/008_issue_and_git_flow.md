# Issue And Git Flow

This doc outlines the lifecycle of an issue in the system and how that lifecycle connects to the DAOhaus repo git flow.

The goal is to make each status explicit, document who moves an issue forward, and show where agent-created code branches fit into the repo workflow.

---

## Issue Sources

Issues can enter the system from:

- Discord
- Refactory UI

Once ingested, the issue starts in the inbox and waits for a human decision before agent triage begins.

---

## Status Lifecycle

### 1. Inbox

The issue has been created and ingested into the system.

**Status:** `Inbox`

**How it enters:**

- Issue is submitted from Discord.
- Issue is submitted from the Refactory UI.

**Human review focus:**

- Confirm the issue is valid and worth triaging.
- Check whether the report has enough context for the agent to evaluate it.
- Close duplicates, spam, or issues that should not enter the agent workflow.

**Next steps:**

- Human can approve the issue to move it to `Triaging`.
- Human can close the issue.

---

### 2. Triaging

The issue is evaluated by the agent. The agent adds a summary and suggested change details so the work can be reviewed before implementation.

**Status:** `Triaging`

**How it enters:**

- Human approves an `Inbox` issue for triage.

**Next steps:**

- Agent moves the issue to `Ready for Agent` when triage is complete.
- Human can close the issue.

---

### 3. Ready For Agent

The issue has been spec'd by the agent and is ready for human review before implementation.

**Status:** `Ready for Agent`

**How it enters:**

- Agent completes triage and adds the summary and suggested change details.

**Human review focus:**

- Review the agent summary for accuracy.
- Review the suggested solution or implementation approach.
- Confirm the proposed scope is appropriate before the agent changes code.
- Request clarification outside the status flow if the issue is not ready for implementation.

**Next steps:**

- Human can approve the issue to move it to `Working`.
- Human can close the issue.

---

### 4. Working

The agent creates a change request branch and updates the code.

**Status:** `Working`

**How it enters:**

- Human approves a `Ready for Agent` issue for implementation.
- Agent resumes work after the issue is moved to `Changes Requested`.

**Next steps:**

- Agent moves the issue to `Awaiting Review` when the implementation is ready.
- Human can close the issue.

---

### 5. Awaiting Review

The issue branch is ready for code review and evaluation.

At this point, a human currently needs to manually create the pull request. Automating PR creation is a future enhancement opportunity.

**Status:** `Awaiting Review`

**How it enters:**

- Agent completes implementation on the change request branch.

**Human review focus:**

- Review the code on the agent-created branch.
- Confirm the branch implements the approved issue scope and suggested solution.
- Check for regressions, unsafe changes, missing tests, or mismatches with repo patterns.
- Decide whether the work is ready to approve or needs another agent pass.

**Next steps:**

- Human can move the issue to `Approved`.
- Human can move the issue to `Changes Requested`.
- Human can close the issue.

---

### 6. Changes Requested

The human has reviewed the work and requested changes.

The agent should act on the latest review comment, move the issue back to `Working`, update the existing change request branch, and then move the issue back to `Awaiting Review` when done.

**Status:** `Changes Requested`

**How it enters:**

- Human requests changes from `Awaiting Review`.

**Human review focus:**

- Leave a clear latest comment describing what needs to change.
- Focus the request on concrete code, behavior, test, or scope issues.
- Make sure the requested changes are actionable by the agent.

**Next steps:**

- Agent moves the issue back to `Working` and addresses the latest comment.
- Human can close the issue.

---

### 7. Approved

The human has reviewed and approved the change.

In this step, a human currently creates the pull request into the target branch.

**Status:** `Approved`

**How it enters:**

- Human approves the issue from `Awaiting Review`.

**Human review focus:**

- Confirm the branch code is acceptable for a PR into `develop`.
- Confirm any requested changes have been addressed.
- Confirm the implementation is ready for the repo's normal PR review and merge process.

**Next steps:**

- Human creates or finalizes the PR into the target branch.
- Human can close the issue.
- Future enhancement: add a `Completed` status after the PR has been merged.

---

### 8. Closed

The issue has been closed and should no longer be acted on by the agent.

**Status:** `Closed`

**How it enters:**

- Human closes the issue from any status.

**Next steps:**

- No agent action is expected.
- If the issue needs to continue later, a human should reopen it or create a new issue depending on the system behavior.

---

### Optional Future State: Completed

The system may eventually add a `Completed` status to distinguish approved work from merged work.

This would make the end state clearer:

- `Approved`: human has approved the issue and PR work can proceed.
- `Completed`: PR has been merged and the issue lifecycle is done.

---

## State Transition Summary

```text
Inbox
  -> Triaging
  -> Ready for Agent
  -> Working
  -> Awaiting Review
  -> Approved
```

Change request loop:

```text
Awaiting Review
  -> Changes Requested
  -> Working
  -> Awaiting Review
```

Close path:

```text
Any status
  -> Closed
```

---

## Role Responsibilities

### Human

- Approves inbox issues for triage.
- Reviews agent-generated triage output.
- Approves spec'd issues for implementation.
- Reviews completed agent branches.
- Requests changes when the implementation needs more work.
- Approves completed work.
- Manually creates the PR into the target branch.
- Can close an issue at any point.

### Agent

- Evaluates issues during triage.
- Adds issue summary and suggested change details.
- Creates the change request branch.
- Implements code changes.
- Responds to the latest requested-changes comment.
- Moves the issue to the next agent-owned status when its work is complete.

---

## Human Review Points

There are two main human review moments in the lifecycle.

### Suggested Solution Review

This happens in `Ready for Agent`.

The human reviews the agent's summary and suggested change details before any code is written. The decision is whether the issue is sufficiently understood, correctly scoped, and ready for implementation.

### Branch Code Review

This happens in `Awaiting Review`.

The human reviews the agent-created branch after implementation. The decision is whether the code should be approved, sent back through `Changes Requested`, or closed.

---

## DAOhaus Git Flow

### Branches

`main`

- Production branch.
- Receives code after work has passed review and is ready for production release.

`develop`

- Target branch for agent change request work.
- Agent branches fork from `develop`.
- Approved work merges back into `develop`.
- Staging builds are built from this branch.

Change request branches

- Created by the agent during `Working`.
- Fork from `develop`.
- Merge back into `develop` after approval and PR review.
- Named with the change request number and issue title.

Example naming pattern:

```text
cr-123-short-issue-title
```

---

## How Issue Flow Maps To Git Flow

### Inbox Through Ready For Agent

No git branch is required yet.

The issue is being reviewed, triaged, and spec'd before code work begins.

### Working

The agent creates a change request branch from `develop`.

```text
develop
  -> cr-123-short-issue-title
```

The agent commits implementation work to that change request branch.

### Awaiting Review

The branch contains the proposed change and is ready for review.

A human manually creates the PR into `develop`.

```text
cr-123-short-issue-title
  -> develop
```

### Changes Requested

The agent continues work on the existing change request branch.

The issue returns to `Working` while the agent addresses the latest review comment.

### Approved

The human has approved the issue. The PR can be merged into `develop` once repo review requirements are satisfied.

After merge, staging builds can pick up the change from `develop`.

---

## Enhancement Opportunities

- Automatically create the PR when an issue moves to `Awaiting Review`.
- Add a `Completed` status after the PR has merged.
- Track the linked branch and PR directly on the issue.
- Track whether the branch was forked from the latest `develop`.
