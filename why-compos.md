# Why Compos?

Compos Protocol, a unique smart contract layer for Bitcoin, introduces many innovations on Bitcoin but still maintains compatibility and stability by offering a two-way conversion mechanism. **This mechanism ensures 100% compatibility with existing Bitcoin token protocols like BRC-20, Runes, and Ordinals NFT.**

**BRC-20A** is the first token standard using Compos Protocol, unlocking potential experimentations and innovations for BRC-20 tokens. Holders and developers utilizing BRC-20A enjoy the benefits of new features brought by Ordinals while retaining the stability, security, and support of various original BRC-20 infrastructures.

For developers, the protocol mandates the deployment of a BRC-20 token before minting the corresponding BRC-20A token with the same name. This requirement ensures support for users converting between BRC-20A tokens and BRC-20 tokens and opens up new possibilities for experimentation and innovation.

Users holding BRC-20A tokens, who prefer to keep the asset without any on-chain interactions, can opt to convert them into BRC-20 tokens, which offer enhanced stability and security. Users can perform the conversion any number of times and at any moment. When converting a BRC-20A token into a BRC-20 token, the protocol will transfer the corresponding BRC-20A token to a locked address and vice versa. After converting to BRC-20, users can trade on any well-known BRC-20 trading markets such as OKX, Binance, Unisat, etc., enabling them to seamlessly integrate and leverage the comprehensive infrastructures inherent to the BRC-20 ecosystem.

The following diagram illustrates the conversion process between BRC-20A and BRC-20:

<figure><img src=".gitbook/assets/image-20240329152201720 (1).png" alt="" width="563"><figcaption><p>Conversion between BRC-20A and BRC-20</p></figcaption></figure>

In addition to smart contract features, **BRC-20A supports the Jubilee upgrade and Batch Inscribe**. Users can inscribe multiple BRC-20As inscriptions on a single UTXO, significantly saving costs. In separate-outputs mode, it can save over 50% of fees, and in same-sats mode, **even more than 90%**, far exceeding CBRC-20. For instance, if a user wants to inscribe 100 times BRC-20 tokens, they can do so with one transaction using BRC-20A's same-sats and then convert them into BRC-20 tokens with another transaction. Effectively, this equates to accomplishing merely two transactions that previously required a hundred separate transactions to achieve the same quantity of BRC-20 tokens.

\
