---
description: Deploy and host static sites with Novence MCP. Use when creating projects, uploading site files, running quality checks, deploying, attaching domains, or managing Novence forms and quotas.
---

# Novence deploy

Use the Novence MCP tools (server `novence`) for static-site hosting.

## Prerequisites

- `NOVENCE_API_KEY` set to a Bearer `nv_` key (see `SETUP.md` / bootstrap at `POST https://api.novence.ai/v1/bootstrap`).

## Typical loop

1. `create_project` with a name.
2. `get_upload_urls_batch` for site paths, PUT file bodies to the presigned URLs.
3. `confirm_uploads_batch`.
4. `deploy` (optionally `force`).
5. Poll `get_deployment_status` / `get_checks_results` until published.
6. `get_preview_url` for the live URL (`https://{suffix}.novence.ai`).
7. Optional: `configure_custom_domain`, `create_form`, `get_quotas_and_usage`.

## Rules

- Prefer batch upload tools for multi-file sites.
- Do not invent APIs — use the MCP tools.
- For a local HTML billing/account console, use `get_account_console_kit` / `create_account_session` (never embed `nv_` in HTML).
