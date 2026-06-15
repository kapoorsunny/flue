---
title: islo
description: Connect a Node-target Flue application to a named islo sandbox through its CLI.
lastReviewedAt: 2026-05-30
---

The islo adapter adapts a named islo sandbox into Flue's sandbox interface by invoking the local `islo` CLI. It is designed for a Node.js server, container, or CI runner where the binary is installed and can launch remote commands.

## Quickstart

Add islo as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox islo
```

## Configure

| Variable       | Purpose                                                                                                                |
| -------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `ISLO_API_KEY` | **Alternative authentication** — Authenticates server or CI operation when existing CLI authentication is unavailable. |

| Requirement                            | Purpose                                                                   |
| -------------------------------------- | ------------------------------------------------------------------------- |
| Existing CLI authentication or API key | **Required** — Authenticates through the CLI session or `ISLO_API_KEY`.   |
| Node.js child-process capability       | **Required** — Allows the adapter to invoke the CLI.                      |
| `islo` binary on `PATH`                | **Required** — Executes remote shell and file operations.                 |
| Named islo sandbox                     | **Required** — Identifies the application- or deployment-managed sandbox. |

## Choose this adapter when

Use islo when an application can rely on a host-installed CLI and wants to connect to named sandboxes from a Node execution environment. Do not use it in Cloudflare Workers or other runtimes that cannot execute native child processes.

The adapter runs remote shell/file work through the CLI; ensure its host process, credentials, and agent inputs match your intended trust boundary.

See [Deploy on Node.js](/docs/ecosystem/deploy/node/), [Sandboxes](/docs/guide/sandboxes/), and [Sandbox Adapter API](/docs/api/sandbox-api/).
