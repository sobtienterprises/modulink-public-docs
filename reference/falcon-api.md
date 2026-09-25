# Falcon Cycle and Export API

This reference carries forward the manual's integration procedures with current
request fields. Use the [operator workflow](../workflows/operate-falcon.md) for
normal site operation. Match the API contract to the installed software release.

## Authentication and base address

The operator API uses `Authorization: Bearer <TOKEN>`. Obtain a token with the
[technician authentication procedure](technician-commissioning.md).
The Falcon base path is `/api/v1/skills/falcon` on the Basestation.

Use HTTPS with the verified site certificate. These templates assume the
certificate is trusted by the client. Add `--cacert /path/to/site-ca.pem` if needed.
Replace every angle-bracket placeholder. Keep credentials and response tokens private.

## Start a cycle

Current software requires more than the operator name and job reference in the
July manual. Read the skid's current measurement setup and the permitted duration
before creating a request. The current browser workflow supplies these fields:

| Field | Meaning |
| --- | --- |
| `key` | A new unique request identifier; retain it for retries. |
| `operator_name` | Person responsible for the record. |
| `job_ref` | Job reference, or null. |
| `expires_at` | Future UTC expiry in RFC 3339 form, within the configured duration limit. |
| `record_measurements` | Whether this cycle records configured measurements. |
| `expected_setup_revision` | Revision from the skid's current measurement setup. |

Prepare the request in `cycle-request.json`:

```json
{
  "key": "<NEW-REQUEST-ID>",
  "operator_name": "<OPERATOR-NAME>",
  "job_ref": "<JOB-REFERENCE>",
  "expires_at": "<UTC-EXPIRY>",
  "record_measurements": true,
  "expected_setup_revision": "<CURRENT-SETUP-REVISION>"
}
```

```sh
curl --fail-with-body 'https://modulink.local/api/v1/skills/falcon/skids/<SKID-ID>/cycles' \
  -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json' \
  --data-binary @cycle-request.json
```

HTTP 201 returns a created cycle. HTTP 202 can mean the workflow is still pending;
inspect its state before starting stages. HTTP 409 can mean a cycle is already
active or pending. Retain the original request for uncertain retries rather than
creating another key. Inspect `/cycle-requests/<REQUEST-ID>` to recover its result.

## Stages, notes, and completion

Use the returned cycle ID. Current stage values are validated:

| Field | Values |
| --- | --- |
| `action` | `Clean`, `Soak`, `Flush`, `Rinse` |
| `chemistry` | `High pH`, `Low pH`, `Neutral` |
| `temp` | `High`, `Ambient` |

The older manual described these as free text. Arbitrary values are not accepted
by the current handler.

```sh
curl --fail-with-body 'https://modulink.local/api/v1/skills/falcon/cycles/<CYCLE-ID>/stages' \
  -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json' \
  --data '{"action":"Clean","chemistry":"High pH","temp":"Ambient"}'
```

Record the returned stage ID. Stop the stage when that cleaning phase ends:

```sh
curl --fail-with-body -X POST \
  'https://modulink.local/api/v1/skills/falcon/cycles/<CYCLE-ID>/stages/<STAGE-ID>/stop' \
  -H 'Authorization: Bearer <TOKEN>'
```

Add an observation:

```sh
curl --fail-with-body 'https://modulink.local/api/v1/skills/falcon/cycles/<CYCLE-ID>/notes' \
  -H 'Authorization: Bearer <TOKEN>' -H 'Content-Type: application/json' \
  --data '{"text":"<OBSERVATION>"}'
```

Repeat stages as required. End the cycle with `complete` or `abandoned`:

```sh
curl --fail-with-body -X POST \
  'https://modulink.local/api/v1/skills/falcon/cycles/<CYCLE-ID>/end?status=complete' \
  -H 'Authorization: Bearer <TOKEN>'
```

Read `/cycles/<CYCLE-ID>` to confirm the final record. Ending a record is not a
physical equipment stop.

## Cleaning advisory settings

Read `GET /settings` for the stage catalog and settings. Read
`GET /skids/<SKID-ID>` for the skid's `done_rule` override. The manual documents
these defaults; confirm them on the installed release:

| Key | Manual default | Meaning |
| --- | --- | --- |
| `n` | 30 | Minimum samples in each trend window |
| `min_stage_seconds` | 600 | Minimum dwell before an advisory |
| `dp_flat_eps` | 1.0 | Pressure-change threshold in psi |
| `flow_flat_eps` | 0.5 | Concentrate-velocity threshold in ft/s |

Use the current UI's **Cleaning advisory thresholds**, or a reviewed
`PATCH /skids/<SKID-ID>/settings` request with a complete `done_rule` object.
The manual warns that replacing the object can return omitted fields to defaults.
Record the values before and after an edit. An advisory never certifies cleaning.

## ERP export

The read-only ERP API uses `X-API-Key: <SITE-API-KEY>`, not the operator Bearer token.
Obtain the key through the site's private handover. Its base path is
`/api/v1/skills/falcon/erp`.

| GET endpoint | Result |
| --- | --- |
| `/meta` | Site/skid metadata and retention information |
| `/cycles` | Cycle list |
| `/cycles/<CYCLE-ID>` | One cycle |
| `/cycles/<CYCLE-ID>/readings` | Recorded readings; a bounded scope is required |
| `/cleaning-events` | Cleaning-event summary |

```sh
curl --fail-with-body \
  'https://modulink.local/api/v1/skills/falcon/erp/cycles/<CYCLE-ID>/readings?from=<RFC3339-START>&to=<RFC3339-END>' \
  -H 'X-API-Key: <SITE-API-KEY>'
```

For readings, use `stage_id` or a `from`/`to` time scope. An unscoped request
returns HTTP 400. List responses include `data` and `page`. If `page.next_cursor`
is not null, request the next page with that cursor and the same filters. URL-encode
query values. Stop when the next cursor is null.

The manual specifies at least 90 days of cycle readings. Check `/meta` and the
site retention agreement. Export needed records before their retention period
ends; an ERP export is not a complete Basestation backup.
