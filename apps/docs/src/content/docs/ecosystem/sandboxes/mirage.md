---
title: Mirage
description: Connect Flue agents to Mirage workspaces and mounted resources.
lastReviewedAt: 2026-05-30
---

The Mirage adapter adapts an application-owned Mirage `Workspace` into Flue's sandbox interface. Mirage offers runtime packages for Node and browser-class runtimes, allowing the adapter pattern to be used on Node or Cloudflare when you choose compatible resources.

## Quickstart

Add Mirage as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox mirage
```

## Configure

| Requirement                              | Purpose                                                                                   |
| ---------------------------------------- | ----------------------------------------------------------------------------------------- |
| `@struktoai/mirage-node` package         | **Required on Node.js** — Provides Node-compatible Mirage Workspace resources.            |
| `@struktoai/mirage-browser` package      | **Required on Cloudflare** — Provides browser-compatible Workspace resources only.        |
| Application-owned resource configuration | **Required** — Defines mounts, credentials, writable boundaries, and lifetime.            |
| Environment-variable credentials         | **Not required** — Mirage resource credentials are configured by the application instead. |

The generated adapter uses Mirage's shared workspace contract. Some Mirage resources, such as SSH- or database-oriented Node resources, require the Node runtime and must not be imported into a Cloudflare build.

## Choose this adapter when

Use Mirage when your application wants to assemble a workspace from explicit mounted resources and present that workspace to an agent through a single sandbox boundary. Your application owns resource mounting, credentials, writable boundaries, and workspace lifetime.

See [Sandboxes](/docs/guide/sandboxes/), [Deploy on Node.js](/docs/ecosystem/deploy/node/), [Deploy on Cloudflare](/docs/ecosystem/deploy/cloudflare/), and [Sandbox Adapter API](/docs/api/sandbox-api/).
