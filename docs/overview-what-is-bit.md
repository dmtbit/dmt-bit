# What is $BIT

## A token of the bits field

$BIT is a TAP-protocol DMT token whose supply is mined from the integer value of the `bits` field of Bitcoin blocks. Every Bitcoin block — from genesis to the current tip — carries one `bits` field in its header, and each block is eligible to mint $BIT exactly once.

Once a block has been claimed by a valid mint inscription, it is claimed forever. There is no reissue, no second chance, no admin override. The set of mintable blocks is the set of Bitcoin blocks that exist; the set of claimed blocks grows monotonically as people inscribe.

## Why "BIT"

The name has three layers of meaning, and they all align:

- **The field name.** `bits` is a literal field in the Bitcoin block header — the difficulty encoding that every node parses on every block.
- **The etymological root.** The Bitcoin whitepaper coins the word from `bit + coin`. "Bit" predates "Bitcoin"; it is what Bitcoin is built out of.
- **The unit of information.** Per Shannon, a bit is the smallest possible unit of information. Bitcoin is a chain of bits. $BIT is a token of that chain.

## What it is not

- Not a layer-2 token. $BIT lives on Bitcoin L1 as Ordinals inscriptions.
- Not wrapped, bridged, or pegged. There is no off-chain custodian and no cross-chain mirror.
- Not a presale or ICO. There is no team allocation, no pre-mine, no fundraising round.
- Not a memecoin in the disposable sense. The supply is a function of Bitcoin's chain data, not a marketing decision.

$BIT is an Ordinals-native fungible token deployed through TAP Protocol, with supply derived deterministically from Bitcoin block headers.

## How it relates to DMT

DMT — Digital Matter Theory — is a Bitcoin-native framework for tokens whose supply is derived from Bitcoin block data rather than being chosen by a team. DMT was first deployed in 2023 and defines a registry of "elements," each pointing at a specific field inside a block. A DMT token is minted by inscribing a TAP `dmt-mint` ordinal that references a target block; the mint quantity is computed from that block's data at the chosen field.

$BIT is a DMT token, and the field it references is `bits` — element 11 in the DMT registry. For the framework itself, see [Digital Matter Theory](https://dmt-bit.com/docs/overview/digital-matter-theory).

## Next

  
#### The bits field

    What `bits` is, how it's encoded, and why DMT picks it.
  
  
#### Mint spec

    The exact TAP payload to inscribe a $BIT mint.
