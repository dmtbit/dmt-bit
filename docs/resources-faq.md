# FAQ

## Frequently asked questions

#### What is $BIT?

$BIT is a Bitcoin-native fungible token deployed via TAP Protocol on Ordinals. It mints from the `bits` field of every Bitcoin block — the 4-byte field that encodes difficulty. Each block can mint $BIT exactly once.

#### Why is it called BIT?

It's named after the `bits` field that drives its supply. The field is the name. As a bonus: `bit + coin = bitcoin` — the etymology lines up.

#### Is there a team allocation or premine?

No. $BIT is a fair-mint asset. Every $BIT in existence comes from someone inscribing a `dmt-mint` against a Bitcoin block — including any held by the people who deployed the ticker.

#### What does 

No team wallet. No presale. No reserved supply. The `dmt-deploy` inscription itself doesn't carry a balance — it just registers the ticker and parameters. To get $BIT, you (or anyone) inscribe a `dmt-mint` ordinal pointing at a block. First valid inscription wins that block.

#### How do I know which block to mint?

Use a TAP indexer to find unminted blocks. Older Bitcoin blocks emit larger $BIT quantities because the `bits` integer was numerically higher in the early difficulty regime. Demand for "rare" blocks (genesis, halvings, anniversaries, palindromes) tends to be higher. See [How to Mint](https://dmt-bit.com/docs/how-to-mint).

#### Why is $BIT supply variable per block?

Mint quantity per block equals the integer value of that block's `bits` field. The `bits` field encodes the difficulty target and changes every retarget (every 2016 blocks). So mints are not uniform — they shift with Bitcoin's difficulty history.

#### What happens when all blocks are minted?

New blocks land every ~10 minutes, so the mintable pool grows alongside Bitcoin itself. There is no point at which "all blocks are minted forever" — but at any given moment, the historical block range that's been claimed is bounded.

#### Can the project change the rules later?

No. The `dmt-deploy` inscription is immutable on Bitcoin. The element, ticker, and parameters cannot be modified after deploy. See [Deploy](https://dmt-bit.com/docs/spec/deploy).

#### Is $BIT affiliated with the DMT or TAP teams?

No. $BIT is a community-deployed DMT token. DMT is the framework; TAP is the protocol; we use both per their public specs. We are not endorsed by their authors and we do not speak for them.

#### Where can I ask more questions?

Public: [X](https://x.com/dmt_bit). Private: [hello@dmt-bit.com](mailto:hello@dmt-bit.com).
