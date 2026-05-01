# Supply expansion

## No fixed cap

$BIT does not have a fixed maximum supply. The total supply at any moment equals the sum of $BIT minted from all claimed blocks so far. New blocks can always be minted as Bitcoin produces them, until the protocol's allowed range is exhausted, if any.

## Per-block emission

Each Bitcoin block contributes a quantity of $BIT equal to the integer value of its `bits` field. Bitcoin blocks land roughly every 10 minutes, so $BIT supply expansion tracks Bitcoin's block production — no team-controlled emission schedule, no inflation curve set in advance.

## The supply curve declines over time

Bitcoin's `bits` field encodes the difficulty target. As the network's hashrate grows, difficulty rises, and the `bits` integer **falls**. So per-block $BIT mints get smaller over time. The math is a function of Bitcoin itself, not a token-team decision.

Concretely: early Bitcoin blocks had higher `bits` values; modern blocks (post-2024) have much lower ones. The earliest blocks mint the most $BIT. Late blocks mint less.

| Block | Approx. bits integer | Approx. $BIT mint |
| --- | --- | --- |
| 1 | ~486,604,799 | ~487M |
| 100,000 | ~452,491,029 | ~452M |
| 500,000 | ~402,841,392 | ~403M |
| 800,000 | ~386,220,668 | ~386M |
| 840,000 | ~385,948,428 | ~386M |

*Approximate values for illustration. Final mint function (full integer vs other transformation) is being finalized — see the bitpaper at launch.*

## What this means for holders

- **Older blocks are scarcer to claim** — once minted, they're gone forever, and they emit the largest $BIT amounts.
- **No emission schedule from the team** — emission is whatever Bitcoin blocks have produced.
- **Variable per-block reward** — $BIT minted per block is not constant, unlike most fixed-reward tokens.

## Compared to Bitcoin's own supply

Bitcoin caps at 21M coins via halvings. $BIT does not — it follows the `bits` field, which has no hard cap. They share the cadence (per-block) but not the math: Bitcoin halves on a schedule; $BIT decays continuously with difficulty.

$BIT uses the **whole-integer** reading of the `bits` field. Each block's `bits` is decoded directly to its base-10 integer value, and that integer is the $BIT amount minted by the first valid inscription for that block.
