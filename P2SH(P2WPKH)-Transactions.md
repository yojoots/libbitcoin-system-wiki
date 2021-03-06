## Sending to a P2SH(P2WPKH) Output
Sending a transaction to a Pay-to-Witness-Public-Key-Hash (P2WPKH) address wrapped in a Pay-to-Script-Hash address requires the construction of the following output script:

| Transaction Element | Script                                                                  |
| --------------------|-------------------------------------------------------------------------|
| Output Script       | `HASH160` `[20-byte hash160(P2WPKH(public key hash))]` `EQUAL`          |

The construction of a P2SH(P2WPKH) output mirrors that of a Pay-to-Script-Hash output. The embedded script of the P2SH output shown above is the P2WPKH script.

```c++
// P2SH(P2WPKH) output.
// P2SH embedded script = P2WPKH(public key hash)
//    0 [20-byte public key hash]
short_hash keyhash_dest = bitcoin_short_hash(pubkey_witness_aware);
operation::list p2wpkh_operations;
p2wpkh_operations.push_back(operation(opcode::push_size_0));
p2wpkh_operations.push_back(operation(to_chunk(keyhash_dest)));
script p2wpkh_embedded_script(p2wpkh_operations);

// P2SH output script.
// hash160 [20-byte hash160(embedded script)] equal
short_hash embedded_script_hash = bitcoin_short_hash(
    p2wpkh_embedded_script.to_data(false));
script output_script = script::to_pay_script_hash_pattern(embedded_script_hash);

// Build output.
std::string btc_amount = "1.298";
uint64_t output_amount;
decode_base10(output_amount, btc_amount, btc_decimal_places);
output p2sh_p2wpkh_output(output_amount, output_script);
```
If the spending of the previous transaction output(s) do not require the construction of witnesses, the rest of the transaction is built and signed according to the documentation sections [building transactions](https://github.com/libbitcoin/libbitcoin/wiki/Building-Transactions) and [sighash](https://github.com/libbitcoin/libbitcoin/wiki/Sighash-and-TX-Signing).

The complete P2SH(P2WPKH) example script can be found [here](https://github.com/libbitcoin/libbitcoin/wiki/Examples-from-Pay-to-Witness-Transactions).

## Spending a P2SH(P2WPKH) Output

Spending a P2SH(P2WPKH) output requires constructing the transaction according to the following scheme.

| Transaction Element | Script                                                                  |
| --------------------|-------------------------------------------------------------------------|
| Output Script       | `According to destination address`                                      |
| Input Script        | `[zero <20-byte publicKeyHash>]`                                        |
| Script Code         | `DUP` `HASH160` `[20-byte hash160(PublicKey)]` `EQUALVERIFY` `CHECKSIG` |
| Witness             | `[Signature]` `[PublicKey]`                                             |

Compared to spending a native P2WPKH output, the input script is not left empty in a P2SH(P2WPKH) transaction, but is instead populated with a single data push representing the serialised P2SH embedded script (specifically, a P2WPKH script).

We construct the input object for our P2SH(P2WPKH) spending example.

```c++
// Omitted: Construction of output according to destination address
```

```c++
// P2SH(P2WPKH) input.
// Previous TX hash.
std::string prev_tx =
    "8231a9027eca6f2bd7bdf712cd2368f0b6e8dd6005b6b348078938042178ffed";
hash_digest prev_tx_hash;
decode_hash(prev_tx_hash, prev_tx);
// Previous UXTO index.
uint32_t index = 0;
output_point uxto_to_spend(prev_tx_hash, index);
// Build P2SH(P2WPKH) input object.
input p2sh_p2wpkh_input;
p2sh_p2wpkh_input.set_previous_output(uxto_to_spend);
p2sh_p2wpkh_input.set_sequence(max_input_sequence);

// Build transaction.
transaction tx;
tx.set_version(1u);
tx.inputs().push_back(p2sh_p2wpkh_input);
tx.outputs().push_back(p2pkh_output);
```

### Signing a Transaction with a P2SH(P2WPKH) Input
[BIP143](https://github.com/bitcoin/bips/blob/master/bip-0143.mediawiki) describes a witness-specific sighash generation algorithm for signatures evaluated by `CHECKSIG`, `CHECKSIGVERIFY`, `CHECKMULTISIG`, `CHECKMULTISIGVERIFY`.  

In particular, a script code and the previous input amount are required for the signature algorithm. The script code for spending a P2WPKH is simply a pay-to-public-key-hash script of the destination address.

```c++
// Create signature for witness.

// Script code.
script script_code = script::to_pay_key_hash_pattern(
      bitcoin_short_hash(pubkey_witness_aware));

// Previous input amount.
uint8_t input_index(0u);
std::string btc_amount_in = "1.298";
uint64_t input_amount;
decode_base10(input_amount, btc_amount_in, btc_decimal_places);

// Pass script_version::zero & prev input amount.
endorsement sig;
script::create_endorsement(sig, my_secret_witness_aware, script_code, tx,
    input_index, sighash_algorithm::all, script_version::zero, input_amount);
```
The `script::create_endorsement` method will generate a sighash according to the witness program version parameter. For inputs requiring a witness of the current version, this argument will be set to version zero in order for the witness-specific sighash algorithm to be applied.

### P2SH(P2WPKH) Input Script
The required input script for spending the P2SH(P2WPKH) output is the embedded script. The input script does not include any signatures, as these will be included in the witness.

The embedded script is a single data push of the P2WPKH script.

```c++
// Input script.
// embedded script = P2WPKH script
short_hash keyhash_dest = bitcoin_short_hash(pubkey_witness_aware);
operation::list p2wpkh_operations;
p2wpkh_operations.push_back(operation(opcode::push_size_0));
p2wpkh_operations.push_back(operation(to_chunk(keyhash_dest)));
script p2wpkh_embedded_script(p2wpkh_operations);

// Wrap (P2SH) embedded script in single single data push.
data_chunk p2sh_embedded_script_chunk = to_chunk(p2wpkh_embedded_script.to_data(true));
script p2sh_embedded_script_wrapper(p2sh_embedded_script_chunk, false);
tx.inputs()[0].set_script(p2sh_embedded_script_wrapper);
```

### P2SH(P2WPKH) Witness

The witness of a P2SH(P2WPKH) input is identical to that of a native P2WPKH input.  

```c++
// Build witness.
// 02 [signature] [public key]
data_stack witness_stack;
witness_stack.push_back(sig);
witness_stack.push_back(to_chunk(pubkey_witness_aware));
witness p2wpkh_witness(witness_stack);
tx.inputs()[0].set_witness(p2wpkh_witness);
```
Note that the witness class is constructed from a data stack, which in turn is an alias for the standard vector class storing data chunk elements. The witness object produces a serialised format which prepends a single-byte length prefix to each data chunk in its stack.

The serialised encoding of the witness may appear similar to Bitcoin scripts, but it differs in that it only consists of serialised data pushes with the aforementioned length prefixes.

This can be observed in the serialised witness from our example:

```c++
// Number of following witness elements for the first input.
02
// Length of 71-byte endorsement.
47
// Endorsement( DER signature + sighash marker)
304402207ecbb796a2bc706d90e2ed7efb58f59822bdc4c253b91f6eecd26ca5df1a6bb60220700b737f3c49b2f21bb228fadeab786e2ac78fd87890ede3f5d299e81880d96301
// Length of 33-byte public key
21
// Even public key
026ccfb8061f235cc110697c0bfb3afb99d82c886672f6b9b5393b25a434c0cbf3
```

### Serialised P2SH(P2WPKH) Transaction

Finally, we can express our P2SH(P2WPKH) spending transaction in the following serialised form:

```C++
// Serialize transaction.
std::cout << encode_base16(tx.to_data(true,true)) << std::endl;
```
```C++
01000000000101edff78210438890748b3b60560dde8b6f06823cd12f7bdd72b6fca7e02a9318200000000171600149a19a31c2fda7d0c30215ec954a20a542aa84ad3ffffffff016003b807000000001976a914bbef244bcad13cffb68b5cef3017c7423675552288ac0247304402207ecbb796a2bc706d90e2ed7efb58f59822bdc4c253b91f6eecd26ca5df1a6bb60220700b737f3c49b2f21bb228fadeab786e2ac78fd87890ede3f5d299e81880d9630121026ccfb8061f235cc110697c0bfb3afb99d82c886672f6b9b5393b25a434c0cbf300000000
```
Parsing the serialised form with BX gives us an overview of our constructed P2SH(P2WPKH) transaction.

```
BX tx-decode -f json 01000000000101edff78210438890748b3b60560dde8b6f06823cd12f7bdd72b6fca7e02a9318200000000171600149a19a31c2fda7d0c30215ec954a20a542aa84ad3ffffffff016003b807000000001976a914bbef244bcad13cffb68b5cef3017c7423675552288ac0247304402207ecbb796a2bc706d90e2ed7efb58f59822bdc4c253b91f6eecd26ca5df1a6bb60220700b737f3c49b2f21bb228fadeab786e2ac78fd87890ede3f5d299e81880d9630121026ccfb8061f235cc110697c0bfb3afb99d82c886672f6b9b5393b25a434c0cbf300000000
```
```json
{
    "transaction": {
        "hash": "e85f4cbe53a60ba027ba565653915499d9b6a7e824e260f23cd69bfab1992624",
        "inputs": [
            {
                "address_hash": "dcdc2f89b96c420751e3750da7d5073a81b16946",
                "previous_output": {
                    "hash": "8231a9027eca6f2bd7bdf712cd2368f0b6e8dd6005b6b348078938042178ffed",
                    "index": "0"
                },
                "script": "[00149a19a31c2fda7d0c30215ec954a20a542aa84ad3]",
                "sequence": "4294967295",
                "witness": "[304402207ecbb796a2bc706d90e2ed7efb58f59822bdc4c253b91f6eecd26ca5df1a6bb60220700b737f3c49b2f21bb228fadeab786e2ac78fd87890ede3f5d299e81880d96301] [026ccfb8061f235cc110697c0bfb3afb99d82c886672f6b9b5393b25a434c0cbf3]"
            }
        ],
        "lock_time": "0",
        "outputs": [
            {
                "address_hash": "bbef244bcad13cffb68b5cef3017c74236755522",
                "script": "dup hash160 [bbef244bcad13cffb68b5cef3017c74236755522] equalverify checksig",
                "value": "129500000"
            }
        ],
        "version": "1"
    }
}
```

You can find the complete P2SH(P2WPKH) example script [here](https://github.com/libbitcoin/libbitcoin/wiki/Examples-from-Pay-to-Witness-Transactions).