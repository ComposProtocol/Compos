# BRC-20A

## **1 Initialize**

* TX0: deploy brc-20

```
{
  "p": "brc-20",
  "op": "deploy",
  "tick": "abcd",
  "max": "21000000",
  "lim": "21000000"
}
```

* TX1: mint total supply in one go

```
{
  "p": "brc-20",
  "op": "mint",
  "tick": "abcd",
  "amt": "21000000"
}
```

* TX2: deploy OCF

```
{
 "p": "ocf",
 "v": "0.1",
 "op": "deploy",
 "name": "raffle",
 "func": "fn valid_if(para: &[String]) -> bool { return get_brc20_tick(&get_ord_id(), 0) == \\"abcd\\" && get_brc20_amt(&get_ord_id(), 0) <= 1000.0 && para[0].as_bytes()[0] as char == get_block_hash(get_block_number()).chars().last().unwrap();}"
}
```

* Following the OCF example, the `func` uses only one line of code to create a simple lottery game on Bitcoin: users place their bets on the last character of the block's hash in their minted OCF inscription. If they guess correctly, they successfully mint 1,000 `$abcd` BRC-20A tokens.
* **Attention:** Since BRC-20A is compatible with BRC-20, TX0 and TX1 must be separate transactions. Separate outputs or same-sats cannot be used for BRC-20 inscription, as the BRC-20 protocol currently does not support these features.

## **2 Deploy BRC-20A**

* TX3: deploy BRC-20A (Attention: Within a single BRC-20A inscription, only a combination of 1 OCF and 1 BRC-20 is supported. Support for multiple combinations will be available in the future).

```
{
	"p": "compos",
	"v": "0.1",
	"op": "deploy",
	"comp": ["brc-20", "ocf"],
	"init": [
		"/content/tx0idi0",
		"/content/tx1idi0",
		"/content/tx2idi0"
	]
}
```

* Here, the order of inscription IDs in the `init` corresponds to the sequence in `comp`: if `comp` starts with BRC-20, then the first inscription ID corresponds to the deployment inscription of BRC-20, the second inscription is the completion of the BRC-20 minting, followed by the deployment inscription of OCF.
  * We recommend placing BRC-20 first in the `comp` and OCF last, for instance, `["brc-20", "ocf"]`.
  * If the quantity or order in `comp` and `init` do not align, the BRC-20A deployment inscription is considered invalid.

## **3 Mint BRC-20A**

The format for minted inscriptions is as follows:

```
[Referenced Deployment Inscription, Inscription 1, Inscription 2]
```

Assuming `/content/tx3idi0` is a valid deployment inscription for BRC-20A, using the lottery mentioned above as an example, the BRC-20A minting inscription would be:

```
[
	"/content/tx3idi0",
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

**Attention:** If the deployed `func` requires sending BTC to a specific address (such as the deployer's address), often implemented via the `txo_exist` function, then beyond the inscription's body, the transaction output in which the inscription resides must also satisfy the conditions of the OCF inscription.

## **4 Transfer BRC-20A**

Transferring BRC-20A tokens is the same as the transfer process of BRC-20.

1. Inscribe the transfer function to your ordinal compatible wallet. Make sure the transfer function inscription information is valid before inscribing.
   1. **Be careful when using an inscription service. Some inscription tools inscribe to themselves first and then transfer it to the customer (when the intermediate inscription service-owned address has no balance and the transfer function is invalid). Some ordinal wallets generate a different address each time. Make sure to send it to the address that holds the balance.**
2. Once received and if valid, send the inscription to the desired destination to transfer the balance.

## **5 Convert between BRC-20A and BRC-20**

Currently, the BRC-20A deployer holds all the balance of the counterpart BRC-20 token. As a result, the conversion service should be implemented and deployed by the BRC-20A deployer.

We expect custody conversion services (similar to a general ERC-20 token bridge) to become available. A protocol-level solution is also possible.
