# Digital Matter Theory

## The thesis

Bitcoin blocks are immutable records of work. The data inside them — fields like `bits`, `nonce`, `time`, and the transactions and hashes they contain — is **non-arbitrary**: nobody chose any of it, it emerged from mining and from the chain's own consensus rules. DMT — Digital Matter Theory — proposes that this non-arbitrary data is the natural starting matter for new on-chain assets. If you want a scarce digital thing whose existence isn't a marketing decision, the most credible source is the chain itself.

## Mechanics (high-level)

DMT defines a registry of **elements**. Each element points at a specific field — and optionally a pattern within that field — inside Bitcoin block data. To mint a DMT token, a user inscribes a TAP `dmt-mint` ordinal that references an element identifier and a target block. The mint quantity for that inscription is derived from the target block's data at the chosen field. The first valid inscription per `(token, block)` pair wins; subsequent attempts on the same block are rejected by indexers.

Tokens are deployed once via a TAP `dmt-deploy` inscription, which fixes the element, the start and end block, and any other constraints. From that point on, the deploy is immutable.

DMT is **not a separate chain or sidechain**. It is an inscription-layer convention on Bitcoin L1, indexed by TAP Protocol. Every `dmt-mint` is a Bitcoin transaction; the canonical state lives in Bitcoin itself, with TAP indexers reading and validating it.

## Why this matters

- **Provable scarcity from native Bitcoin data.** Supply is computed from the chain — anyone running a node can verify it.
- **No team-controlled emission curve.** There is no admin key, no upgradeable contract, no parameter that a deployer can tune after the fact.
- **Supply is a function of the chain's own physics.** Difficulty, nonce distributions, timestamps — these are properties of mining, not of any team's discretion.
- **Immutable by Bitcoin's own consensus.** A DMT token's history cannot be rewritten without rewriting Bitcoin.

## Where to read more

  
#### DMT GitBook

    The protocol's canonical reference.
  
  
#### TAP Protocol specs

    The token-layer protocol that DMT extends.
