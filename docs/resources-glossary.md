# Glossary

## Terms

**`bits`** — The 4-byte field in every Bitcoin block header that encodes the network's difficulty target. Field 11 in DMT's element registry. The source of $BIT supply.

**DMT (Digital Matter Theory)** — A Bitcoin-native framework for creating tokens whose supply is derived deterministically from data inside Bitcoin blocks. Built on top of TAP Protocol. See [Digital Matter Theory](https://dmt-bit.com/docs/overview/digital-matter-theory).

**`dmt-deploy`** — The TAP operation that registers a DMT token. One-time per ticker, first-deploy-wins. See [Deploy](https://dmt-bit.com/docs/spec/deploy).

**`dmt-mint`** — The TAP operation that claims a DMT token's supply attached to a specific Bitcoin block. See [Mint](https://dmt-bit.com/docs/spec/mint).

**Element (`.element`)** — A text inscription on Bitcoin that registers a namespace bound to a block-data field. See [Element](https://dmt-bit.com/docs/spec/element).

**Fair-mint** — A token launch with no team allocation, presale, or reserved supply. Every unit comes from public minting.

**Field 11** — The DMT element registry's index for Bitcoin's `bits` field. The element name `dmt.11.element` references this field.

**First-deploy-wins** — TAP convention: the first valid inscription registering a given ticker is canonical; subsequent deploys of the same ticker are ignored.

**First-valid-inscription wins** — TAP convention for mints: per (ticker, block), only the first valid `dmt-mint` is honored. Same rule, different scope.

**Hybrid token model** — A property of DMT mints: each mint inscription is simultaneously a fungible balance and a non-fungible ordinal. See [Hybrid token model](https://dmt-bit.com/docs/tokenomics/hybrid-token-model).

**Indexer** — A service that reads Bitcoin block data and Ordinals inscriptions, replays valid TAP operations, and maintains authoritative token balances. Trac and GeniiData are common TAP indexers.

**Inscription** — An Ordinals concept: arbitrary content (text, JSON, image, etc.) recorded on Bitcoin via taproot witness data, anchored to a specific sat. TAP operations are inscriptions.

**Mantissa (coefficient)** — The 3-byte significand of the `bits` field. Combined with the exponent to compute the full difficulty target.

**Non-arbitrary token (DMT term)** — A token whose supply parameters are derived from public chain data rather than chosen by a team.

**Ordinal** — An individual sat tracked by Ordinals theory. Inscriptions are anchored to ordinals.

**TAP Protocol** — A token-layer protocol on Bitcoin Ordinals. Defines token operations like deploy/mint/transfer via JSON inscriptions. DMT extends TAP with `dmt-deploy` and `dmt-mint` opcodes.

**Ticker** — A token's short name. Case-insensitive in TAP. 3 or 5–32 UTF-16 chars. Unique-first-deploy.

**`token-transfer`** — TAP operation for moving fungible balances between wallets. For DMT tokens, ticker is prefixed with `dmt-`. See [Transfer](https://dmt-bit.com/docs/spec/transfer).

**Whole-field minting** — A DMT element configuration where mint quantity per block equals the integer value of the entire field, with no pattern matching. $BIT uses this mode.

Missing a term? Ask on X.
