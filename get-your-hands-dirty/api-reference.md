# API reference (partial)

This page shows a small subset of the public REST API for HomeSphere.

## Get device state

GET /api/v1/devices/{device_id}

Responses

- 200 — OK (application/json)
- 401 — Unauthorized

Example response

```json
{
  "id": "lr-light-01",
  "type": "light",
  "state": { "on": true, "brightness": 80 }
}
```

## Set device state

POST /api/v1/devices/{device_id}/actions

Request body

```json
{ "action": "turn_on", "params": { "brightness": 60 } }
```

Authentication

Use a bearer token in the Authorization header. Example shown with curl:

```bash
curl -H "Authorization: Bearer $HOMESPHERE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"action":"turn_on"}' \
  https://api.homesphere.example/api/v1/devices/lr-light-01/actions
```

For SDKs and example clients, link to `api-client-examples.md` (coming soon).
