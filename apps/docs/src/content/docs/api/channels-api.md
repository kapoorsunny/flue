---
title: Channels API
description: Define transport channels and dispatch asynchronous input to agent sessions.
---

## Imports

TODO: Document canonical `@flue/runtime` imports and the focused `@flue/runtime/channels` subpath.

## Public exposure middleware

Public HTTP and WebSocket exposure is enabled by exported Hono middleware on agent and workflow modules:

```ts
// .flue/agents/assistant.ts
import { type AgentRouteHandler, type AgentWebSocketHandler } from '@flue/runtime';

export const route: AgentRouteHandler = async (_c, next) => next();
export const websocket: AgentWebSocketHandler = async (_c, next) => next();
```

For a workflow, use `WorkflowRouteHandler` and `WorkflowWebSocketHandler` instead. Either middleware may authenticate or reject a request before calling `next()`. Authored provider channels defined with `defineChannel(...)` are a separate inbound integration surface.

## `defineChannel(...)`

TODO: Document custom typed channels, listeners, and event emission.

## `dispatch(...)`

TODO: Reference asynchronous agent delivery, admission inputs, receipts, and `dispatchId`.

## Channel types

TODO: Reference channel event maps, contexts, listeners, route handlers, and dispatch request types.

## Dispatch is not a workflow run

TODO: Clearly distinguish `dispatchId` from workflow `runId`.
