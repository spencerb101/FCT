---
description: These data structures are composed by the Users.
---

# User elements

## Entry

An Entry is the element which carries user data. An Entry Reveal is essentially this data.

The External IDs are a part of the Entry which have byte sequence lengths that must be known by Factom. The first Entry in a Factom Chain uses the External IDs to define the Chain Name. Other Entries can use the External IDs as their application dictates.

To be valid, the External IDs are parsed and the end of the last element must match the defined length for the External IDs as defined in the header.

External IDs \(ExtID\) are intended to provide any sort of tagging information for Entries that applications may find useful. Keys to databases are likely to be a common use. External IDs are simply data to Factom, and are not used in the consensus algorithm after the first Entry.

External IDs and Content is not checked for validity, or sanitized, as it is only viewed as binary data.

| Data | Field Name | Description |
| :---: | :---: | :---: |
| **Header** |  |  |
| varInt\_F | Version | starts at 0.  Higher numbers are currently rejected. Can safely be coded using 1 byte for the first 127 versions. |
| 32 bytes | ChainID | This is the Chain which the author wants this Entry to go into. |
| 2 bytes | ExtIDs Size | Describes how many bytes required for the set of External IDs for this Entry.  Must be less than or equal to the Payload size.  Big endian. |
|  |  |  |
| **Payload** |  | This is the data between the end of the Header and the end of the Content. |
|  |  |  |
| **External IDs** |  | This section is only interpreted and enforced if the External ID Size is greater than zero. |
| 2 bytes | ExtID element 0 length | This is the number of the following bytes to be interpreted as an External ID element.  Cannot be 0 length. |
| variable | ExtID 0 | This is the data for the first External ID. |
| 2 bytes | ExtID X | Size of the X External ID |
| variable | ExtID X data | This is the Xth element.  The last byte of the last element must fall on the last byte specified ExtIDs Size in the header. |
|  |  |  |
| **Content** |  |  |
| variable | Entry Data | This is the unstructured part of the Entry.  It is all user specified data. |

Minimum empty Entry length: 35 bytes

Minimum empty first Entry with Chain Name of 1 byte: 38 bytes

Maximum Entry size: 10KiB + 35 bytes = 10275 bytes

Typical size recording the hash of a file with 200 letters of ExtID metadata: 1+32+2+2+200+32 = 269 bytes

example size of something similar to an Omni\(MSC\) transaction, assuming 500 bytes [per transaction](https://blockchain.info/address/1EXoDusjGwvnjZUyKkxZ4UHEf77z6A5S4P): 1+32+2+500 = 535 bytes

Example Entry with a Chain Name of 'test', spaces added for clarity: As first Entry: 00 954d5a49fd70d9b8bcdb35d252267829957f7ef7fa6c74f88419bdc5e82209f4 0006 0004 74657374 5061796c6f616448657265

As regular Entry without ExtID: 00 954d5a49fd70d9b8bcdb35d252267829957f7ef7fa6c74f88419bdc5e82209f4 0000 5061796c6f616448657265

As regular Entry with ExtID of 'Hello' in 'test' chain: 00 954d5a49fd70d9b8bcdb35d252267829957f7ef7fa6c74f88419bdc5e82209f4 0007 0005 48656c6c6f 5061796c6f616448657265

## Entry Hash

The Entry Hash is a 32 byte identifier unique to specific Entry data. It is referenced in the Entry Block body as well as in the Entry Commit. In a desire to maintain long term resistance to [second-preimage attacks](http://en.wikipedia.org/wiki/Preimage_attack) in SHA2, as well as preventing length extension attacks, SHA512 is included in the Entry Hash generation process. For a future attacker to come up with a dishonest piece of data, they would need contend with many extra hashing rounds with a combined SHA512 and SHA256 in series. This operation is in contrast to the SHA256d, which does one hash over the SHA256 of the protected data. To brute force a SHA256d collision, modifying data at the end can only require 128 rounds. Prepending the SHA512 requires finding collision to iterate over the entire Entry more than once per attempt.

Straight SHA256 is used for Merkle roots due to anticipated CPU hardware acceleration, as well as being double-checkable by the serial hash. Entries \(unlike blocks\) do not have two independent ways of hashing protecting data, so this is why the hashing is more complex.

To calculate the Entry Hash, first the Entry is serialized and passed into a SHA512 function. The 64 bytes output from the SHA512 function is prepended to the serialized Entry. The Entry+prependage are then fed through a SHA256 function, and the output of that is the Entry Hash.

Using the above Entry as an example.

00954d5a49fd70d9b8bcdb35d252267829957f7ef7fa6c74f88419bdc5e82209f400005061796c6f616448657265 is passed into SHA512 and that gives: 0ba3c58955c69b02aa675d8ff15b505a48335fdc9a06354ba55e4149f77b69835c8c2b7002ca3b09202846d03626bada6b408fa1374f22dc396c64d9a3980ed3

The Entry is appended to the SHA512 result to make 0ba3c58955c69b02aa675d8ff15b505a48335fdc9a06354ba55e4149f77b69835c8c2b7002ca3b09202846d03626bada6b408fa1374f22dc396c64d9a3980ed300954d5a49fd70d9b8bcdb35d252267829957f7ef7fa6c74f88419bdc5e82209f400005061796c6f616448657265 which is then SHA256 hashed to make an Entry Hash of: 72177d733dcd0492066b79c5f3e417aef7f22909674f7dc351ca13b04742bb91

## Entry Commit

An Entry Commit is a payment for a specific Entry. It deducts a balance held by a specific public key in the amount specified. They are collected into the Entry Credit chain as proof that a balance should be decremented.

| data | Field Name | Description |
| :---: | :---: | :--- |
| **Header** |  |  |
| varInt\_F | Version | starts at 0.  Higher numbers are currently rejected.  Can safely be coded using 1 byte for the first 127 versions. |
| 6 bytes | milliTimestamp | This is a timestamp that is user defined.  It is a unique value per payment. This is the number of milliseconds since 1970 epoch. |
| 32 bytes | Entry Hash | This is the SHA512+256 descriptor of the Entry to be paid for. |
| 1 byte | Number of Entry Credits | This is the number of Entry Credits which will be deducted from the balance of the public key. Any values above 10 are invalid. |
| 32 bytes | Pubkey | This is the Entry Credit public key which will have the balance reduced. It is the ed25519 A value. |
| 64 bytes | Signature | This is a signature of this Entry Commit by the pubkey.  Parts ordered R then S. Signature covers from Version through 'Number of Entry Credits' |

The Entry Commit is only valid for 12 hours before and after the milliTimestamp. Since Entry Credits are balance based, replay attacks can reduce balances. Also a user can pay for the same Entry twice, and have two copies in Factom. Since a P2P network is used, the payments would need to be differentiated. The payments would be differentiated by public key and the time specified. This puts a limit of 1000 per second on any individual Entry Credit public key per duplicate Entry. The milliTimestamp also helps the network protect itself. Adding the time element allows peers to automatically reject payments beyond 12 hours plus or minus. This means they must check for duplicates only over a rolling one day period.

The number of Entry Credits is based on the Payload size. Cost is 1 EC per partial KiB. Empty Entries cost 1 EC.

The Entry Commits \(and Chain Commits\) have two hashes associated with them. Each hash is a single SHA256 of the data. One is the hash of the entire Commit from the Version through the Signature. The other is the hash of the ledger fields \(Version through Number of Entry Credits\), which is the TXID. The TXID is immune from transaction malleability, since it does not cover the signature. Doublespends share the same ledger hash.

## Chain Commit

A Chain Commit is a simultaneous payment for a specific Entry and a payment to allow a new Chain to be created. It deducts a balance held by a specific EC public key in the amount specified. They are collected into the Entry Credit chain as proof that a balance should be decremented.

| Data | Field Name | Description |
| :---: | :---: | :--- |
| varInt\_F | Version | starts at 0.  Higher numbers are currently rejected. Can safely be coded using 1 byte for the first 127 versions. |
| 6 bytes | milliTimestamp | This is a timestamp that is user defined.  It is a unique value per payment. This is the number of milliseconds since 1970 epoch. |
| 32 bytes | ChainID Hash | This is a double hash \(SHA256d\) of the ChainID which the Entry is in. |
| 32 bytes | Commit Weld | SHA256\(SHA256\(Entry Hash `|` ChainID\)\) This is the double hash \(SHA256d\) of the Entry Hash concatenated with the ChainID. |
| 32 bytes | Entry Hash | This is the SHA512+256 descriptor of the Entry to be the first in the Chain. |
| 1 byte | Number of Entry Credits | This is the number of Entry Credits which will be deducted from the balance of the public key. Any values above 20 or below 11 are invalid. |
| 32 bytes | Pubkey | This is the Entry Credit public key which will have the balance reduced. |
| 64 bytes | Signature | This is a signature of this Chain Commit by the pubkey.  Parts ordered R then S. Signature covers from Version through 'Number of Entry Credits' |

The Federated server will keep track of the Chain Commits based on ChainID Hash. The Federated servers keep track of the Chain Commits they receive. When the first Entry is received, it will reveal the ChainID. If the ChainID was a secret, then it now can be compared against all the possible Chain Commits claiming to pay for Entries of a certain ChainID. Once the ChainID is revealed, the ChainID hash and the 'Entry Hash + ChainID' fields can be compared to see if they match and form valid hashes. If they do not match, that Chain Commit is invalid. If they do match, then the first one to be acknowledged gets accepted as the first Entry. They maintain exclusivity for 1 hour for each ChainID hash after an acknowledgement. The commit itself must be within 12 hours +/- of the milliTimestamp.

A prudent user will not broadcast their first Entry until the Federated server acknowledges the Chain Commit. If they do not wait, a malicious peer on the P2P network can put their Entry as the first one in that Chain, or stop the chain from being created for 1 hour. This is the denial of chain attack.

Chain Commits cost 10 Entry Credits to create the Chain, plus the fee per KiB of the Entry itself.

The TXID of a Chain Commit shares the same form as a Entry Commit.

## Factoid Transaction

Factoid transactions are similar to Bitcoin transactions, but incorporate some [lessons learned](http://www.reddit.com/r/Bitcoin/comments/2jw5pm/im_gavin_andresen_chief_scientist_at_the_bitcoin/clfp3xj) from Bitcoin.

* They are closer to P2SH style addresses, where the value is sent to the hash of a redeem condition, instead of sent to the redeem condition itself. To redeem value, a datastructure containing public keys, etc should be revealed. This is referred to as the **Redeem Condition Datastructure \(RCD\)**
* Factoids use Ed25519 with Schnorr signatures.  They have [many benefits](https://ripple.com/uncategorized/curves-with-a-twist/0) over the ECDSA signatures used in Bitcoin.
* The signatures are enforced to be [canonical](https://github.com/FactomProject/ed25519/blob/master/ed25519.go#L143).  This will limit malleability by attackers without the private key.
* Scripts are not used.  They may be added later, but are not implemented in the first version. Instead of scripts, there are a limited number of valid RCDs which are interpreted.  This is similar to how Bitcoin only has a handful of standard transactions.  Non-standard transactions are not relayed on the Factom P2P network. In Factom, non-standard transactions are undefined.  Adding new transaction types will cause a hard fork of the Factom network.

Factoids are balanced based and have all the value combined to a single amount. The address is a hash of a Redeem Condition Datastructure \(RCD\). The Factoid transaction is denominated in Factoshis, which is 10^-8 Factoids.

| data | Field Name | Description |
| :---: | :---: | :--- |
| **Header** |  |  |
| varInt\_F | Version | Version of the transaction type.  Versions other than 2 are not relayed. Can safely be coded using 1 byte for the first 127 versions. |
| 6 bytes | milliTimestamp | Same rules as the Entry Commits. This is a unique value per transaction.  This field is the number of milliseconds since 1970 epoch.  The Factoid transaction is valid for 24 hours before and after this time. |
| 1 byte | Input Count | This is how many Factoid addresses are being spent from in this transaction. |
| 1 byte | Factoid Output Count | This is how many Factoid addresses are being spent to in this transaction. |
| 1 byte | Entry Credit Purchase Count | This is how many Entry Credit addresses are being spent to in this transaction. |
|  |  |  |
| **Inputs** |  |  |
| varInt\_F | Value | \(Input 0\) This is how much the Factoshi balance of Input 0 will be decreased by. |
| 32 bytes | Factoid Address | \(Input 0\) This is an RCD hash which previously had value assigned to it. |
| varInt\_F | Value | \(Input X\) This is how much the Factoshi balance of Input X will be decreased by. |
| 32 bytes | Factoid Address | \(Input X\) This is an RCD hash which previously had value assigned to it. |
|  |  |  |
| **Factoid Outputs** |  |  |
| varInt\_F | Value | \(Output 0\) This is how much the Output 0 Factoshi balance will be increased by. |
| 32 bytes | Factoid Address | \(Output 0\) This is an RCD hash which will have its balance increased. |
| varInt\_F | Value | \(Output X\) This is how much the Output X Factoshi balance will be increased by. |
| 32 bytes | Factoid Address | \(Output X\) This is an RCD hash which will have its balance increased. |
|  |  |  |
| **Entry Credit Purchase** |  |  |
| varInt\_F | Value | \(Purchase 0\) This many Factoshis worth of ECs will be credited to the Entry Credit public key 0. |
| 32 bytes | EC Pubkey | \(Purchase 0\) This is Entry Credit public key that will have its balance increased. |
| varInt\_F | Value | \(Purchase X\) This many Factoshis worth of ECs will be credited to the Entry Credit public key X. |
| 32 bytes | EC Pubkey | \(Purchase X\) This is Entry Credit public key that will have its balance increased. |
|  |  |  |
| **Redeem Condition Datastructure \(RCD\) Reveal / Signature Section** |  |  |
| variable | RCD 0 | First RCD.  It hashes to input 0. The length is dependent on the RCD type, which is in the first byte. There are as many RCDs as there are inputs. |
| variable | Signature 0 | This is the data needed to satisfy RCD 0. It is a signature for type 1, but might be other types of data for later RCD types.  Its length is dependent on the RCD type. |
| variable | RCD X | Xth RCD.  It hashes to input X. |
| variable | Signature X | This is the data needed to satisfy RCD X. |

The transaction is protected against replay attacks because the servers do not allow duplicate transactions with the same timestamp if they share the same inputs and outputs. Changing any of those fields would also break the signature.

The signatures cover the Header, Inputs, Outputs, and Purchases. The RCD is protected from tampering because the signed inputs specify only one possible RCD.

The Factoids have two hashes associated with them. Both are a single SHA256 of the data. One is the hash of the entire transaction from the Header through the Signatures. The other is the hash of the ledger fields \(Header through Entry Credit Purchase\), which is the TXID. The TXID is immune from transaction malleability, since it does not cover the signature \(or subkeys of a multisig\). Doublespends share the same ledger hash.

#### **Redeem Condition Datastructure \(RCD\)**

This can be considered equivalent to a Bitcoin redeem script behind a P2SH transaction. The first version will only support single signature addresses. Type 1 is defined here. The RCD is hashed with SHA256 twice, \(SHA256d\), to prevent potential length extension attacks. Multisignature RCDs are planned for release soon.

**RCD Type 1**:

| data | Field Name | Description |
| :---: | :---: | :--- |
| varInt\_F | Type | The RCD type.  This specifies how the datastructure should be interpreted.  Type 1 is the only currently valid type. Can safely be coded using 1 byte for the first 127 types. |
| 32 bytes | Pubkey 0 | The raw ed25519 public key. |

Note: For the token sale, a raw Ed25519 pubkey is included in an OP\_RETURN output along with the payment to the sale multisig address. The the genesis block will contain a transaction which outputs to many 1 of 1 addresses. There will be an output for each of the Bitcoin payments' specified pubkeys. The addresses will be derived from the exposed pubkeys. Payments with the same pubkey will have their balances combined.

Some later RCD types will be added. Output types supporting [atomic cross](https://en.bitcoin.it/wiki/Atomic_cross-chain_trading) chain swaps and [time locking](https://github.com/bitcoin/bips/blob/master/bip-0065.mediawiki) outputs are desirable. Output scripts are also useful and desirable, but can open security holes. They are not critical for the first release of Factom, so we will implement them later. This would give us the ability to make conditional outputs \(IF, AND, OR, etc\). Nesting is also desirable. This would give multisig within a multisig transaction. Implementing scripts will give all the intermediate RCD types, so possibly going directly to scripts can bypass a special atomic cross chain swap, etc.

Ed25519 allows for threshold multisig in a [single signature](http://crypto.stackexchange.com/questions/20581/does-ed25519-support-cryptographic-threshold-signatures), but that cryptography will have to come later. This does have the disadvantage against Bitcoin style, multiple individual key checking though. When a signature is made, this method does not show who in the group made the signature.

#### **Fees**

Fees are the difference between the outputs and the inputs. The fees are [sacrificed](https://blog.ethereum.org/2014/02/01/on-transaction-fees-and-the-fallacy-of-market-based-solutions/). They are defined by, but not reclaimed by the Federated servers. The minimum transaction fees are based on the current exchange rate of Factoids to Entry Credits. The outputs must be less than the inputs by at least the the fee amount at confirmation time. The minimum fees are the sum of 3 things that cause load on the system:

1. Transaction data size. -- Factoid transactions are charged the same amount as Entry Credits \(EC\).  The size fees are 1 EC per KiB with a maximum transaction size of 10 KiB.
2. Number of outputs created -- These are data points which potentially need to be tracked far into the future.  They are more expensive to handle, and require a larger sacrifice.  Outputs cost 10 EC per output. A purchase of Entry Credits also requires the 10 EC sized fee to be valid.
3. Number of signatures checked -- These cause expensive computation on all full nodes.  A fee of 1 EC equivalent must be paid for each signature included.

A minimal transaction buying Entry Credits or sending Factoids to one address from a single sig address would cost the equivalent of 12 Entry Credits.

### **Coinbase Factoid Transaction**

The coinbase transaction is how new Factoids come into the system to reward network participants. These are new Factoids created by the protocol. The outputs are determined by the Coinbase Descriptor which is included in the Admin block 1000 blocks prior \(approx 1 week\).

In M1 and M2, coinbase transactions were included in each factoid block. All but the genesis block coinbase tx had 0 inputs and 0 outputs. In M3, the coinbase tx will similarly be 0 inputs and 0 outputs except for coinbases included at 25 block intervals. A non-zero coinbase output will be on Factoid blocks following 1000 blocks after a Coinbase Descriptor in the Admin block.

| data | Field Name | Description |
| :---: | :---: | :--- |
| **Header** |  |  |
| varInt\_F | Version | Determined by Federated Servers, version 2 for now. |
| 6 bytes | milliTimestamp | The time is set as the Directory Block timestamp. |
| 1 byte | Input Count | Always zero. coinbase has no inputs. As such, it has no RCD reveals or signatures. |
| 1 byte | Factoid Output Count | This is how many Factoid addresses are being spent to in this transaction. It is coordinated among the Federated Servers. |
| 1 byte | Entry Credit Purchase Count | Always zero. Federated Servers do not need to buy entry credits in the coinbase. |
|  |  |  |
| **Factoid Outputs** |  |  |
| varInt\_F | Value | \(Output 0\) This is how much the Output 0 Factoshi balance will be increased by. |
| 32 bytes | Factoid Address | \(Output 0\) This is an RCD hash which will have its balance increased. |
| varInt\_F | Value | \(Output X\) This is how much the Output X Factoshi balance will be increased by. |
| 32 bytes | Factoid Address | \(Output X\) This is an RCD hash which will have its balance increased. |

### **Balance Increase**

This datastructure is a pointer to a valid Factoid transaction which purchases Entry Credits. It creates a trigger to increase the Entry Credit balance of a particular EC pubkey. It is derived deterministically from every Factoid output which credits EC keys.

| data | Field Name | Description |
| :--- | :--- | :--- |
| 32 bytes | EC Public Key | This is the public key which the Factoid transaction has credited. |
| 32 bytes | TXID | This is the transaction ID of the Factoid transaction crediting the above public key. |
| varInt\_F | Index | The index in the above Factoid transaction's Purchase field crediting the EC pubkey. |
| varInt\_F | NumEC | This is the number of Entry Credits granted to the EC public key based on the current exchange rate in effect. |

## Human Readable Addresses

Factoid and Entry Credit addresses are modeled after Bitcoin addresses. They have an identifiable prefix and a checksum to prevent typos. See [base58check](https://en.bitcoin.it/wiki/Base58Check_encoding) encoding. Instead of Bitcoin's 160 bits, they use 256 bits. They also use 2 bytes for the version byte instead of Bitcoin's 1 byte.

### **Factoid Address**

Factoids are sent to an RCD Hash. Inside the computer, the RCD hash is represented as a 32 byte number. The user sees Factoid addresses as a 52 character string starting with FA.

To convert a 32 byte RCD Hash to a Factoid address follow these steps:

1. Concatenate 0x5fb1 and the RCD Hash bytewise
   * `5fb10000000000000000000000000000000000000000000000000000000000000000` using zeros as a substitute RCD Hash
2. Take the SHA256d of the above data.  Append the first 4 bytes of this SHA256d to the end of the above value bytewise.
   * `5fb10000000000000000000000000000000000000000000000000000000000000000d48a8e32`
3. Convert the above value from base 256 to base 58.  Use standard Bitcoin base58 encoding to display the number.
   * `FA1y5ZGuHSLmf2TqNf6hVMkPiNGyQpQDTFJvDLRkKQaoPo4bmbgu`

Factoid addresses will range between `FA1y5ZGuHSLmf2TqNf6hVMkPiNGyQpQDTFJvDLRkKQaoPo4bmbgu` and `FA3upjWMKHmStAHR5ZgKVK4zVHPb8U74L2wzKaaSDQEonHajiLeq` representing all zeros and all f-characters \(hex\).

### **Entry Credit Address**

Entry Credits are redeemed to an Ed25519 raw public key. Inside the computer, the pubkey is represented as a 32 byte number. The user sees Entry Credit addresses as a 52 character string starting with EC.

To convert a 32 byte pubkey to an Entry Credit address follow these steps:

1. Concatenate 592a and the pubkey bytewise
   * `592a0000000000000000000000000000000000000000000000000000000000000000` using zeros as a substitute pubkey
2. Take the SHA256d of the above data.  Append the first 4 bytes of this SHA256d to the end of the above value bytewise.
   * `592a00000000000000000000000000000000000000000000000000000000000000003cf4595f`
3. Convert the above value from base 256 to base 58.  Use standard Bitcoin base58 encoding to display the number.
   * `EC1m9mouvUQeEidmqpUYpYtXg8fvTYi6GNHaKg8KMLbdMBrFfmUa`

Entry Credit addresses will range between `EC1m9mouvUQeEidmqpUYpYtXg8fvTYi6GNHaKg8KMLbdMBrFfmUa` and `EC3htx3MxKqKTrTMYj4ApWD8T3nYBCQw99veRvH1FLFdjgN6GuNK` representing all zeros and all f-characters \(hex\).

### **Private Keys**

Private keys for Factoids and Entry Credits follow a similar pattern. They start with Fs and Es, with the s standing for secret.

#### **Factoid Private Keys**

Single signature private keys are represented in human readable form using the same base58check as the public keys. The only difference is the prefix bytes. The Factoid private key prefix is `0x6478`.

Human readable Factoid private keys will range between `Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj` and `Fs3GFV6GNV6ar4b8eGcQWpGFbFtkNWKfEPdbywmha8ez5p7XMJyk` representing all zeros and all f-characters \(hex\).

#### **Entry Credit Private Keys**

Single signature private keys are represented in human readable form using the same base58check as the public keys. The only difference is the prefix bytes. The Entry Credit private key prefix is `0x5db6`.

Human readable Entry Credit private keys will range between `Es2Rf7iM6PdsqfYCo3D1tnAR65SkLENyWJG1deUzpRMQmbh9F3eG` and `Es4NQHwo8F4Z4oMnVwndtjV1rzZN3t5pP5u5jtdgiR1RA6FH4Tmc` representing all zeros and all f-characters \(hex\).

