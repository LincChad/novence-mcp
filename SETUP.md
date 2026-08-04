# Novence MCP setup

Use this skill when the user installs the Novence plugin or needs an API key for MCP tools.

## Goal

Connect Claude Code to the hosted Novence MCP server at `https://api.novence.ai/mcp` using a Bearer `nv_` API key.

## Steps

1. Ask for the user's email if they do not already have a Novence key.
2. Call bootstrap (REST, not MCP):

```bash
curl -sS -X POST https://api.novence.ai/v1/bootstrap \
  -H 'Content-Type: application/json' \
  -d '{"email":"USER_EMAIL"}'
```

3. The response includes an `nv_…` API key. Tell the user to export it:

```bash
export NOVENCE_API_KEY='nv_…'
```

4. Optionally verify the emailed OTP via REST (`POST /v1/auth/verify`) to unlock full Free quotas. Unverified keys still work with limited quotas.
5. Confirm MCP tools with `/mcp` — Novence tools such as `list_projects`, `create_project`, and `deploy` should appear.
6. Prefer the agent loop: create project → upload files → deploy → poll `get_deployment_status` until live → optional domain/forms.

## Notes

- Never put `nv_` keys in HTML or commit them to git.
- Docs: https://novence.ai/mcp
- Privacy: https://novence.ai/privacy
- Support: support@novence.ai
