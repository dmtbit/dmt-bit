# Why non-arbitrary

## The problem with arbitrary supply

Most token supplies are arbitrary. Somebody picked the number. Somebody decides the emission schedule. Somebody — usually with an admin key, a multisig, or a governance vote — can change it. That is a trust assumption baked into the asset itself. Even fair-launch tokens with a fixed cap had a person choose the cap; the "fixed-ness" is a promise, not a property of the universe.

## What "non-arbitrary" means here

$BIT's supply at any block is derived from that block's `bits` field — a number that Bitcoin's own consensus produced, via difficulty adjustment, via the cumulative work of every miner who contributed hashpower up to that point. No team picked it. No team can change it without changing Bitcoin itself. The supply is not a parameter of the token; it is a function of the chain.

## Trade-offs

| For | Against |
| --- | --- |
| Provable: anyone can decode `bits` from a node and verify the mint amount. | You can't model a fixed cap. Total supply depends on how many blocks ever get mined. |
| Verifiable: emission is computable from chain data alone, no trusted indexer required. | Per-block supply is variable across the chain's history — not a clean constant. |
| Anchored to actual proof-of-work, not to a team's chosen number. | Long-term total supply depends on how difficulty evolves, which nobody can predict. |
| No emission politics — no governance, no admin keys, no schedule changes. | Less convenient for tokenomics spreadsheets that assume a hard cap. |

## Why we accept the trade-off

For an asset whose entire premise is "the bit of Bitcoin," picking any arbitrary supply would betray the point. A team-chosen cap — however clean the round number, however rigorous the immutability promise — is still a team choice, and a team choice is the one thing this asset is supposed to not be. The supply has to be Bitcoin's own. Otherwise it is not the bit of Bitcoin; it is just another token with an orange logo.
