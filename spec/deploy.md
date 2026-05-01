# Deploy

## What deploy does

A `dmt-deploy` inscription tells TAP indexers "from now on, this ticker is a DMT token whose supply is mined from this element." It binds a ticker to an [element](https://dmt-bit.com/docs/spec/element), fixes the supply derivation rules, and opens the token to public minting. It is a one-time act per ticker — the first valid inscription wins, and every subsequent deploy with the same ticker is ignored.

## Schema

```json
{
  "p": "tap",
  "op": "dmt-deploy",
  "elem": "<element_inscription_id>",
  "tick": "bit",
  "prj": "<optional_project_inscription_id>",
  "dim": "h | v | d | a",
  "dt": "h | n | x | s | b",
  "id": "<optional_unat_content_inscription_id>"
}
```

## Parameters

| Field | Type | Required | Description |
|---|---|---|---|
| `p` | `string` | yes | Protocol identifier. Always "tap". |
| `op` | `string` | yes | Operation. Always "dmt-deploy". |
| `elem` | `string` | yes | Inscription ID of the .element this token references. |
| `tick` | `string` | yes | Ticker. Case-insensitive. 3 or 5-32 UTF-16 chars. Unique-first-deploy. |
| `prj` | `string` | no | Inscription ID of an existing project (e.g. 0.bitmap). Reserves the namespace within that project. |
| `dim` | `string` | no | Dimension when matching a pattern: "h" horizontal, "v" vertical, "d" diagonal, "a" sum of h+v+d. Required when element has a pattern. |
| `dt` | `string` | no | Data type for interpreting the field value: "h" hex, "n" numeric, "x" unix-time, "s" string, "b" boolean. Required when element has a pattern. |
| `id` | `string` | no | Inscription ID of UNAT render content (script, image, model). Optional — used to attach renderable per-mint content. |

## $BIT deploy

For $BIT, the deploy uses `tick: "bit"`, `elem` set to the `dmt.11.element` inscription ID, `dt: "n"` (decode the `bits` field as a numeric integer rather than raw hex), no pattern, no `prj`, and no `id`. The canonical $BIT deploy is at inscription `9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0` — fetch it on `ordinals.com` to inspect the full payload.

```json
{
  "p": "tap",
  "op": "dmt-deploy",
  "elem": "<element_inscription_id>",
  "tick": "bit",
  "dt": "n"
}
```

## Rules and gotchas

- The first valid `dmt-deploy` for a given ticker wins. Every subsequent deploy of the same ticker is ignored by indexers.
- Tickers are **case-insensitive**. `bit`, `BIT`, and `Bit` collide and resolve to the same namespace.
- Once deployed, the spec is **immutable**. The element, ticker, and parameters can't be changed. There is no upgrade path — a new ticker would mean a new token.
- The deployer wallet has no ongoing privilege after deploy. There is no admin key, no premine, no preferential mint. Mints are open to anyone on equal terms.
- Tickers must be 3 characters or 5–32 UTF-16 characters. Lengths of 1, 2, and 4 are not allowed.

## See also

- [Mint](https://dmt-bit.com/docs/spec/mint) — how `dmt-mint` claims supply from a specific block
- [Element](https://dmt-bit.com/docs/spec/element) — what `elem` points at and why
