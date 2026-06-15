---
title: Vercel Sandbox
description: Connect a Flue agent to an application-owned Vercel Sandbox environment.
lastReviewedAt: 2026-05-30
---

The Vercel Sandbox adapter adapts an initialized `@vercel/sandbox` `Sandbox` into Flue's sandbox interface. Use it when application code should execute agent work inside a Vercel-managed sandbox rather than on its host filesystem.

## Quickstart

Add Vercel Sandbox as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox vercel
```

## Configure

| Variable            | Purpose                                                                                                             |
| ------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `VERCEL_OIDC_TOKEN` | **Required for OIDC authentication** — Injected automatically on Vercel; set it explicitly when using OIDC locally. |

| Requirement                     | Purpose                                                                                                      |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Vercel-supported authentication | **Required** — Uses OIDC on Vercel or an access token or other supported authentication flow outside Vercel. |
| `@vercel/sandbox` package       | **Required** — Creates the Vercel Sandbox adapted by Flue.                                                   |
| Application-owned lifecycle     | **Required** — Creates the sandbox and decides its retention and cleanup.                                    |

## Typical use

```ts
import { Sandbox } from '@vercel/sandbox';
import { createAgent } from '@flue/runtime';
import { vercel } from '../sandboxes/vercel';

const sandbox = await Sandbox.create({ runtime: 'node24' });
const agent = createAgent(() => ({
  model: 'anthropic/claude-sonnet-4-6',
  sandbox: vercel(sandbox),
}));
```

Keep Vercel authentication values in trusted application configuration and determine whether sandboxes should be fresh per job or reusable for stable agent identities.

See [Sandboxes](/docs/guide/sandboxes/) and [Sandbox Adapter API](/docs/api/sandbox-api/).
