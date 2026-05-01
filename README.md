# $BIT — The bit of Bitcoin

[![Website](https://img.shields.io/badge/website-dmt--bit.com-f7931a?style=flat-square)](https://dmt-bit.com)
[![BITpaper](https://img.shields.io/badge/read-the_BITpaper-white?style=flat-square)](https://dmt-bit.com/bitpaper)
[![Twitter](https://img.shields.io/badge/twitter-@dmt__bit___-1DA1F2?style=flat-square)](https://x.com/dmt_bit_)

This repository contains the open spec, documentation, and brand assets for
**$BIT**, a community Digital Matter Theory (DMT) token inscribed on Bitcoin
Ordinals via the [TAP Protocol](https://github.com/Trac-Systems/tap-protocol-specs).

> $BIT is named after the **`bits`** field — element 11 of the Bitcoin block
> header, the difficulty target. The same field that gives "bitcoin" its
> etymological root.

For the human-readable site, see **<https://dmt-bit.com>**.

---

## What $BIT is

- A **DMT token**, inscribed via TAP Protocol on Bitcoin Ordinals.
- **Fair-mint**, no presale, no team allocation, no insider round.
- **First valid inscription per `(ticker, block)` wins.** Mint by inscribing a
  standard `dmt-mint` JSON ordinal pointing at an unminted block.
- Mint quantity is derived deterministically from the block's `bits` field —
  no randomness, no oracle, no off-chain input.

Read the full thesis in the [BITpaper](https://dmt-bit.com/bitpaper).

---

## What this repository is — and is not

**This repository is** the public spec, documentation, and brand kit for $BIT.
It is the source of truth for protocol-level facts (deploy ID, mint format,
verification recipe).

**This repository is not** a wallet, a mint service, or an exchange. It does
not contain transactional code. It does not custody funds, sign transactions,
or process mints. Users mint $BIT by inscribing a JSON ordinal directly on
Bitcoin from their own wallet, using third-party TAP-aware tools.

---

## How to mint, in one minute

1. Get a TAP-aware ordinals wallet (e.g. the
   [TAP Wallet](https://www.tracsystems.io/tap-wallet) by Trac Systems, or any
   wallet that supports inscribing arbitrary JSON ordinals).
2. Pick an unminted Bitcoin block. Verify availability on a TAP indexer
   (e.g. [trac.network](https://trac.network/)).
3. Inscribe the following JSON, replacing `<BLOCK_HEIGHT>` with your target:

   ```json
   {
     "p": "tap",
     "op": "dmt-mint",
     "dep": "9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0",
     "tick": "bit",
     "blk": "<BLOCK_HEIGHT>"
   }
   ```

4. Pay the network fee. Wait for confirmation. Indexers credit the first valid
   inscription per block.

For the full step-by-step walkthrough, see
[**dmt-bit.com/docs/how-to-mint**](https://dmt-bit.com/docs/how-to-mint).

---

## Repository layout

```
.
├── README.md           ← you are here
├── LICENSE             ← MIT
├── spec/               ← protocol-level operations ($BIT-relevant subset of TAP)
│   ├── deploy.md       ← the dmt-deploy operation
│   ├── mint.md         ← the dmt-mint operation
│   ├── transfer.md     ← the token-transfer operation
│   └── element.md      ← the underlying DMT element ($BIT references field 11)
├── docs/               ← background, tokenomics, FAQs, glossary
│   ├── index.md
│   ├── how-to-mint.md
│   ├── verification.md
│   ├── overview-*.md   ← what $BIT is, the bits field, why it's non-arbitrary
│   ├── tokenomics-*.md ← supply expansion, hybrid token model
│   └── resources-*.md  ← FAQ, glossary
└── brand/              ← official logos, banners — free to use for community work
    ├── bit-logo.svg
    ├── bit-logo-transparent.svg
    ├── bit-logo-4096.png
    ├── bit-banner.svg
    ├── bit-banner-1500x500.png
    └── bit-banner-3000x1000.png
```

---

## Verification

The canonical $BIT deploy inscription is:

```
9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0
```

Anyone can independently verify the deploy and any mint by:

1. Fetching the inscription content from a Bitcoin Ordinals indexer.
2. Confirming `p: "tap"`, `op: "dmt-deploy"`, `tick: "bit"`.
3. Cross-checking against TAP indexer state (Trac, GeniiData, or any
   TAP-compliant indexer).

See [`docs/verification.md`](./docs/verification.md) for the recipe.

---

## Disclaimer

$BIT is a community-launched DMT token. **Not affiliated** with Bitcoin,
Bitcoin Core, the Ordinals project, TAP Protocol, or Trac Systems. References
to those projects in this repository are informational only.

There is **no team allocation, no presale, no airdrop, no rewards mechanism,
and no guaranteed return**. Tokens are volatile and may go to zero. Nothing
in this repository is investment, legal, tax, or financial advice. You are
responsible for your own decisions. Do not transact if you do not understand
what an Ordinal inscription, a TAP token, or a Bitcoin transaction fee is.

For the full disclaimer, see <https://dmt-bit.com/legal>.

---

## License

[MIT](./LICENSE). Use the spec, fork the docs, remix the brand. Attribution
appreciated but not required.

---

## Links & contact

- **Website**: <https://dmt-bit.com>
- **BITpaper**: <https://dmt-bit.com/bitpaper>
- **Documentation**: <https://dmt-bit.com/docs>
- **How to mint**: <https://dmt-bit.com/docs/how-to-mint>
- **Twitter / X**: <https://x.com/dmt_bit_>
- **Email**: <hello@dmt-bit.com>
- **About / disclaimer**: <https://dmt-bit.com/legal>
