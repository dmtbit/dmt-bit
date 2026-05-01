# Verification

## Why verify

TAP tickers are first-deploy-wins and case-insensitive. Imposters can deploy lookalike tickers. The **deploy inscription ID** is the only ground truth. Always verify before transacting or extending trust.

## Canonical references

| Resource | Inscription ID |
| --- | --- |
| $BIT element (`dmt.11.element`) | Resolved via the deploy's `elem` field |
| $BIT deploy (`dmt-deploy`) | `9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0` |
| First mint inscription | Look up the lowest `blk` minted on a TAP indexer for ticker `bit` |

Always confirm the deploy inscription ID matches the one published on this docs site **and** the project's official X. If they disagree, do not transact.

## How to look up a $BIT mint

Use a TAP indexer (Trac, GeniiData, etc.) to query the ticker `bit` for any block, wallet, or inscription. Indexers maintain authoritative balances by replaying every TAP-valid inscription. If an indexer disagrees with another indexer, check both against the raw inscription JSON on-chain — the chain is the tiebreaker.

Look up the inscription ID on `ordinals.com` or a similar explorer. The raw JSON of the inscription is visible. Confirm the JSON contains:

- `"op": "dmt-mint"`
- `"tick": "bit"`
- `"dep": <canonical deploy ID>`
- the target `"blk"` as a string

If any field is off, the mint is invalid regardless of what a third-party UI shows.

A TAP-aware wallet displays your $BIT balance directly. The number you see should match what an indexer reports for your address. If they don't match, prefer the indexer — wallet UIs sometimes lag, cache, or filter.

## Spotting fakes

- The deploy inscription ID **must match** the one published here.
- The element referenced by the deploy **must be `dmt.11.element`** (the canonical element ID at launch).
- Tokens prefixed `dmt-` in transfer ops are TAP convention. A `token-transfer` with `tick: "bit"` (no `dmt-` prefix) won't be honored.
- Be wary of marketplaces listing "BIT" tokens that don't reference the canonical deploy. Other tokens might use the same ticker via different deploys — indexers may track multiple deploys for the same ticker, but only the first valid one is canonical. The deploy inscription ID is the only thing that can't be spoofed.

For the mint flow itself, see [How to mint $BIT](https://dmt-bit.com/docs/how-to-mint).
