# Security Clearance API Documentation

The ClawSecure Security Clearance API provides real-time programmatic integrity verification for OpenClaw agents. Developers and platforms can verify an agent's security status before granting access to sensitive data or actions — enabling OpenClaw security automation at scale.

## Base URL

```
https://www.clawsecure.ai/api/v1
```

## Authentication

The Security Clearance API is currently **free and open** — no API key required. Rate limiting applies to prevent abuse.

Future versions will introduce optional API key authentication for higher rate limits and premium features.

## Endpoints

### POST `/api/v1/clearance`

Verify the integrity of an OpenClaw agent in real time.

**Request Body (JSON):**

| Field | Type | Required | Description |
|---|---|---|---|
| `agent_id` | string | Yes | The skill identifier (e.g., `github-user/skill-name`) |
| `current_skill_hash` | string | No | SHA-256 hash of the currently installed skill code. If provided, ClawSecure verifies the hash matches the last audited version. |

**Example Request:**

```bash
curl -X POST https://www.clawsecure.ai/api/v1/clearance \
  -H "Content-Type: application/json" \
  -d '{
    "agent_id": "github-user/skill-name",
    "current_skill_hash": "sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855"
  }'
```

**Example Response (SECURE):**

```json
{
  "status": "SECURE",
  "score": 92,
  "agent_id": "github-user/skill-name",
  "last_audit": "2026-02-25T14:30:00Z",
  "report_url": "https://www.clawsecure.ai/report/abc123",
  "hash_match": true,
  "categories_covered": 10
}
```

**Example Response (UNVERIFIED):**

```json
{
  "status": "UNVERIFIED",
  "score": null,
  "agent_id": "github-user/unknown-skill",
  "last_audit": null,
  "report_url": null,
  "hash_match": false,
  "categories_covered": 0
}
```

### Response Fields

| Field | Type | Description |
|---|---|---|
| `status` | string | `SECURE`, `UNVERIFIED`, or `DENIED` |
| `score` | integer or null | Security score (0-100). Null if not yet audited. |
| `agent_id` | string | The queried skill identifier |
| `last_audit` | string or null | ISO 8601 timestamp of the most recent audit |
| `report_url` | string or null | Direct link to the full Security Audit Report |
| `hash_match` | boolean | Whether the provided hash matches the audited version |
| `categories_covered` | integer | Number of OWASP ASI categories covered (0-10) |

### Status Codes

| Status | Meaning | Recommended Action |
|---|---|---|
| `SECURE` | Agent has been audited and the hash matches the verified version | Safe to proceed |
| `UNVERIFIED` | Agent has not been audited or the hash is not recognized | Submit for scanning before granting access |
| `DENIED` | Agent failed critical security checks | Do not grant access to sensitive resources |

### GET `/api/v1/clearance`

Returns self-documenting API information with an example request and all possible status values. Useful for integration testing.

**Example:**

```bash
curl https://www.clawsecure.ai/api/v1/clearance
```

## Rate Limits

| Tier | Limit | Notes |
|---|---|---|
| Free (current) | 100 requests/minute per IP | No authentication required |
| Premium (planned) | Higher limits with API key | Coming Q2 2026 |

Requests exceeding the rate limit receive a `429 Too Many Requests` response.

## Integration Examples

### Verify Before Install (Bash)

```bash
#!/bin/bash
SKILL="github-user/skill-name"
RESPONSE=$(curl -s -X POST https://www.clawsecure.ai/api/v1/clearance \
  -H "Content-Type: application/json" \
  -d "{\"agent_id\": \"$SKILL\"}")

STATUS=$(echo $RESPONSE | jq -r '.status')

if [ "$STATUS" = "SECURE" ]; then
  echo "✅ Skill verified. Safe to install."
else
  echo "⚠️ Skill status: $STATUS. Review the report before proceeding."
fi
```

### Continuous Monitoring (Python)

```python
import requests

def check_clearance(agent_id, skill_hash=None):
    payload = {"agent_id": agent_id}
    if skill_hash:
        payload["current_skill_hash"] = skill_hash

    response = requests.post(
        "https://www.clawsecure.ai/api/v1/clearance",
        json=payload
    )
    return response.json()

result = check_clearance("github-user/skill-name")
print(f"Status: {result['status']}, Score: {result['score']}")
```

## Error Handling

| HTTP Code | Meaning |
|---|---|
| `200` | Success |
| `400` | Invalid request body (missing `agent_id`) |
| `429` | Rate limit exceeded |
| `500` | Server error |

## Need Help?

- **Full platform:** [clawsecure.ai](https://www.clawsecure.ai)
- **Registry:** [Browse 2,890+ audited agents](https://www.clawsecure.ai/registry)
- **Issues:** [Open a feature request](https://github.com/clawsecure/clawsecure-openclaw-security/issues)
