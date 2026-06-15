---
title: E2B
description: Connect a Flue agent to an E2B Linux sandbox.
lastReviewedAt: 2026-05-30
---

The E2B adapter adapts an initialized E2B sandbox from the `e2b` package into Flue's sandbox interface. Use it for provider-managed Linux execution when an agent needs shell commands and workspace files outside the application host.

## Quickstart

Add E2B as a sandbox to any existing Flue project by running the following command in your terminal or coding agent of choice.

```bash
flue add sandbox e2b
```

## Configure

| Variable      | Purpose                                        |
| ------------- | ---------------------------------------------- |
| `E2B_API_KEY` | **Required** — Authenticates with the E2B API. |

| Requirement                    | Purpose                                                                     |
| ------------------------------ | --------------------------------------------------------------------------- |
| `e2b` package                  | **Required** — Provides the initialized E2B sandbox adapted by Flue.        |
| Provider-managed Linux sandbox | **Required** — Supplies the command and filesystem environment.             |
| Application-owned lifecycle    | **Required** — Creates the sandbox and closes or retains it as appropriate. |

## Integration shape

```ts
import { Sandbox } from 'e2b';
import { createAgent } from '@flue/runtime';
import { e2b } from '../sandboxes/e2b';

const sandbox = await Sandbox.create();
const agent = createAgent(() => ({
  model: 'anthropic/claude-sonnet-4-6',
  sandbox: e2b(sandbox),
}));
```

Select templates, timeouts, network access, secret exposure, and resource reuse through your application and provider policy. Flue adapts the active environment; it does not choose provider retention for you.

See [Sandboxes](/docs/guide/sandboxes/) and [Sandbox Adapter API](/docs/api/sandbox-api/).
