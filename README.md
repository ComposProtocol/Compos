# Introduction

Compos Protocol enhances existing Bitcoin Layer 1 protocols like BRC-20, Runes, and Ordinals by combining an asset inscription (e.g., BRC-20) with a logic inscription. This combination introduces powerful features to the original asset protocols, leveraging the capabilities of both layers.

For instance, combining BRC-20 asset inscriptions with OCF logic inscriptions within the Compos Protocol framework unlocks features like native X-To-Earn on the Bitcoin blockchain. This integration enables the creation of tokens with embedded logic, allowing for conditional fair launches where users must perform actions (X) to inscribe the token. This new method of distributing tokens, which requires user engagement or participation (such as playing or socializing), exemplifies the concept of X-To-Inscribe.

The role of OCF (On-Chain-Function) is a crucial part of the Compos Protocol to achieve native X-To-Earn capabilities on the Bitcoin network, in which you can write smart contracts using Rust and deploy to CVM, a virtual machine we implemented using WASM on Bitcoin.

Compos Protocol can integrate different protocols with logic inscriptions in the BTC ecosystem. With our initial rollout, Phase 1 will support BRC-20. Further down the road, Phase 2 will support Ordinals NFT.

Phase 1: BRC-20 + OCF = BRC-20A

Phase 2: Ordinals NFT + OCF

Phase 3: Runes + OCF

Here's an example of a BRC-20A inscription:

```json
[
  "/content/txidi0", // refers to the deploy insciption
  {
    "p": "brc-20",
    "op": "mint",
    "tick": "acbd",
    "amt": "1000"
  },
  {
    "p": "ocf",
    "op": "call",
    "name": "raffle",
    "params": ["a"]
  }
]
```

Compos Inscription has the following components:

* Part 1 refers to a BRC-20A deploy inscription that defines a `raffle` function.
* Part 2 refers to a BRC-20 inscription of minting ticker `abcd` with an amount of `1000`.
* Part 3 refers to an OCF inscription that calls the function `raffle` and passes params of `["a"]`.

The whole Compos inscription is valid if the called function returns `true`, and therefore, minting the `abcd` token requires calling `raffle` with the proper `params`.

