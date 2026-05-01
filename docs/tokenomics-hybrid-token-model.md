# Hybrid token model

## Two things at once

Every $BIT mint is **two things in one inscription**:

- A **fungible balance** in your wallet — measured in $BIT.
- A **unique non-fungible ordinal** — an immutable inscription on Bitcoin pointing at a specific block.

The two sides transfer independently.

## The fungible side

Indexers credit your wallet's $BIT balance the moment your mint inscription confirms. You can transfer any portion of your $BIT to another wallet via `token-transfer`. Same UX as any TAP fungible — partial transfers, multiple recipients, all standard.

## The non-fungible side

The mint inscription itself is an ordinal — sat-anchored, individually addressable, transferable. Each one says "this wallet minted block N." Block 0, block 1, block 100,000 — each is a one-of-one inscription. Collectors can hold rare-block mints (early blocks, halving blocks, anniversary blocks) independently of the fungible balance attached.

## Independent transfers

| Action | What moves | What stays |
| --- | --- | --- |
| **Send $BIT** via `token-transfer` | The fungible balance | The mint inscription |
| **Send the mint inscription** as an ordinal | The ordinal itself | The fungible balance |

The two are decoupled at the indexer level. Selling your mint inscription on an ordinals marketplace does not transfer the $BIT balance it originally produced — that lives in your wallet's TAP balance and moves only via `token-transfer`.

## Why this matters

For traders, $BIT behaves like any fungible token — quote it, swap it, route it. For collectors, the mint inscriptions form a complete collection — one per claimed Bitcoin block — with rarity and provenance tied directly to which block was claimed and by whom. Two markets, one asset, no wrapping required.
