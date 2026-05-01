# How to mint $BIT

## Before you start

Minting $BIT means inscribing a small JSON ordinal on Bitcoin that claims a specific block's `bits` value. This is the same flow as any TAP DMT token mint. You'll need a TAP-aware ordinals wallet, BTC for fees, and the canonical $BIT deploy inscription ID.

**$BIT is live.** Canonical deploy inscription:
`9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0`. Always verify this ID against an authoritative source (e.g. the project's X profile) before transacting.

## What you need

- A **TAP-aware ordinals wallet** — any ordinals-capable Bitcoin wallet that supports inscribing arbitrary text inscriptions. Examples: Unisat, OrdinalsWallet, or any wallet with an inscribe/text endpoint.
- **BTC for inscription fees**. The fee covers the Bitcoin transaction that carries your inscription. A tiny JSON inscription is cheap, but witness data costs more during mempool congestion.
- The canonical **$BIT deploy inscription ID**: `9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0`.
- A **target block height** to claim that hasn't been minted yet.

## Step-by-step

### Pick an unminted block

Use a TAP indexer to find a block that hasn't been claimed yet. Search by ticker `bit` for the list of already-minted blocks; pick anything not on it. **First-valid-inscription wins** per block, so be ready to broadcast.

### Open your TAP-aware wallet

Make sure it's funded with BTC for the inscription fee. The amount depends on the current mempool — typically a few thousand sats for a tiny JSON inscription, more during high traffic.

### Compose the mint inscription

Copy the JSON below and set `blk` to your chosen block height. The `dep` field is already filled in with the canonical $BIT deploy inscription.

```json
{
  "p": "tap",
  "op": "dmt-mint",
  "dep": "9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0",
  "tick": "bit",
  "blk": "14257"
}
```

**`tick` must be exactly `"bit"` (lowercase). `blk` must be a string of digits, not a JSON number.** The example above mints block 14257 — replace it with whichever unminted block you want to claim.

### Inscribe the JSON

In your wallet's "Inscribe" or "Inscribe Text" flow, paste the JSON above. Most wallets will let you preview the resulting ordinal. Confirm and pay the fee.

### Wait for confirmation

Bitcoin confirms blocks roughly every 10 minutes. Once your inscription confirms, TAP indexers will validate it. If you were the first valid mint for that block, your wallet's $BIT balance increases by the amount derived from the block's `bits` value.

### Verify

Open your wallet's TAP balance view, or look up your wallet on a TAP indexer. You should see your $BIT balance and the ordinal mint inscription. The inscription itself is also a one-of-one ordinal — visible in any ordinals explorer.

## Rules and gotchas

#### First valid inscription wins

If two mints target the same block, only the first one to confirm on Bitcoin wins. The other is rejected by indexers, but you still pay the inscription fee. Don't fight gas wars on contested blocks unless you mean it.

#### Tickers are case-insensitive

`bit`, `BIT`, `Bit` all collide. Use lowercase to match the deploy and avoid surprises in tooling that does its own normalization.

#### `amt` is a string

Same for `blk`. JSON numbers (without quotes) will be rejected by some indexers. Always quote numeric fields in TAP JSON.

#### Fee != mint cost

The Bitcoin transaction fee is what you pay. There is no separate mint fee for $BIT — the protocol is fee-free at the token level. You pay miners, not the project.

#### Reorgs

Bitcoin reorgs are rare but possible. If your inscription is in a reorged block and someone else claims first in the new chain, you lose. In practice, wait a few confirmations for high-value mints.

## Where to verify a mint

See [Verification](https://dmt-bit.com/docs/verification) for canonical lookup endpoints, indexer references, and how to spot fakes.

## Help / questions

Ask on X. The community is small and direct — no Discord/Telegram support channel.
