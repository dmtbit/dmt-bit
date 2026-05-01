# $BIT Documentation

$BIT is a Bitcoin-native fungible token deployed via TAP Protocol on Ordinals, with supply derived from the `bits` field of every Bitcoin block. These docs are the technical and conceptual reference: what $BIT is, how the mint works, the tokenomics, and how to participate.

**The bit of Bitcoin.** Mined from the bits field of every Bitcoin block since genesis.

## Sections

  
#### What is $BIT

    The token, the thesis, and what it is not.
  
  
#### The bits field

    Field 11 in the DMT registry — encoding, range, verification.
  
  
#### Mint spec

    TAP `dmt-mint` payload format and validation rules.
  
  
#### Tokenomics

    Per-block emission, supply curve, retarget effects.
  
  
#### How to mint

    Walkthrough for inscribing a $BIT mint.
  
  
#### FAQ

    Common questions and edge cases.
  

## Status

$BIT is **live**. The canonical deploy is at inscription `9424802e38fc889969417cd90df4c4147209d2a83ed83798c0c4aa4391ad36e5i0`. Any unminted Bitcoin block is mintable on a first-valid-inscription-wins basis. See [How to mint](https://dmt-bit.com/docs/how-to-mint) for the flow.
