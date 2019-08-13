---
description: Command reference for the Factom CLI
---

# Factom CLI Commands

factom-cli is a command line interface program for interacting with factomd and factom-walletd.

```text
factom-cli [OPTIONS] SUBCOMMAND [OPTIONS]
```

### Flags

#### -f <a id="f"></a>

```bash
$ echo hello | factom-cli addchain -f -n moe -n larry \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The f flag, used with the addchain, addentry, buyec, composechain, composeentry, sendfct, sendtx, and signtx subcommands, tells factom-cli to continue on with processing without waiting for acknowledgment of the success of the subcommand to be generated. 

This can be useful for scripts where you can execute a long string of subcommands in a fraction of the time it would take if you had to wait for an acknowledgment of each command individually.

#### -q <a id="q"></a>

```bash
$ echo goodbye | factom-cli addentry -q -n moe -n larry -e curly \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The q flag specifies “quiet” execution of the addchain, addentry, addtxecoutput, addtxfee, addtxinput, addtxoutput, buyec, newtx, sendfct, sendtx, signtx, and subtxfee subcommands. This means that no output will be returned back to the user. 

This again can be useful for scripts where there is no need for feedback from factom-cli.

#### -e -x <a id="e-x"></a>

```bash
$ factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] \
[-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>
```

The addentry subcommands support the -e and -x flags for adding external ids to the Entries they create. Multiple -e and -x flags may be used, and -e and -x may be used in combination. -e string will encode the string as binary and set it as the next external id. -x hexstring will decode the hexstring into binary and set it as the next external id.

#### -n -h <a id="n-h"></a>

```bash
$ factom-cli get chainhead -n test -h 3031
```

The get firstentry, get chainhead, and get allentries subcommands support the -n and -h flags for using Chain Names as an alternative for providing a ChainID. The Chain Name is the combination of External IDs on the first Entry in the Chain.

#### -r <a id="r"></a>

```bash
$ factom-cli sendfct -r $my_factoid_address factom.michaeljbeam.me
```

The r flag tells factom-cli to try and resolve a public Factoid or Entry Credit Address from a DNS name registered through Netki.

#### -C <a id="c"></a>

```bash
$ echo hello | factom-cli addchain -n moe -n larry -C \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The C flag, used with the addchain subcommand, limits the subcommand output to a single field, the ChainID with no headers. This means that a variable can be assigned to the value of the executed command directly.

#### -E <a id="e"></a>

```bash
$ echo goodbye | factom-cli addentry -n moe -n larry -e curly -E \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The E flag, used with the addchain and addentry subcommands, limits the subcommand output to a single field, the Entry Hash with no headers. This means that a variable can be assigned to the value of the executed command directly.

#### -T <a id="t"></a>

```bash
$ factom-cli get pendingtransactions -T
```

The T flag, used with the addchain, addentry, buyec, get pendingtransactions, listtxs address, listtxs subcommands, limits the subcommand output to a single field, the Entry Hash with no headers. This means that a variable can be assigned to the value of the executed command directly.

### Commands <a id="commands"></a>

#### status <a id="status"></a>

```bash
factom-cli status TxID|FullTx
```

Returns information about a factoid transaction, or an entry / entry credit transaction

#### addchain <a id="addchain"></a>

```bash
factom-cli addchain [-fq] [-n NAME1 -n NAME2 -h HEXNAME3 ] [-CET] /
ECADDRESS <STDIN>
```

Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

#### addentry <a id="addentry"></a>

```bash
factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] /
 [-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>
```

Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

#### addtxecoutput <a id="addtxecoutput"></a>

```bash
factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
```

Add an Entry Credit output to a transaction in the wallet

#### addtxfee <a id="addtxfee"></a>

```bash
factom-cli addtxfee TXNAME ADDRESS
```

Add the transaction fee to an input of a transaction in the wallet

#### addtxinput <a id="addtxinput"></a>

```bash
factom-cli addtxinput TXNAME ADDRESS AMOUNT
```

Add a Factoid input to a transaction in the wallet

#### addtxoutput <a id="addtxoutput"></a>

```bash
factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
```

Add a Factoid output to a transaction in the wallet

#### backupwallet <a id="backupwallet"></a>

```bash
factom-cli backupwallet
```

Backup the running wallet

#### balance <a id="balance"></a>

```bash
factom-cli balance [-r] ADDRESS
```

If this is an EC Address, returns the number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

#### buyec <a id="buyec"></a>

```bash
factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
```

Buy entry credits

#### composechain <a id="composechain"></a>

```text
$ factom-cli composechain [-f] [-n NAME1 -n NAME2 -h HEXNAME3 ] /
ECADDRESS <STDIN>
```

Create API calls to create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

#### composeentry <a id="composeentry"></a>

```text
$ factom-cli composeentry [-f] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] /
[-e EXTID1 -e EXTID2 -x HEXEXTID ...] ECADDRESS <STDIN>
```

Create API calls to create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

#### composetx <a id="composetx"></a>

```text
$ factom-cli composetx TXNAME
```

Compose a wallet transaction into a JSON RPC object

#### ecrate <a id="ecrate"></a>

```text
factom-cli ecrate
```

It takes this many Factoids to buy an Entry Credit. Displays the larger between current and future rates. Also used to set Factoid fees.

#### exportaddresses <a id="exportaddresses"></a>

```text
factom-cli exportaddresses
```

List the private addresses stored in the wallet

#### get <a id="get"></a>

```text
factom-cli get allentries|chainhead|dblock|eblock|entry|firstentry| /
head|heights
```

Get data about Factom Chains, Entries, and Blocks

#### get allentries <a id="get-allentries"></a>

```text
factom-cli get allentries [-n NAME1 -N HEXNAME2 ...] CHAINID
```

Get all of the Entries in a Chain

#### get chainhead <a id="get-chainhead"></a>

```text
factom-cli get chainhead [-n NAME1 -N HEXNAME2 ...] CHAINID
```

Get ebhead by chainid

#### get dblock <a id="get-dblock"></a>

```text
factom-cli get dblock KEYMR
```

Get dblock contents by Merkle root

#### get eblock <a id="get-eblock"></a>

```text
factom-cli get eblock KEYMR
```

Get eblock by Merkle root

#### get entry <a id="get-entry"></a>

```text
factom-cli get entry HASH
```

Get entry by hash

#### get firstentry <a id="get-firstentry"></a>

```text
factom-cli get firstentry [-n NAME1 -N HEXNAME2 ...] CHAINID
```

Get the first entry from a chain

#### get head <a id="get-head"></a>

```text
factom-cli get head
```

Get the latest completed directory block

#### get heights <a id="get-heights"></a>

```text
factom-cli get heights
```

Get the current heights of various blocks in factomd

#### importaddress <a id="importaddress"></a>

```text
factom-cli importaddress ADDRESS [ADDRESS...]
```

Import one or more secret keys into the wallet

#### importwords <a id="importwords"></a>

```text
factom-cli importwords '12WORDS'
```

Import 12 words from Koinify sale into the Wallet

#### listaddresses <a id="listaddresses"></a>

```text
factom-cli listaddresses
```

List the addresses stored in the wallet

#### listtxs <a id="listtxs"></a>

```text
factom-cli listtxs [tmp|all|address|id|range]
```

List transactions from the wallet or the Factoid Chain

#### listtxs address <a id="listtxs-address"></a>

```text
factom-cli listtxs address ECADDRESS|FCTADDRESS
```

List transaction from the Factoid Chain with a specific address. This command will only list confirmed transactions.

#### listtxs \[all\] <a id="listtxs-all"></a>

```text
factom-cli listtxs [all]
```

List all transactions from the Factoid Chain. This command will only list confirmed transactions.

#### listtxs id <a id="listtxs-id"></a>

```text
factom-cli listtxs id TXID
```

List transaction from the Factoid Chain. This command will only list confirmed transactions.

#### listtxs range <a id="listtxs-range"></a>

```text
factom-cli listtxs range START END
```

List the transactions from the Factoid Chain within the specified range. This command will only list confirmed transactions.

#### listtxs tmp <a id="listtxs-tmp"></a>

```text
factom-cli listtxs tmp
```

List current working transactions in the wallet

#### newecaddress <a id="newecaddress"></a>

```text
factom-cli newecaddress
```

Generate a new Entry Credit Address in the wallet

#### newfctaddress <a id="newfctaddress"></a>

```text
factom-cli newfctaddress
```

Generate a new Factoid Address in the wallet

#### newtx <a id="newtx"></a>

```text
factom-cli newtx TXNAME
```

Create a new transaction in the wallet

#### properties <a id="properties"></a>

```text
factom-cli properties
```

Get version information about facotmd and the factom wallet

#### receipt <a id="receipt"></a>

```text
factom-cli receipt ENTRYHASH
```

Returns a Receipt for a given Entry

#### rmtx <a id="rmtx"></a>

```text
factom-cli rmtx TXNAME
```

Remove a transaction in the wallet

#### sendfct <a id="sendfct"></a>

```text
factom-cli sendfct FROMADDRESS TOADDRESS AMOUNT
```

Send Factoids between 2 addresses

#### sendtx <a id="sendtx"></a>

```text
factom-cli sendtx TXNAME
```

Send a Transaction to Factom

#### signtx <a id="signtx"></a>

```text
factom-cli signtx TXNAME
```

Sign a transaction in the wallet

#### subtxfee <a id="subtxfee"></a>

```text
factom-cli subtxfee TXNAME ADDRESS
```

Subtract the transaction fee from an output of a transaction in the wallet

