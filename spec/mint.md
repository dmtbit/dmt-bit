# Mint

## What mint does

A `dmt-mint` inscription claims the $BIT supply attached to a specific Bitcoin block. Each block can be minted exactly once per token — the first valid inscription per `(ticker, block)` pair wins, and any later attempt against the same block is rejected by indexers. There is no rate limit beyond that and no privileged minter; whoever inscribes first earns the block's supply.

## Schema

```json
{
  "p": "tap",
  "op": "dmt-mint",
  "dep": "9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0",
  "tick": "bit",
  "blk": "14257"
}
```

## Parameters

| Field | Type | Required | Description |
|---|---|---|---|
| `p` | `string` | yes | Protocol identifier. Always "tap". |
| `op` | `string` | yes | Operation. Always "dmt-mint". |
| `dep` | `string` | yes | Inscription ID of the canonical $BIT dmt-deploy. Indexers reject mints that point at any other deploy. |
| `tick` | `string` | yes | Ticker being minted. For $BIT this is "bit". Case-insensitive. |
| `blk` | `string` | yes | Block height to claim, as a string. Must be an unminted block within the token's allowed range. First-valid wins. |

**First is first.** If two mint inscriptions target the same block, the first to confirm on Bitcoin wins. The other is invalid — no partial credit, no refund of network fees.

## How quantity is determined

For $BIT (a whole-field token referencing field 11), the mint quantity equals the numeric interpretation of that block's `bits` value. The `dt: "n"` flag in the deploy instructs indexers to decode the hex field as a base-10 integer.

```text
block 840000
bits     = 0x1703a30c
integer  = 385948428
=> $BIT minted = 385,948,428
```

*Final mint function for $BIT (full integer vs mantissa-only vs another transformation) is being finalized. The example above uses the full-integer reading. See the bitpaper at launch for the locked spec.*

## Mint flow

**Pick a target block.** Choose a block height that hasn't been minted yet. Verify availability on a TAP indexer (e.g. Trac, GeniiData) before paying for the inscription.

**Fill in the JSON.** Set `dep` to the canonical $BIT deploy inscription ID, `tick: "bit"`, and `blk` to your target height as a string.

**Inscribe.** Use a TAP-aware ordinals tool to inscribe the JSON. Pay the network fee. Higher fee rate = faster confirmation = better odds in a contested block.

**Wait for confirmation.** Once the inscription confirms and the indexer validates it, your wallet is credited with the calculated $BIT amount. The inscription itself stays in your wallet as a hybrid asset (see below).

## Hybrid mint

Each mint inscription is **simultaneously fungible and non-fungible**. The fungible side is the $BIT amount credited to your wallet — spendable and divisible via [token-transfer](https://dmt-bit.com/docs/spec/transfer). The non-fungible side is the inscription itself: a unique ordinal pointing at a specific block, transferable or sellable on any ordinals marketplace like any other inscription. You hold both at once, and they move independently — sending the inscription to a buyer does not move the fungible balance, and a `token-transfer` does not move the inscription.

## Rules

- Each block ⇒ at most one valid mint per ticker. First confirmed wins.
- The deployer cannot mint preferentially. There is no premine and no admin path.
- The block must be within the token's allowed range. For $BIT, any Bitcoin block is mintable — first-valid-inscription wins per `(ticker, block)`.
- `blk` is a string. Indexers reject numeric `blk` values.
- `dep` must be the canonical $BIT deploy inscription ID. Mints pointing at any other deploy are not $BIT mints.
