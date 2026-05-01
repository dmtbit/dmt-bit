# The bits field

## What it is

The `bits` field is part of every Bitcoin block header. It encodes the network's target difficulty for that block — the threshold a block hash must beat to be considered valid by consensus. Every node verifies it, every block has it, and its value is set deterministically by Bitcoin's difficulty-retarget rules. It is a 4-byte field, represented as 8 hexadecimal characters in standard tooling.

## Encoding

`bits` is a compact 4-byte representation of a 256-bit target. The structure is **1 byte of exponent followed by 3 bytes of mantissa (coefficient)**.

The decoded difficulty target is computed as:

```text
target = mantissa × 2^(8 × (exponent − 3))
```

DMT does not use the decoded target. It references the **integer value of the raw 4-byte field itself** — i.e. the `bits` value parsed as a single big-endian unsigned integer.

```text
bits     0x1703a30c
exp      0x17 (23)
coeff    0x03a30c (238860)
integer  385948428
```

## Why DMT picks this field

The `bits` field changes only at difficulty retargets — once every 2,016 blocks, roughly every two weeks. Between retargets, `bits` is constant; at each retarget, it adjusts to track network hashrate. As difficulty rises, the integer encoding of `bits` falls, and as difficulty falls, the integer rises.

This makes the `bits` value a slow-moving function of Bitcoin's actual security: a per-block number that everyone agrees on, that no one chose, and that loosely tracks the chain's own physics. A supply curve anchored to `bits` declines as the network grows — mirroring the spirit (if not the math) of Bitcoin's halving cadence.

## Range

Per the Bitcoin protocol, `bits` values have historically spanned roughly `0x17000000` to `0x1d00ffff`. The integer encoding is therefore non-uniform across the chain's history, often producing per-block mint quantities in the tens of millions.

The **exact mint function** for $BIT — whether it uses the full integer, the exponent only, the mantissa only, or another transformation of the `bits` field — is being finalized. See the bitpaper for the canonical definition once published.

## In the DMT element registry

DMT's element registry assigns numbered fields to keys in Bitcoin's block JSON. Field `11` is `bits`. The element name `dmt.11.element` represents the whole-field reference; this is the element identifier a $BIT mint inscription points at. Element-name conventions and the full registry are defined by the DMT specification.

## Verification

Anyone can independently decode the `bits` field of any Bitcoin block. Standard sources include a local Bitcoin Core node (`getblockheader <hash>`), any block explorer, and the raw block hex. Because `bits` is part of the block header, it is covered by Bitcoin's own consensus and proof-of-work — it cannot be altered without re-mining the block.

The mint quantity for any given block is therefore deterministic and verifiable from chain data alone, with no reliance on an indexer's good behavior.
