# Security Clearance API

The current contract of the ClawSecure Security Clearance API (request fields, statuses, errors and rate limits) is published by the API itself, so it always matches the running service:

```bash
curl -H 'User-Agent: your-app-name/1.0' https://www.clawsecure.ai/api/v1/clearance
```

Send a User-Agent header that names your application.

To check a skill, send `POST https://www.clawsecure.ai/api/v1/clearance` with a JSON body that names the skill you are checking in `skill_identifier`. The response above describes every request field (including the optional hash check), every status, the errors and the rate limit.

To report a security issue, see [SECURITY.md](../SECURITY.md).
