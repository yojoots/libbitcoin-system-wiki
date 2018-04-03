All examples from the fork rules documentation chapter are shown here in full.

**BIP16**
* example_p2sh();

**BIP141/143**
* example_p2wpkh();

```c++
#include <bitcoin/bitcoin.hpp>
#include <string.h>
#include <iostream>

using namespace bc;
using namespace wallet;
using namespace chain;
using namespace machine;

// "Normal" wallets.
auto my_secret0 = base16_literal(
    "b7423c94ab99d3295c1af7e7bbea47c75d298f7190ca2077b53bae61299b70a5");
ec_private my_private0(my_secret0, ec_private::testnet, true);
ec_compressed pubkey0 = my_private0.to_public().point();
payment_address my_address0 = my_private0.to_payment_address();

auto my_secret1 = base16_literal(
    "d977e2ce0f744dc3432cde9813a99360a3f79f7c8035ef82310d54c57332b2cc");
ec_private my_private1(my_secret1, ec_private::testnet, true);
ec_compressed pubkey1 = my_private1.to_public().point();

// "Witness Aware" wallets.
auto my_secret_witness_aware = base16_literal(
    "0a44957babaa5fd46c0d921b236c50b1369519c7032df7906a18a31bb905cfdf");
ec_private my_private_witness_aware(my_secret_witness_aware,
    ec_private::testnet, true);
ec_compressed pubkey_witness_aware = my_private_witness_aware
    .to_public().point();


transaction create_example_transaction() {

  // Function creates tx object as a tx template for all subequent examples.
  //---------------------------------------------------------------------------

  // Destination output, a p2pkh script for example.
  std::string btc_amount = "0.998";
  uint64_t output_amount;
  decode_base10(output_amount, btc_amount, btc_decimal_places);
  script p2pkh_script = script::to_pay_key_hash_pattern(
      bitcoin_short_hash(pubkey1));
  output p2pkh_output(output_amount, p2pkh_script);

  // Build example input.
  input example_input;
  std::string prev_tx =
      "44101b50393d01de1e113b17eb07e8a09fbf6334e2012575bc97da227958a7a5";
  hash_digest prev_tx_hash;
  decode_hash(prev_tx_hash,prev_tx);
  uint32_t index = 0;
  output_point uxto_to_spend(prev_tx_hash, index);
  example_input.set_previous_output(uxto_to_spend);
  example_input.set_sequence(max_input_sequence);

  // Build Transaction
  transaction tx;
  tx.set_version(1u);
  tx.inputs().push_back(example_input);
  tx.outputs().push_back(p2pkh_output);
  tx.set_locktime(0u);

  return tx;

}


void example_p2sh(const transaction& example_transaction) {

  // Create local example_transaction copy.
  transaction p2sh_transaction = example_transaction;


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


  // Script Verification w/o BIP16 activation.
  //---------------------------------------------------------------------------

  // Add input script to transaction.
  p2sh_transaction.inputs()[0].set_script(no_sig_input_script);

  // Turn off BIP16 soft fork.
  uint32_t my_fork_rules = rule_fork::all_rules ^ rule_fork::bip16_rule;

  // Verify w/o signatures.
  code ec;
  witness empty_witness;
  ec = script::verify(p2sh_transaction, 0u,
          my_fork_rules, no_sig_input_script,
          empty_witness, p2sh_multisig_script,
          prev_output_amount);

  // Prints success (Bitcoin:0)
  std::cout << ec << std::endl;


  // Script Verification with BIP16 activation.
  //---------------------------------------------------------------------------

  // Add input script to transaction.
  p2sh_transaction.inputs()[0].set_script(sig_input_script);

  // BIP16 is active.
  my_fork_rules = rule_fork::all_rules;

  // Input script also works without BIP16 activation.
  //my_fork_rules = rule_fork::all_rules ^ rule_fork::bip16_rule;

  // Verify w/o signatures.
  ec = script::verify(p2sh_transaction, 0u,
          my_fork_rules, sig_input_script,
          empty_witness, p2sh_multisig_script,
          prev_output_amount);

  // Prints success (Bitcoin:0)
  std::cout << ec << std::endl;

}


void example_p2wpkh(const transaction& example_transaction) {

  // Create local example_transaction copy.
  transaction p2wpkh_transaction = example_transaction;


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


  // Script Verification w/o BIP141/143 activation.
  //---------------------------------------------------------------------------

  uint32_t my_fork_rules = rule_fork::all_rules ^ rule_fork::bip141_rule
      ^ rule_fork::bip143_rule;

  witness empty_witness;
  script empty_input_script;
  code ec;

  ec = script::verify(p2wpkh_transaction, 0u,
          my_fork_rules, empty_input_script,
          empty_witness, p2wpkh_operations,
          prev_output_amount);

  // Prints success (Bitcoin:0)
  std::cout << ec << std::endl;


  // Create Witness.
  //---------------------------------------------------------------------------

  // Create signature & witness.
  // Script code.
  script p2wpkh_script_code = script::to_pay_key_hash_pattern(
      bitcoin_short_hash(pubkey_witness_aware));

  // Pass script_version::zero & prev input amount.
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


  // Script Verification with BIP141/143 activation.
  //---------------------------------------------------------------------------

  my_fork_rules = rule_fork::all_rules;
  // Without bip141: error code 77, unexpected witness.
  // Without bip143: error code 65, stack false...
  //    (BIP143 signature serialisation not activated).

  // Add witness to transaction.
  p2wpkh_transaction.inputs()[0].set_witness(p2wpkh_witness);

  ec = script::verify(p2wpkh_transaction, 0u,
          my_fork_rules, empty_input_script,
          p2wpkh_witness, p2wpkh_operations,
          prev_output_amount);

  // Prints success (Bitcoin:0)
  std::cout << ec << std::endl;

}

int main() {

  transaction tx = create_example_transaction();

  example_p2sh(tx);

  example_p2wpkh(tx);

  return 0;

}
```
