---
title: Modal
description: Connect a Flue agent to an application-owned Modal Sandbox.
lastReviewedAt: 2026-05-30
---

The Modal adapter adapts an already-initialized Modal Sandbox from the `modal` JavaScript SDK into Flue's sandbox interface. Use it for provider-backed command execution and files when your application provisions Modal sandbox resources.

## Quickstart

Add Modal as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox modal
```

## Configure

| Variable             | Purpose                                                                                                           |
| -------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `MODAL_TOKEN_ID`     | **Required without `~/.modal.toml`** — Identifies the Modal token when file-based credentials are unavailable.    |
| `MODAL_TOKEN_SECRET` | **Required without `~/.modal.toml`** — Authenticates the Modal token when file-based credentials are unavailable. |

| Requirement          | Purpose                                                                            |
| -------------------- | ---------------------------------------------------------------------------------- |
| `modal` package      | **Required** — Provides the Modal JavaScript SDK.                                  |
| Node.js 22 or later  | **Required** — Runs the SDK used by the generated adapter.                         |
| Suitable Modal image | **Required** — Provides the shell and system utilities required by the agent work. |

## Choose this adapter when

Use Modal when your application already manages Modal applications, images, or sandbox lifetimes and needs to expose that compute boundary to Flue operations. The adapter adapts the created sandbox; creation, shutdown, secret handling, networking, and image content remain your responsibility.

See [Sandboxes](/docs/guide/sandboxes/) and [Sandbox Adapter API](/docs/api/sandbox-api/).
