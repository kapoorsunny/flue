---
title: Cloudflare Shell
description: Use a durable Cloudflare Workspace with code-oriented agent operations.
---

The Cloudflare Shell adapter adapts an application-owned `@cloudflare/shell` `Workspace` into a Flue sandbox on the Cloudflare target. Unlike a Linux shell sandbox, it provides a durable workspace and a model-facing `code` tool that executes JavaScript against workspace state through a Worker Loader binding.

## Quickstart

Add Cloudflare Shell as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox cloudflare-shell
```

## Configure

| Requirement                               | Purpose                                                                                                                              |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Cloudflare target                         | **Required** — Runs the Workspace and Worker Loader integration.                                                                     |
| `@cloudflare/shell` package               | **Required** — Provides the durable Workspace.                                                                                       |
| `@cloudflare/codemode` package            | **Required** — Provides code-oriented model operations.                                                                              |
| `worker_loaders` binding such as `LOADER` | **Required on Cloudflare** — Executes JavaScript against Workspace state; this is a Cloudflare binding, not an environment variable. |
| Environment-variable credentials          | **Not required** — The integration uses the `worker_loaders` binding instead.                                                        |
| Ordinary Linux shell                      | **Not provided** — This adapter provides a model-facing `code` tool, not shell command execution.                                    |

Import the generated helpers from your project adapter file, not from `@flue/runtime/cloudflare`:

```ts
import { getDefaultWorkspace, getShellSandbox } from '../sandboxes/cloudflare-shell';
```

## Choose this adapter when

Use Cloudflare Shell when files must be stored in a durable Workspace and agent work can be expressed through Workspace operations. It is not interchangeable with a container: `harness.shell(...)` and `session.shell(...)` do not provide Linux command execution through this adapter.

If the workspace should survive later user interactions, associate it with a stable addressable agent instance. A workspace created inside one workflow invocation belongs to that invocation's owner rather than forming a shared cross-run workspace.

You can hydrate content from R2 through the generated adapter helper before initializing the consuming harness. Hydration is a copy into Workspace, not a live-mounted bucket.

See [Sandboxes](/docs/guide/sandboxes/) and [Deploy on Cloudflare](/docs/ecosystem/deploy/cloudflare/).
