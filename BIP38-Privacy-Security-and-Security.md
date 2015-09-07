In **multiply mode** BIP-38 defines three new artifacts:

* `intermediate code`
* `confirmation code`
* `encrypted private key`

It also makes use of existing Bitcoin artifacts:

* `private key`
* `public key`
* `payment address`

The scenario for which these artifacts are defined envisions two actors, an `owner` and a `printer`.

 1. The owner creates an `intermediate code` using a secret passphrase (on a trusted platform).
 2. The owner provides the `intermediate code` to the printer.
 3. The printer generates an `encrypted private key` from the `intermediate code`.
 5. The printer provides the `encrypted private key` and a `confirmation code` to the owner.
 6. The printer has access to the `public key` and `payment address` and may provide these to the owner as well.
 7. The printer has no ability to obtain the corresponding `private key` without the original passphrase.

### Privacy
From a privacy standpoint the only material issue is that the owner has given the printer knowledge of the `public key` of an owner `private key`. This means that any payment to a `payment address` derived from that `public key` can be associated with the owner's person (i.e. tainted). The printer is therefore trusted to not disclose this association.

### Security
The owner must validate information returned from the printer. Otherwise there are several ways the printer can steal (i.e. intentionally) or lose (i.e. through negligence) the owner's money. Validation must be done on a trusted platform, such as the one first used to generate the `intermediate code`. Otherwise the `private key` of the `encrypted private key` may have been compromised.

#### Theft of Money
The printer could just generate an `encrypted private key` without using the owner's `intermediate code`. In this case any money spent to the `public key` of the encrypted private key would be spendable by the printer and not by the owner. The owner can prevent this by validating the `confirmation code` against the originating `intermediate code`.

The printer could return a `payment address` (or `public key`) that is unrelated to the `intermediate code`. If the `intermediate code` is valid but does not represent the corresponding `payment address` any money sent to the `payment address` will similarly not be spendable by the `owner`. Therefore the validation step must accept the `payment address` as a parameter.

#### Denial of Money
The printer could generate a valid `confirmation code` using the owner's `intermediate code` and return an unrelated `encrypted private key`. If the owner validates the `confirmation code` against the `intermediate code` the owner will know that the printer cannot spend money sent to the related `payment address`. However this offers no assurance whatsoever that the owner can spend from the validated `payment address`.