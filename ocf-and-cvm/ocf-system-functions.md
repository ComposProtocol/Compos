# OCF System Functions

Compos Protocol, through its CVM, has innovatively developed a set of system functions specifically designed to facilitate access to the Bitcoin blockchain's data for developers. Developers can seamlessly invoke these functions within OCF.

We have outlined a strategic plan to implement system functions progressively, categorized into seven distinct types, aligning with our roadmap for gradual deployment:

* Global:
  * `get_block_number, get_tx_id, get_ord_id, get_ord_owner`
* Block related:
  * `get_block_hash, get_block_timestamp, get_block_merkleroot, get_nonce get_block_brc20a_len,`
    * `get_block_brc20a_len`: retrieve the total number of BRC-20A inscriptions issued by a specific address in a given block, considering both separate-outputs and same-sats scenarios.
  * `get_block_difficulty, get_block_size, get_block_total_input, get_block_total_output, get_block_reward_btc, get_block_fee_reward_btc, get_block_stripped_size`
* TX related:
  * `get_tx_block_number, get_tx_ord_len, txo_exist`
    * `get_tx_ord_len`: get the number of inscriptions within the transaction, noting that multiple bodies are possible for batch inscriptions.
    * `txo_exist`: used to verify the existence of a transaction output in the transaction that sends a specific amount of BTC value to a particular address.
  * `get_tx_input_btc, get_tx_output_btc, get_tx_fee_price, get_tx_hash, get_tx_virtual_size, get_tx_index, get_tx_value, get_tx_lock_time`
* Ordinals layer related:
  * `get_ord_number, get_ord_owner, get_ord_genesis_tx_id, get_ord_metadata, get_ord_metaprotocol, get_ord_content_body, get_ord_ref_by, ord_ref_byself`
    * `get_ord_content_body`: parse the body of this inscription as a string. This body refers to `content_type` with a tag of `1`.
    * `get_ord_ref_by`: retrieve the inscriptions that recursively reference this specific inscription.
    * `ord_ref_byself`: returns if a particular inscription has been referenced by its owner
  * `get_ord_by_field, get_ord_p, get_ord_genesis_block_number, get_ord_genesis_fee, get_ord_from_address, get_ord_location, get_ord_offset, get_ord_value, get_ord_content_type, get_ord_sat_ordinal, get_ord_sat_rarity, get_ord_satributes, get_ord_provenance`
* OCF layer related:
  * `get_ocf_params`: retrieve the parameters of a specific OCF inscription
* BRC-20 layer related:
  * `get_brc20_op, get_brc20_tick, get_brc20_max_supply, get_brc20_current_supply, get_brc20_amt`
* Address related:
  * `get_balance, get_brc20_balance, get_brc20_transferable_balance, get_brc20_available_balance`

In OCF `version`= 0.1, we have implemented the following system functions:

```
// Global system functions
// Global system functions do not have explicit input parameters, as there exists an implicit parameter, which is the location of the OCF inscription (encompassing the block it resides in, the transaction it's part of, its ordinals ID, and the sender of the transaction).
fn get_block_number() -> u64;
fn get_tx_id() -> String;
fn get_ord_id() -> String;
fn get_ord_owner() -> String;
fn get_block_hash(block_number: u64) -> String;
fn get_block_brc20a_len(block_number: u64, addr: &str) -> i64; // retrieve the number of BRC-20A inscriptions sent by a specific address in a given block
fn get_tx_block_number(tx_id: &str) -> u64;
fn get_ord_genesis_tx_id(ord_id: &str) -> String;
fn get_ord_ref_by(ord_id: &str) -> String; // retrieve the inscriptions that recursively reference this specific inscription
fn ord_ref_byself(ord_id: &str) -> bool; // returns if a particular inscription has been referenced by its own owner
fn get_ocf_params(ord_id: &str) -> Vec<String>; // retrieve the parameters of a specific OCF inscription
fn get_brc20_tick(ord_id: &str, comp_index: u32) -> String;
fn get_brc20_max_supply(ord_id: &str, comp_index: u32) -> f64;
fn get_brc20_current_supply(ord_id: &str, comp_index: u32) -> f64;
fn get_brc20_amt(ord_id: &str, comp_index: u32) -> f64;
fn get_brc20_balance(owner: &str, tick: &str) -> f64;
```
