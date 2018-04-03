Bitcoin soft fork rule support are signalled with a 32-bit sequence in the block version field, with each of the first 29 bits each representing support for a given BIP.  

This 32-bit representation can be found in the [`rule_fork`](https://github.com/libbitcoin/libbitcoin/blob/master/include/bitcoin/bitcoin/machine/rule_fork.hpp#L27-L101) enum object in Libbitcoin. Individual soft fork rules can be easily activated or deactivated by modifying the respective bit .

```c++
// Turn off BIP16 soft fork, by selectively deactivating the BIP16 fork bit.
uint32_t my_fork_rules = rule_fork::all_rules ^ rule_fork::bip16_rule;

// Turn off BIP141/143 soft fork(s).
uint32_t my_fork_rules = rule_fork::all_rules ^ rule_fork::bip141_rule
    ^ rule_fork::bip143_rule;
```
The ability selectively support specific soft forks gives Libbitcoin the greater flexibility to support various chains. The entire list of soft forks supported by Libbitcoin can be found [here](https://github.com/libbitcoin/libbitcoin/blob/master/include/bitcoin/bitcoin/machine/rule_fork.hpp#L27-L101).

## Example: BIP16 Soft Fork

We may also toggle the activation of specific fork rules to effectively illustrate the backwards compatibility of past soft forks, such as BIP16(pay-to-script-hash).

[BIP16](https://github.com/bitcoin/bips/blob/master/bip-0016.mediawiki) did not add any new script operators, but introduced a new stack evaluation rule: First, the redeem script data push in the input script would be verified, to ensure it hashed to the redeem script hash in the P2SH script. If this evaluated to true, the redeem script would then be evaluated again, but this time together with the unlocking script.

![BIP16](https://ipfs.io/ipfs/QmdEHcQAw4uTELoyRUXYf87Xbx7YaqaR12g3YXxPm7n1Xs)

We can demonstrate the BIP16 soft fork in Libbitcoin by constructing a P2SH(2-of-2 Multisig) script and passing it to the interpreter together with two different input scripts: One input script which contains only the redeem script, and another one, which also includes an unlocking script, as illustrated above.

```c++
// Omitted for brevity:
// Construction of p2sh_transaction object used in example below.
```
```c++
// Previous output script / Previous output amount.
//---------------------------------------------------------------------------

// Previous output script = P2SH(2-of-2 Multisig).

// 2-of-2 Multisig.
uint8_t signatures(2u);
point_list points;
points.push_back(pubkey0);
points.push_back(pubkey1);
script multisig_script = script::to_pay_multisig_pattern(signatures, points);

// P2SH(2-of-2 Multisig) script.
short_hash multisig_script_hash = bitcoin_short_hash(
    multisig_script.to_data(false));
script p2sh_multisig_script = script::to_pay_script_hash_pattern(
    multisig_script_hash);

// Previous output amount.
std::string prev_btc_amount = "1.0";
uint64_t prev_output_amount;
decode_base10(prev_output_amount, prev_btc_amount, btc_decimal_places);
```

We now construct two different input scripts for comparison. The first input script only contains the redeem script which hashes to the redeem script hash in the P2SH(2-of-2 Multisig) script.

The second input script also includes the unlocking script with the two required signatures.

```c++
// Input Scripts.
//---------------------------------------------------------------------------

// Create Endorsements.
endorsement sig0;
endorsement sig1;
uint8_t input0_index(0u);
script::create_endorsement(sig0, my_secret0, multisig_script,
    p2sh_transaction, input0_index, sighash_algorithm::all);
script::create_endorsement(sig1, my_secret1, multisig_script,
    p2sh_transaction, input0_index, sighash_algorithm::all);

// Create input script w/o signatures (no BIP16).
operation::list no_sig_input_operations;
no_sig_input_operations.push_back(operation(multisig_script.to_data(false)));
script no_sig_input_script(no_sig_input_operations);

// Create input script /w signatures (BIP16).
operation::list sig_input_operations;
sig_input_operations.push_back(operation(opcode::push_size_0));
sig_input_operations.push_back(operation(sig0));
sig_input_operations.push_back(operation(sig1));
sig_input_operations.push_back(operation(multisig_script.to_data(false)));
script sig_input_script(sig_input_operations);
```
We can now demonstrate that the our first script does indeed evaluate to true pre BIP16. You can easily check that it does not follow the BIP16 rules by activating BIP16 and running the script again.

```c++
// Script Verification w/o BIP16 activation.
//---------------------------------------------------------------------------

// Add input script to transaction.
p2sh_transaction.inputs()[0].set_script(no_sig_input_script);

// Turn off BIP16 soft fork.
uint32_t my_fork_rules = rule_fork::all_rules ^ rule_fork::bip16_rule;

// Verify w/o signatures.
code ec;
witness empty_witness;
ec = script::verify(p2sh_transaction, 0u, my_fork_rules, no_sig_input_script,
    empty_witness, p2sh_multisig_script, prev_output_amount);

// Prints success (Bitcoin:0)
std::cout << ec << std::endl;
```
We will now activate BIP16 in the following step. In order to conform to BIP16 rules, our input script must contain the 2-of-2 multisig unlocking script.

```c++
// Script Verification with BIP16 activation.
//---------------------------------------------------------------------------

// Add input script to transaction.
p2sh_transaction.inputs()[0].set_script(sig_input_script);

// BIP16 is active.
my_fork_rules = rule_fork::all_rules;

// Input script also works without BIP16 activation.
// my_fork_rules = rule_fork::all_rules ^ rule_fork::bip16_rule;

// Verify with signatures.
ec = script::verify(p2sh_transaction, 0u, my_fork_rules, sig_input_script,
    empty_witness, p2sh_multisig_script, prev_output_amount);

// Prints success (Bitcoin:0)
std::cout << ec << std::endl;
```
By deactivating BIP16 in the example above you can verify that the input script is backwards compatible.

You can find the complete example script of this section [here](https://github.com/libbitcoin/libbitcoin/wiki/Examples:-Fork-Rules).

## Example: BIP141/143 Soft fork

BIP141 introduced the witness as part of the transaction serialisation format, which contains signatures previously located in the input script. BIP143 updated the sighash serialisation format for witness signatures.

Let us consider a P2WPKH script, which is backwards compatible to previous consensus rules, meaning that it can spent by anyone when BIP141 is not activated.

![BIP141/143](https://ipfs.io/ipfs/QmTV3aG31kd3kTNWbbNSMV2z6atYKxijevgVFq85vJY5gA)

To demonstrate this in Libbitcoin, we will first construct the P2WPKH script, and then attempt to spend it with an empty input script.

```c++
// Omitted for brevity:
// Construction of p2wpkh_transaction object used in example below.
```
```c++
// Previous output script / Previous output amount.
//---------------------------------------------------------------------------

// Previous P2WPKH.
// 0 [20-byte hash160(public key)]
operation::list p2wpkh_operations;
p2wpkh_operations.push_back(operation(opcode::push_size_0));
p2wpkh_operations.push_back(
    operation(to_chunk(bitcoin_short_hash(pubkey_witness_aware))));

// Previous output amount.
uint8_t input_index(0u);
std::string prev_btc_amount = "1.0";
uint64_t prev_output_amount;
decode_base10(prev_output_amount, prev_btc_amount, btc_decimal_places);

```

With BIP141/143 deactivated, this output script will evaluate to true with an empty input script.

```c++
// Script Verification w/o BIP141/143 activation.
//---------------------------------------------------------------------------

uint32_t my_fork_rules = rule_fork::all_rules ^ rule_fork::bip141_rule
    ^ rule_fork::bip143_rule;

witness empty_witness;
script empty_input_script;
code ec;

ec = script::verify(p2wpkh_transaction, 0u, my_fork_rules, empty_input_script,
    empty_witness, p2wpkh_operations, prev_output_amount);

// Prints success (Bitcoin:0)
std::cout << ec << std::endl;
```

Set the fork rules to `all_rules` to verify that it is not valid with BIP141/143 activated. With BIP141/143 activated, we need to construct a valid witness.

```c++
// Create Witness.
//---------------------------------------------------------------------------

// Create signature & witness.
// Script code.
script p2wpkh_script_code = script::to_pay_key_hash_pattern(
    bitcoin_short_hash(pubkey_witness_aware));

// Pass script_version::zero & prev input amount
endorsement sig0;
script::create_endorsement(sig0, my_secret_witness_aware, p2wpkh_script_code,
    p2wpkh_transaction, input_index, sighash_algorithm::all,
    script_version::zero, prev_output_amount);

// Create witness.
// 02 [signature] [public key]
data_stack witness_stack;
witness_stack.push_back(sig0);
witness_stack.push_back(to_chunk(pubkey_witness_aware));
witness p2wpkh_witness(witness_stack);
```

The witness is added to transaction and passed to `script::verify()`. We leave the input script empty as the signatures are included in the witness.

```c++
// Script Verification with BIP141/143 activation.
//---------------------------------------------------------------------------

my_fork_rules = rule_fork::all_rules;
// Without bip141: error code 77, unexpected witness.
// Without bip143: error code 65, stack false...
//    (BIP143 signature serialisation not activated)

// Add witness to transaction.
p2wpkh_transaction.inputs()[0].set_witness(p2wpkh_witness);

ec = script::verify(p2wpkh_transaction, 0u, my_fork_rules, empty_input_script,
    p2wpkh_witness, p2wpkh_operations, prev_output_amount);

// Prints success (Bitcoin:0)
std::cout << ec << std::endl;
```
Note that the witness transaction above is not valid when BIP141/143 are deactivated. In Libbitcoin, you will have to replace the witness object with an empty one. Over-the-wire however, the witness data would not be included in messages to nodes who have not activated BIP141/143, so that this transaction would still be backwards compatible nonetheless.

You can find the complete example script of this section [here](https://github.com/libbitcoin/libbitcoin/wiki/Examples:-Fork-Rules).
