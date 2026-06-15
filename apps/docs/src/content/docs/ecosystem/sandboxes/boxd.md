---
title: boxd
description: Connect a Flue agent to an application-owned boxd Linux VM.
lastReviewedAt: 2026-05-30
---

The boxd adapter adapts an already-initialized boxd `Box` from `@boxd-sh/sdk` into Flue's sandbox interface. Use it when an agent needs a provider-backed Linux virtual machine with filesystem and shell behavior rather than the lightweight default workspace.

## Quickstart

Add boxd as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox boxd
```

## Configure

| Variable       | Purpose                                                                                                            |
| -------------- | ------------------------------------------------------------------------------------------------------------------ |
| `BOXD_API_KEY` | **Alternative authentication** — Authenticates with boxd when a short-lived token is not used.                     |
| `BOXD_TOKEN`   | **Alternative authentication** — Provides provider-supported short-lived authentication instead of `BOXD_API_KEY`. |

| Requirement                 | Purpose                                                          |
| --------------------------- | ---------------------------------------------------------------- |
| One boxd credential         | **Required** — Uses either `BOXD_API_KEY` or `BOXD_TOKEN`.       |
| `@boxd-sh/sdk` package      | **Required** — Creates the Linux VM adapted to `SandboxFactory`. |
| Application-owned lifecycle | **Required** — Creates, reuses, and deletes the VM.              |

The generated adapter expects your application to create and own the boxd VM. It does not decide VM identity, retention, or cleanup for you.

## Use it when

Choose boxd when a task requires real Linux command behavior in an isolated provider VM, particularly where a separate VM per workspace or agent instance is part of your application design.

Before reusing a VM across sessions or tenants, define identity, authorization, egress, secrets, and cleanup policies. Conversation persistence remains controlled separately by Flue session storage.

See [Sandboxes](/docs/guide/sandboxes/) for execution-boundary design and [Sandbox Adapter API](/docs/api/sandbox-api/) for the adapter contract.
