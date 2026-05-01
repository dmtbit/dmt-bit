# Transfer

## What transfer does

A `token-transfer` inscription moves a specified quantity of fungible $BIT from your wallet to another. The inscription itself, when sent to a destination address, executes the transfer at indexer level — there is no on-chain "send" call. Inscribe, then send the resulting ordinal to the recipient. Indexers reconcile balances when the send confirms.

## Schema

```json
{
  "p": "tap",
  "op": "token-transfer",
  "tick": "dmt-bit",
  "amt": "1000"
}
```

**The transfer ticker is prefixed with `dmt-`** (i.e. `dmt-bit`, not `bit`). This is a TAP convention for fungible transfers of DMT tokens. The `dmt-deploy` and `dmt-mint` operations use the bare ticker (`bit`); only `token-transfer` uses the `dmt-` prefix.

## Parameters

| Field | Type | Required | Description |
|---|---|---|---|
| `p` | `string` | yes | Protocol identifier. Always "tap". |
| `op` | `string` | yes | Operation. Always "token-transfer". |
| `tick` | `string` | yes | Transfer ticker. For $BIT this is "dmt-bit" — note the dmt- prefix, which is required for fungible transfers of DMT tokens. Case-insensitive. |
| `amt` | `string` | yes | Quantity to transfer, as a string. Cannot exceed your $BIT account balance. |

## Flow

**Inscribe to yourself.** Inscribe the `token-transfer` JSON to your own wallet. The inscription becomes a "transferable" balance — earmarked but not yet sent.

**Send the inscription.** Send the resulting ordinal to the recipient's Bitcoin address as you would any inscription. Use a TAP-aware wallet so the inscription is treated as a transfer payload, not just an ordinal.

**Wait for confirmation.** Once the send confirms, indexers debit your $BIT balance and credit the recipient's by `amt`.

## Rules

- `amt` must be a string, not a JSON number. `"1000"` is valid; `1000` is not.
- `amt` cannot exceed your current $BIT balance. Over-sized transfers are rejected by indexers.
- The fungible (`token-transfer`) and non-fungible (the original [mint](https://dmt-bit.com/docs/spec/mint) inscription) sides of $BIT transfer **independently**. A `token-transfer` does NOT move the original mint inscription, and sending a mint inscription does NOT move the fungible balance.
- A transfer inscription is one-shot: once it has been used to move the balance, it has no further effect.

## Compatibility

Any TAP-aware wallet handles `token-transfer` natively. The flow is identical to every other TAP fungible — there is no $BIT-specific transfer path. If your wallet can send TAP tokens, it can send $BIT.
