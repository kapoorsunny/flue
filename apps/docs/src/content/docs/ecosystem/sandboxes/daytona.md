---
title: Daytona
description: Connect a Flue agent to an application-owned Daytona sandbox.
lastReviewedAt: 2026-06-01
---

The Daytona adapter adapts an already-initialized Daytona sandbox from `@daytona/sdk` into Flue's sandbox interface. Use it when a Node-hosted application needs a provider-managed Linux environment with filesystem and shell operations.

## Quickstart

Add Daytona as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox daytona
```

## Configure

| Variable          | Purpose                                            |
| ----------------- | -------------------------------------------------- |
| `DAYTONA_API_KEY` | **Required** — Authenticates with the Daytona API. |

| Requirement                 | Purpose                                                                                         |
| --------------------------- | ----------------------------------------------------------------------------------------------- |
| `@daytona/sdk` package      | **Required** — Creates the Daytona sandbox adapted by Flue.                                     |
| Application-owned lifecycle | **Required** — Creates, retains, and deletes the sandbox, then passes it to `daytona(sandbox)`. |

The generated adapter expects your application to create and own the Daytona sandbox. It does not decide sandbox identity, retention, or cleanup for you.

## Typical use

```ts
import { Daytona } from '@daytona/sdk';
import { createAgent } from '@flue/runtime';
import { daytona } from '../sandboxes/daytona';

const client = new Daytona({ apiKey: env.DAYTONA_API_KEY });
const sandbox = await client.create();
const agent = createAgent(() => ({
  model: 'anthropic/claude-sonnet-4-6',
  sandbox: daytona(sandbox),
}));
```

Configure images, snapshots, regions, environment variables, and volumes through the Daytona SDK before passing the sandbox to `daytona(...)`. For a narrower working directory, configure `cwd` on the created agent; Flue resolves it once against the adapter's provider-owned base directory during `init()`.

See [Sandboxes](/docs/guide/sandboxes/#remote-sandboxes), [Sandbox Adapter API](/docs/api/sandbox-api/), and [Daytona's TypeScript SDK reference](https://www.daytona.io/docs/en/typescript-sdk/daytona/).
