# Prism Hooks

Working notes for Prism hooks.

Hooks are on-demand entrypoints for workflow-backed requests. They are the event-trigger complement to scheduled tasks.

Use hooks when an outside event, service, or agent action should create a request and optionally start a workflow immediately.

## Mental Model

Prism has three main trigger surfaces:

- Tasks: scheduled jobs that run on cron and may create requests.
- Hooks: event/on-demand triggers that receive payloads and create requests.
- Direct requests: Codex, the admin UI, or another trusted caller creates a request directly.

Hooks should stay thin. A hook should:

1. Accept a JSON payload.
2. Create a request from a small template.
3. Preserve the raw payload as an artifact.
4. Optionally auto-run the workflow until the next gate.

The workflow and its step markdown own the behavior after that.

## Common Uses

Examples:

- GitHub issue webhook creates a request.
- Discord support escalation creates a request.
- Publishing system callback resumes a workflow.
- Third-party automation creates a content request.
- Codex agent exposes a reusable trigger for another service.

Use tasks for scheduled work. Use hooks for event-driven work. Use direct request creation when there is no reusable trigger entrypoint to preserve.

## Data Model

Hooks are stored in the site database.

Important fields:

| Field | Purpose |
| --- | --- |
| `key` | Stable identifier used in the trigger URL. |
| `name` | Human-readable name. |
| `description` | Short admin/agent explanation. |
| `enabled` | Disabled hooks cannot be triggered. |
| `workflow_key` | Workflow used for created requests. |
| `auth_mode` | Currently `service-token`. |
| `request_template_json` | Small request creation template. |
| `auto_run_json` | Whether and how the workflow starts after request creation. |
| `system_default` | Protects built-in hooks from deletion. |
| `last_triggered_at` | Last successful trigger timestamp. |

Custom hooks can be created, updated, deleted, and triggered through the agent API. Built-in hooks can be toggled or updated by migrations/template code, but they are protected from agent deletion.

## Request Template

The request template maps a hook payload into a request.

Typical shape:

```json
{
  "titleTemplate": "Support Request - {{date}}",
  "descriptionTemplate": "Handle this support event.\n\nPayload:\n{{payload}}",
  "requestType": "support",
  "priority": "normal",
  "targetAppId": null,
  "targetEnvironmentId": null,
  "constraints": {
    "source": "hook"
  },
  "attachments": []
}
```

Supported placeholders:

- `{{date}}`: current UTC date as `YYYY-MM-DD`.
- `{{now}}`: current ISO timestamp.
- `{{payload}}`: full JSON payload.
- `{{fieldName}}`: top-level payload field.

Keep templates generic. If a workflow needs detailed interpretation, put that in workflow step markdown and have the step read `hook-payload.json`.

## Trigger Behavior

Trigger endpoint:

```text
POST /agent/hooks/<hook-key>/trigger
```

Authentication:

```text
x-service-token: <PRISM_AGENT_SERVICE_TOKEN>
```

On a successful trigger, Prism:

1. Verifies the hook exists and is enabled.
2. Verifies the target workflow exists and is enabled.
3. Creates a request with `source = hook:<hook-key>`.
4. Stores the raw trigger body as `hook-payload.json`.
5. Records the artifact with kind `hook-payload`.
6. Starts the workflow when `autoRun.enabled` is true.
7. Updates `last_triggered_at`.

The hook payload is durable request context. Agents should read it through the artifact API instead of relying on chat history or local files.

## Agent API

Runtime agents must use `/agent/*`, not `/admin/*`.

Routes:

```text
GET /agent/hooks
POST /agent/hooks
GET /agent/hooks/:key
PATCH /agent/hooks/:key
DELETE /agent/hooks/:key
POST /agent/hooks/:key/trigger
```

The built-in `prism-hook-author` skill in the Prism template tells Codex agents how to create and test hooks.

## Admin UI

The Hooks tab is intentionally operational, not a full authoring UI.

It supports:

- Viewing registered hooks.
- Grouping custom and built-in hooks.
- Enabling and disabling hooks.
- Deleting custom hooks.
- Copying trigger endpoints.
- Sending a manual JSON test payload.

Hook creation and editing are agent-first. Use the hook-authoring skill and `/agent/hooks` API so hook creation follows the same pattern as custom skills, tasks, and workflows.

## Source Labels

Requests created by hooks are marked with:

```text
source = hook:<hook-key>
```

The request board displays that as:

```text
Hook: <hook-key>
```

Other request sources include:

- `manual`: browser-created request.
- `chat`: agent-created request.
- `task-runner`: scheduled workflow task.

This source label is for traceability. Workflow state still lives in workflow run records, and detailed external system records should be attached as external refs when they need later sync or lookup.

## When Not To Use Hooks

Do not use hooks for:

- Cron-based work; use tasks.
- Long-running business logic; use workflows and skills.
- Storing executable code; use reviewed scripts or skills.
- Replacing external refs; attach GitHub, Discord, CMS, Railway, or other external records as refs when they matter.
- Public unauthenticated webhooks; the first implementation is service-token based.

## Future Work

Likely next slices:

- Per-hook secrets for third-party webhook callers that should not receive the full agent service token.
- Optional payload-to-external-ref mapping.
- Replay/retry from a stored hook payload.
- Hook execution history beyond `last_triggered_at`.
- Richer trigger diagnostics in the Hooks tab.
