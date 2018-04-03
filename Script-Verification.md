This section describes the verification of input and output scripts with the relevant off-stack arguments (witnesses, lock-time, unspent outputs etc). Script verification does not verify the chain state information provided to the parsing the script. Script verification assesses whether input & output scripts evaluate to true on the script stack for a given a set of consensus rules.

![script::verify](https://ipfs.io/ipfs/QmeE3FaoJZa75qh47TsdGD6nCEr5EvWraNG32E1jKo3kVj)

In Libbitcoin, the [`script::verify()`](https://github.com/libbitcoin/libbitcoin/blob/master/include/bitcoin/bitcoin/chain/script.hpp#L212-L218) function parses the input and output scripts through the script interpreter, in order to evaluate if the entire script evaluates to true.

The following example demonstrates the spending of a P2PKH output. We construct both P2PKH output and input scripts and then check what the two scripts evaluate to.

```c++
// Omitted for brevity:
// Construction of p2pkh_transaction object used in example below.
```
```c++
// Previous output script / Previous output amount.
//---------------------------------------------------------------------------

// Previous output script: P2PKH.
script p2pkh_output_script = script::to_pay_key_hash_pattern(
      bitcoin_short_hash(pubkey0));

// Previous output amount.
std::string prev_btc_amount = "1.0";
uint64_t prev_output_amount;
decode_base10(prev_output_amount, prev_btc_amount, btc_decimal_places);


// Input script.
//---------------------------------------------------------------------------

// Signature.
endorsement sig_0;
uint8_t input0_index(0u);
script::create_endorsement(sig_0, my_secret0, p2pkh_output_script,
    p2pkh_transaction, input0_index, sighash_algorithm::all);

// Input script operations.
operation::list input_operations;
input_operations.push_back(operation(sig_0));
input_operations.push_back(operation(to_chunk(pubkey0)));
script p2pkh_input_script(input_operations);

// Add input script to transaction.
p2pkh_transaction.inputs()[0].set_script(p2pkh_input_script);


// Verify input script, output script.
//---------------------------------------------------------------------------

// With all fork rules, no witness.
code ec;
witness empty_witness;
ec = script::verify(p2pkh_transaction, 0u, rule_fork::all_rules,
    p2pkh_input_script, empty_witness, p2pkh_output_script,
    prev_output_amount);

// Prints success (Bitcoin:0)
std::cout << ec << std::endl;
```
You can find the complete example script [here](https://github.com/libbitcoin/libbitcoin/wiki/Examples:-Script-Verification).

Note that we have also passed in non-stack arguments into [`script::verify()`](https://github.com/libbitcoin/libbitcoin/blob/master/include/bitcoin/bitcoin/chain/script.hpp#L212-L218), such as the witness and the previous output amount, which is required for verifying BIP143 signatures. The [`rule_fork`](https://github.com/libbitcoin/libbitcoin/blob/master/include/bitcoin/bitcoin/machine/rule_fork.hpp#L27-L101) argument tells the script interpreter which Bitcoin soft [fork rules](https://github.com/libbitcoin/libbitcoin/wiki/Fork-Rules) to apply during the verification of the script.

The script verify method returns a printable [error code](https://github.com/libbitcoin/libbitcoin/blob/master/include/bitcoin/bitcoin/error.hpp#L47-L244) object.
