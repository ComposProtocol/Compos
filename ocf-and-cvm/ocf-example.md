# OCF Example

Here, we demonstrate a simple on-chain lottery game in which users must correctly guess the last character of the next block's hash to successfully mint the BRC-20A token `$abcd` .

The OCF part could be written as follows:

```
{
	"p": "ocf",
	"v": "0.1",
	"op": "deploy",
	"name": "raffle",
	"func": "fn valid_if(para: &[String]) -> bool { return get_brc20_tick(&get_ord_id(), 0) == \"abcd\" && get_brc20_amt(&get_ord_id(), 0) <= 1000.0 && para[0].as_bytes()[0] as char == get_block_hash(get_block_number()).chars().last().unwrap();}"
}
```

* `get_brc20_tick(get_ord_id(), 0) == \\"abcd\\"`: this requires that the first inscription within the Compos inscription has a ticker of `abcd`.
* `get_brc20_amt(get_ord_id(), 0) <=1000`: this requires that the amount of the first inscription within the Compos inscription is less than or equal to 1000.
* `para[0].as_bytes()[0] as char == get_block_hash(get_block_number()).chars().last().unwrap()`: this requires that the parameter passed to the OCF function during minting matches the last character of the block hash.

It only requires a single line of code.
