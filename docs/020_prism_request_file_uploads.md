# Prism Request File Uploads

Working notes for Prism request file uploads and artifact storage.

Prism request artifacts are the durable file surface for workflow outputs, user uploads, and agent-produced handoff files. Request file uploads use the same artifact model instead of introducing a separate storage concept.

## Current Slice

Current behavior:

- Admin users with comment access can upload a local file on a request.
- The upload is stored under the site service data root using request artifact storage helpers.
- The artifact row is attached to the request.
- The upload appears in the request Artifacts tab.
- Uploads are not automatically indexed into Prism Memory or Prism Knowledge.

Current local storage path:

```text
${DATA_ROOT}/workflow-artifacts/requests/<request-id>/<artifact-id>-<filename>
```

Current optional limit:

```env
ARTIFACT_MAX_UPLOAD_MB=50
```

If the env var is omitted, the site defaults to 50 MB. The first implementation keeps uploads flowing through the site API rather than signed direct-to-bucket uploads.

## Artifact Shapes

Prism should keep one artifact metadata contract while allowing several backing shapes:

| Shape | Meaning |
| --- | --- |
| `local` | File stored under the site data volume. |
| `external` | Metadata points at a URL produced by another system, such as a render bucket. |
| `bucket` | Future Prism-owned S3/Railway bucket object storage. |
| `inline` | Future option for small text payloads if useful. |

The artifact row should remain the source of truth for:

- Request id.
- Optional workflow run id.
- Optional execution id.
- Kind.
- Name.
- MIME type.
- Size.
- Storage path or object key.
- Metadata.
- Creator/source.

## Upload Flow

Browser/admin uploads use an authenticated admin route and normal admin permissions.

Typical UI flow:

```text
admin user opens request
  -> uploads file in request detail panel
  -> site validates access and upload size
  -> site writes file under DATA_ROOT
  -> site creates request artifact row
  -> artifact appears in request Artifacts tab
```

Runtime agents should use the agent artifact API for durable outputs they create:

```text
POST /agent/change-board/requests/:id/artifacts
GET /agent/change-board/requests/by-number/:requestNumber/artifacts
GET /agent/change-board/requests/:id/artifacts/:artifactId/content
```

## Memory And Knowledge

Uploads should not automatically become Memory or Knowledge.

A workflow or agent should explicitly decide whether to:

- Summarize the file into a markdown/text artifact.
- Index that summary into Prism Knowledge.
- Include it in a request review.
- Leave it as request-local context only.

This keeps raw uploads from polluting long-lived knowledge indexes and preserves a human/agent review point before promotion.

## Future Provider Interface

When bucket storage is needed, add a provider behind the existing artifact storage helper instead of changing callers.

Suggested interface:

```ts
type ArtifactStorageProvider = {
  write(storageKey: string, body: Buffer): Promise<void>;
  read(storageKey: string): Promise<Buffer>;
  delete(storageKey: string): Promise<void>;
};
```

Suggested env shape:

```env
ARTIFACT_STORAGE_DRIVER=local
ARTIFACT_STORAGE_ROOT=/data/workflow-artifacts
ARTIFACT_MAX_UPLOAD_MB=50

# Future bucket/S3-compatible driver
ARTIFACT_STORAGE_DRIVER=s3
ARTIFACT_BUCKET_NAME=
ARTIFACT_BUCKET_REGION=
ARTIFACT_BUCKET_ENDPOINT=
ARTIFACT_ACCESS_KEY_ID=
ARTIFACT_SECRET_ACCESS_KEY=
```

The default should remain `local` so template instances work without new configuration.

## Remotion And Render Workflows

Render workflows do not need to change immediately. If a separate render service writes to a Railway bucket or other object store, the workflow can register receipts, thumbnails, and final media URLs as Prism request artifacts.

Useful render artifact set:

- `render-plan.json`
- `render-attempt.json`
- `render-receipt.json`
- `thumbnail.png`
- `video.mp4` or an external video URL artifact
- `publish-receipt.json`
