# Element

## What an element is

An `.element` is a text inscription on Bitcoin that **registers a namespace tied to a specific block-data field** (and optionally a pattern within that field). DMT indexers honor the first valid inscription for a given name as the canonical owner of that namespace. Once registered, the element becomes the reference point that any DMT [deploy](https://dmt-bit.com/docs/spec/deploy) must point at via its `elem` parameter.

## Element name format

Element names follow one of two shapes:

- With pattern: `<name>.<pattern>.<field>.element`
- Whole-field (no pattern): `<name>.<field>.element`

The four components:

- **`name`** — the project's namespace claim. Case-insensitive. First inscription wins.
- **`pattern`** — *optional*. Hex, string, or numeric value to match against the field. Mint quantity per block equals the count of pattern occurrences. Omit entirely for whole-field minting.
- **`field`** — required. Numeric index into the Bitcoin block JSON. See the field table below.
- **`.element`** — required suffix. Marks the inscription as an element registration.

## Field parameter table

| Field | Block JSON key | Type |
| --- | --- | --- |
| 4 | `height` | numeric |
| 10 | `nonce` | numeric |
| 11 | `bits` | hex |
| 12 | `difficulty` | numeric |
| 13 | `chainwork` | hex |
| 16 | `tx` (txid array) | array |

*Full field table is in the DMT GitBook. The fields most commonly referenced for DMT tokens are 4, 10, 11, and 16.*

## The element $BIT references

$BIT references **`dmt.11.element`** — a whole-field reference to Bitcoin's per-block `bits` value. This element is the canonical namespace for "DMT tokens of the bits field." It is shared infrastructure: any DMT token that wants to derive supply from `bits` points its deploy at this element.

**Multiple DMT tokens may reference the same element.** The element is the namespace registry — a shared pointer to a block-data field. The token is the [deploy](https://dmt-bit.com/docs/spec/deploy). One element can underlie many deploys with different tickers and supply rules. Element ≠ token.

## Whole-field vs pattern matching

**Whole-field** (no `<pattern>`): mint quantity per block equals the numeric interpretation of the field's value. The deploy's `dt` flag tells indexers how to decode the raw field (hex, numeric, string, etc.) into a number. $BIT uses this mode against the `bits` field.

**Pattern matching** (with `<pattern>`): mint quantity per block equals the count of pattern occurrences inside the field's value. This requires the `dt` flag in the deploy to specify the data type and `dim` to specify the matching dimension (`h`, `v`, `d`, `a`). Used for some other DMT tokens; not used by $BIT.

## Canonical references

| Resource | Inscription ID |
| --- | --- |
| `dmt.11.element` (element) | Resolved via the deploy inscription's `elem` field |
| $BIT deploy (`dmt-deploy`) | `9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0` |

**Always verify the deploy inscription ID before transacting.** Tickers in TAP are case-insensitive and unique-first-deploy. Imposters can inscribe lookalikes — the inscription ID is the only source of truth.
