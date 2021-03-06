---
title: "Event Emittter"
---

# Event Emitter

::: tip
You can find the source code of this package at [packages/core-event-emitter](https://github.com/ARKEcosystem/core/tree/develop/packages/core-event-emitter).
:::

## Installation

```bash
yarn add @arkecosystem/core-event-emitter
```

## Alias

`event-emitter`

## Summary

`core-event-emitter` wraps around NodeJS's native Event class to provide event functionality across an ARK Core node.

## Behind the Scenes

Events are used inside ARK Core to trigger blockchain actions and the delivery of webhook payloads. Additionally, custom plugins can utilize the event emitter package to trigger their own actions in response to blockchain events.

Conceptually, this feature is similar to the [Hooks implementation in WordPress](https://codex.wordpress.org/Plugin_API), as well as to the lifecycle hook access provided by JavaScript frameworks such as [Vue](https://vuejs.org/v2/guide/instance.html#Instance-Lifecycle-Hooks) and [React](https://reactjs.org/docs/state-and-lifecycle.html). All of these systems expose The primary difference is that, because of the need for strict protocols around blockchain data creation and retrieval, ARK events are strictly reactionary. In other words, ARK Core events are **not** capable of changing data at runtime. The `transaction.applied` event, for instance, passes a complete transaction instance, not raw transaction data that can be altered in the style of a WordPress Filter.

Another way to think of the Event API is in the context of a [publish-subscribe pattern](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern). In this pattern, ARK Core packages can act both as publishers and subscribers of events.

The list of events published by ARK Core packages can be found in `core-blockchain`'s `getEvents` [method](https://github.com/ARKEcosystem/core/blob/develop/packages/core-blockchain/src/blockchain.ts#L589-L610):

```ts
public getEvents() {
    return [
        "block.applied",
        "block.disregarded",
        "block.forged",
        "block.received",
        "block.reverted",
        "delegate.registered",
        "delegate.resigned",
        "forger.failed",
        "forger.missing",
        "forger.started",
        "peer.added",
        "peer.removed",
        "round.created",
        "state:started",
        "transaction.applied",
        "transaction.expired",
        "transaction.forged",
        "transaction.pool.added",
        "transaction.pool.rejected",
        "transaction.pool.removed",
        "transaction.reverted",
        "wallet.saved",
        "wallet.created.cold",
    ];
}
```
