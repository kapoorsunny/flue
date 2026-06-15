---
title: exe.dev
description: Connect a Node-target Flue application to an exe.dev VM over SSH.
lastReviewedAt: 2026-05-30
---

The exe.dev adapter adapts an existing exe.dev VM into Flue's sandbox interface using SSH for commands and SFTP for files. Because it depends on Node.js APIs and `ssh2`, use it with the Node target rather than a Cloudflare Worker target.

## Quickstart

Add exe.dev as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox exedev
```

## Configure

| Variable        | Purpose                                                                                       |
| --------------- | --------------------------------------------------------------------------------------------- |
| `EXE_VM_HOST`   | **Required** — Identifies the exe.dev VM used to wire the sandbox adapter.                    |
| `EXE_SSH_KEY`   | **Optional** — Points to a private SSH key file.                                              |
| `SSH_AUTH_SOCK` | **Optional** — Authenticates through an SSH agent instead of `EXE_SSH_KEY`.                   |
| `EXE_API_TOKEN` | **Required for lifecycle examples** — Authenticates helpers that manage exe.dev VM lifecycle. |

| Requirement                       | Purpose                                                                   |
| --------------------------------- | ------------------------------------------------------------------------- |
| Node.js target                    | **Required** — Provides the Node APIs used by the adapter and SSH client. |
| `ssh2` package                    | **Required** — Provides SSH command execution and SFTP file access.       |
| Existing SSH-reachable exe.dev VM | **Required** — Supplies the remote sandbox resource.                      |
| SSH configuration                 | **Required** — Authenticates access to the VM.                            |

## Choose this adapter when

Use exe.dev when a Node-hosted Flue application should operate inside a VM you reach through SSH/SFTP. The adapter blueprint includes optional lifecycle helpers, but the sandbox adapter itself is designed around a VM your application owns.

Treat SSH keys and provider tokens as server-side secrets. Decide whether agent instances share or allocate VMs, and clean up application-owned VMs according to your retention policy.

See [Deploy on Node.js](/docs/ecosystem/deploy/node/), [Sandboxes](/docs/guide/sandboxes/), and [Sandbox Adapter API](/docs/api/sandbox-api/).
