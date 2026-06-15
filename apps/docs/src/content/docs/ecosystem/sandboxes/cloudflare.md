---
title: Cloudflare Sandbox
description: Run Flue agent work inside Cloudflare container-backed sandboxes.
---

Cloudflare Sandbox uses `@cloudflare/sandbox` to provide a container-backed Linux environment to a Flue application deployed on Cloudflare. This integration is platform-native: it is not an adapter module for a Node-target application.

## Quickstart

Add Cloudflare Sandbox as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox cloudflare
```

## Configure

| Requirement                                  | Purpose                                                                                                                      |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Cloudflare target                            | **Required** — Runs the platform-native sandbox integration.                                                                 |
| `@cloudflare/sandbox` package                | **Required** — Provides the Sandbox Durable Object and RPC client.                                                           |
| Container image                              | **Required** — Defines the Linux filesystem and command environment.                                                         |
| Durable Object/container binding             | **Required on Cloudflare** — Exposes the sandbox through Wrangler platform configuration; it is not an environment variable. |
| Stable sandbox identity and retention policy | **Required** — Controls lifecycle and reuse for the application.                                                             |
| Environment-variable credentials             | **Not required** — The platform integration uses Cloudflare bindings and deployment configuration instead.                   |

Cloudflare Sandbox requires a Worker deployment, Durable Object/container configuration, and a container image. Add the dependency to a Cloudflare-targeted project and export its Durable Object class from your Cloudflare deployment module:

```ts
// <source-root>/cloudflare.ts
export { Sandbox } from '@cloudflare/sandbox';
```

Declare the sandbox binding in Wrangler configuration, then wrap the RPC stub returned by `getSandbox(...)` with `cloudflareSandbox(...)` and pass it to an agent:

```ts
import { getSandbox } from '@cloudflare/sandbox';
import { createAgent } from '@flue/runtime';
import { cloudflareSandbox } from '@flue/runtime/cloudflare';

type Env = { Sandbox: DurableObjectNamespace };

export default createAgent<unknown, Env>(({ id, env }) => ({
  model: 'anthropic/claude-sonnet-4-6',
  sandbox: cloudflareSandbox(getSandbox(env.Sandbox, id)),
  cwd: '/workspace',
}));
```

## Choose this integration when

Use Cloudflare Sandbox when an agent on Cloudflare needs git, package installation, native binaries, or other Linux tooling. Prefer Cloudflare Shell instead when a durable workspace with Workspace-oriented operations is sufficient and a Linux toolchain is unnecessary.

Treat network egress, mounted data, credentials, and side effects as application security decisions. See [Sandboxes](/docs/guide/sandboxes/#remote-sandboxes) and [Deploy on Cloudflare](/docs/ecosystem/deploy/cloudflare/).
