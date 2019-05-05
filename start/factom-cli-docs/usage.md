---
description: This page describes how to use the Factom CLI
---

# Usage

## Run Factom Federation

_Time to remember Mr. Miyagi’s lesson._

This step will be used every time you need to run Factom Federation software, so get familiar with it. Practice makes perfect. Wax on, wax off.

Every time you come across “**Run FF**” you need to perform the following steps. These are the necessary steps to run the wallet.  
For Mac and Windows, use the cd command with Terminal to browse to the location of your FF installation. On Linux, you will be able to run commands without having to browse the to install location.

This step is required before you run factomd, factom-walletd, and factom-cli. The three applications are required to run the Factom Federation software.

In a new Terminal window, run

**Mac**

`cd /Applications/Factom/`

**Windows**

`cd C:\Program Files (x86)\Factom\`

On Mac, Windows and Linux, run “factomd” first

`factomd`

Then browse to [http://localhost:8090](http://localhost:8090/) to see the Control Panel for your local FF node.

![Control panel](https://docs.factom.com/images/wallet_018.png)

Syncing the Factom blockchain may take a little while. The Factom Control panel will display the progress and notify you when it has finished syncing. This will also occur when it has been a while since the last time you have run factomd. However, after the first full sync is complete, successive syncs are faster and you will only have to sync blocks since the last full sync. 

Once you are synced, in a new Terminal window browse \(`cd`\) to the location of your FF installation as you did above \(Mac and Windows only\).  
There are two options now, one for people who have run Factom Genesis \(FG\), our previous software release, and one for people who haven’t. The former has to import their old FG wallet file; the latter doesn’t. Choose the next step accordingly.

### If you have used FG

If you have run our previous software release “Factom Genesis \(FG\)” you need to import your FG wallet file \(named _factoid\_wallet\_bolt.db_\) the first time your run _factom-walletd_ to make sure all its previous addresses and balances are transferred over. You have learned how to backup your wallet file in our [Backup Your Wallet File!](https://developers.factomprotocol.org/wallets/enterprise-wallet/run-and-use-the-wallet#backup-your-wallets) guide and you should know if still in the default location within the .factom folder at ~/.factom/factoid\_wallet\_bolt.db.

Simply run the next command with a special flag and the path to your wallet file:

factom-walletd -i=PATH\_TO\_YOUR\_FGWALLETFILE.

For example, if your FG wallet file is still in the .factom folder, run:

`factom-walletd -i=~/.factom/factoid_wallet_bolt.db`

This command will tell factom-walletd to look for the file at the specified path and import all its addresses into the new wallet. The file can be located in a different location on your hard drive, just make sure to specify the path properly.

If by any chance the operation fails, quit factom-walletd, delete the new wallet file located at ~/.factom/wallet/factoid\_wallet.db and try again until you get all your addresses back.  
Remember, you only need to do this once the first time you run factom-walletd, after that you can run it normally.

### If you have never used FG

Run:

`factom-walletd`

> Terminal output for:  
> `factom-walletd`

```text
> factom-walletd

Reading from '/Home/.factom/m2/factomd.conf'
Cannot open custom config file,
Starting with default settings.
open /Home/.factom/m2/factomd.conf: no such file or directory

Reading from '/Home/.factom/m2/factomd.conf'
Cannot open custom config file,
Starting with default settings.
open /Home/.factom/m2/factomd.conf: no such file or directory

Warning, factom-walletd API is not password protected. Factoids can be stolen remotely.
Warning, factom-walletd API connection is unencrypted. The password is unprotected over the network.
Database started from: /Home/.factom/wallet/factom_wallet.db
Database started from: /Home/.factom/wallet/factoid_blocks.cache
2016/11/24 06:28:37 web.go serving :8089
```

You are now ready to use factom-cli to run commands in your third Terminal window. Run the command `-h` \(help\) to see all the available commands and their descriptions. `cd` to the location of your FF installation first, then run:

`factom-cli -h`

> Terminal output for:  
> `factom-cli -h`

```text
> factom-cli -h

Usage of ./factom-cli:

  -factomdcert string
        This file is the TLS certificate provided by the factomd API. (default ~/.factom/m2/factomdAPIpub.cert)
  -factomdpassword string
        Password for API connections to factomd
  -factomdtls
        Set to true when the factomd API is encrypted
  -factomduser string
        Username for API connections to factomd
  -h    help
  -s string
        IPAddr:port# of factomd API to use to access blockchain (default localhost:8088)
  -test.bench string
        regular expression per path component to select benchmarks to run
  -test.benchmem
        print memory allocations for benchmarks
  -test.benchtime duration
        approximate run time for each benchmark (default 1s)
  -test.blockprofile string
        write a goroutine blocking profile to the named file after execution
  -test.blockprofilerate int
        if >= 0, calls runtime.SetBlockProfileRate() (default 1)
  -test.count n
        run tests and benchmarks n times (default 1)
  -test.coverprofile string
        write a coverage profile to the named file after execution
  -test.cpu string
        comma-separated list of the number of CPUs to use for each test
  -test.cpuprofile string
        write a CPU profile to the named file during execution
  -test.memprofile string
        write a memory profile to the named file after execution
  -test.memprofilerate int
        if >=0, sets runtime.MemProfileRate
  -test.outputdir string
        directory in which to write profiles
  -test.parallel int
        maximum test parallelism (default 8)
  -test.run string
        regular expression to select tests and examples to run
  -test.short
        run smaller test suite to save time
  -test.timeout duration
        if positive, sets an aggregate time limit for all tests
  -test.trace string
        write an execution trace to the named file after execution
  -test.v
        verbose: print additional output
  -w string
        IPAddr:port# of factom-walletd API to use to create transactions (default localhost:8089)
  -walletcert string
        This file is the TLS certificate provided by the factom-walletd API. (default ~/.factom/walletAPIpub.cert)
  -walletpassword string
        Password for API connections to factom-walletd
  -wallettls
        Set to true when the wallet API is encrypted
  -walletuser string
        Username for API connections to factom-walletd

factom-cli ack TxID|FullTx
    Returns information about a factoid transaction, or an entry / entry credit transaction

factom-cli addchain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
    Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

factom-cli addentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
    Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
    Add an Entry Credit output to a transaction in the wallet

factom-cli addtxfee TXNAME ADDRESS
    Add the transaction fee to an input of a transaction in the wallet

factom-cli addtxinput TXNAME ADDRESS AMOUNT
    Add a Factoid input to a transaction in the wallet

factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
    Add a Factoid output to a transaction in the wallet

factom-cli backupwallet
    Backup the running wallet

factom-cli balance [-r] ADDRESS
    If this is an EC Address, returns the number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
    Buy entry credits

factom-cli composechain [-e EXTID1 -e EXTID2 -E BINEXTID3 ...] ECADDRESS <STDIN>
    Create API calls to create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

factom-cli composeentry -c CHAINID [-e EXTID1 -e EXTID2 -E BEEF1D ...] ECADDRESS <STDIN>
    Create API calls to create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

factom-cli composetx TXNAME
    Compose a wallet transaction into a JSON RPC object

factom-cli ecrate
    It takes this many Factoids to buy an Entry Credit.  Displays the larger between current and future rates. Also used to set Factoid fees.

factom-cli exportaddresses
    List the private addresses stored in the wallet

factom-cli get allentries|chainhead|dblock|eblock|entry|firstentry|head|heights
    Get data about Factom Chains, Entries, and Blocks

factom-cli get allentries [-n NAME1 -N HEXNAME2 ...] CHAINID
    Get all of the Entries in a Chain

factom-cli get chainhead [-n NAME1 -N HEXNAME2 ...] CHAINID
    Get ebhead by chainid

factom-cli get dblock KEYMR
    Get dblock contents by merkle root

factom-cli get eblock KEYMR
    Get eblock by merkle root

factom-cli get entry HASH
    Get entry by hash

factom-cli get firstentry [-n NAME1 -N HEXNAME2 ...] CHAINID
    Get the first entry from a chain

factom-cli get head
    Get the latest completed directory block

factom-cli get heights
    Get the current heights of various blocks in factomd

factom-cli importaddress ADDRESS [ADDRESS...]
    Import one or more secret keys into the wallet

factom-cli importwords '12WORDS'
    Import 12 words from Koinify sale into the Wallet

factom-cli listaddresses
    List the addresses stored in the wallet

factom-cli listtxs [tmp|all|address|id|range]
    List transactions from the wallet or the Factoid Chain

factom-cli listtxs address ECADDRESS|FCTADDRESS
    List transactions from the Factoid Chain with a particular address

factom-cli listtxs [all]
    List all transactions from the Factoid Chain

factom-cli listtxs id TXID
    List transaction from the Factoid Chain

factom-cli listtxs range START END
    List the transactions from the Factoid Chain within the specified range

factom-cli listtxs tmp
    List current working transactions in the wallet

factom-cli newecaddress
    Generate a new Entry Credit Address in the wallet

factom-cli newfctaddress
    Generate a new Factoid Address in the wallet

factom-cli newtx TXNAME
    Create a new transaction in the wallet

factom-cli properties
    Get version information about facotmd and the factom wallet

factom-cli receipt ENTRYHASH
    Returns a Receipt for a given Entry

factom-cli rmtx TXNAME
    Remove a transaction in the wallet

factom-cli sendfct FROMADDRESS TOADDRESS AMOUNT
    Send Factoids between 2 addresses

factom-cli sendtx TXNAME
    Send a Transaction to Factom

factom-cli signtx TXNAME
    Sign a transaction in the wallet

factom-cli subtxfee TXNAME ADDRESS
    Subtract the transaction fee from an output of a transaction in the wallet
```

## Generate a Factoid Address

To get started, [Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

You are now ready to use factom-cli to generate a new Factoid Address \(FA\).

Run:

`factom-cli newfctaddress`

> Terminal output for:  
> `factom-cli newfctaddress`

```bash
> factom-cli newfctaddress
FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S
```

 The new factoid address will be unique to your wallet and different from our example.

## Generate an Entry Credit Address

{% hint style="info" %}
Perform this step only if you intend to make entries into Factom or want to stock up on Entry Credits \(EC\) for future use. Remember, ECs are non-transferrable and cannot be sold or traded on an exchange. Make sure you need them before you go ahead.
{% endhint %}

To proceed, [Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

You are now ready to use factom-cli to generate a new Entry Credit \(EC\) address.

Run:

`factom-cli newecaddress`

Sample Terminal output is shown below.

> Terminal output for:  
> `factom-cli newecaddress`

```bash
> factom-cli newecaddress
EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
```

  The new EC address will be unique to your wallet and different from the above.

{% hint style="success" %}
Congratulations on your first EC address. You are seriously killing it.
{% endhint %}

## Send and Receive Factoids

**To send Factoids** \(FCT\) from your local wallet to an external Factoid Address \(FA\) you will need a source address and a destination address to execute the necessary command.

You need to perform this action when you want to send FCT to an exchange, a friend, or a third party.  
Assuming you have already [created a local FA address](https://developers.factomprotocol.org/start/factom-cli-docs/usage#generate-a-factoid-address) \(source address\) and have a destination address, you will need to:

[Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation) \(Yes, we know it’s growing on you\)

Here's an example for thesendfct command with:

 Terminal output for:  
`factom-cli sendfct`

```bash
> factom-cli sendfct FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.234
TxID: 0de09676c65ad18179c5a27cfbfae4f0392a42773b4024aed71eca937f7ce7a6
```

{% hint style="info" %}
Note that your FA addresses and FCT amount will be different.
{% endhint %}

In this example, the sendfct command moved 1.234 FCT from the source address to the destination address. You should be able to see the Transaction ID \(TxID\) on the terminal.

**To receive Factoids** use the same command as above. For instance, you may move FCT between two FA addresses within your local wallet.

However, if you are sending yourself FCT from an exchange or want to receive FCT from a third party, just provide your FA Address. Once sent you can [verify your local FCT balance](https://developers.factomprotocol.org/wallets/enterprise-wallet/run-and-use-the-wallet#verify-fct-and-ec-balances). 

{% hint style="info" %}
The TxID is a very useful way to verify that FCT have moved to the correct address. We recommend noting it down especially when sending or receiving to and from a third party.
{% endhint %}

## Convert Factoids to Entry Credits

_“It’s still magic even if you know how it’s done.”_  
_― Terry Pratchett, A Hat Full of Sky_

Before we automagically convert Factoids \(FCT\) to Entry Credits \(EC\), here is how the spell works. FCT are burned to create ECs. The number of FCT used will be deducted from your wallet’s balance, so don’t freak out when you see your FCT balance reduced. Just look for the newly created ECs on the EC address. Now if you don’t see the newly created ECs, it’s time to freak out and repeat these words, “Houston, we have a problem.” \(Disclaimer: Factom has no customer service center in Houston.\)

You will need a source address containing some FCT and a destination EC address to be able to execute the necessary command.

{% hint style="warning" %}
In this example, we assume that you have already created a local EC address \(destination\) and you have some FCT in your local FA address \(source\).
{% endhint %}

To get ECs proceed as follows.

[Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

Then use the buyec command with: .

> Terminal output for:  
> `factom-cli buyec`

```text
> factom-cli buyec FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 30
TxID: f378ef393897d5cc5ef910eb3c9aeea5988dfdbb8b94a6cc6a31c5876f629b6a
```

{% hint style="info" %}
Remember this is an example, and your FA and EC address, as well as the amount, will be different.
{% endhint %}

The buyec command burned some Factoids from the FA address and deposited 30 EC in the specified EC address. The Terminal also presented the TxID \(Transaction ID\). The TxID is useful for checking that ECs have moved to the right address. Take note of it for your records.

## Redeem Factoids from Koinify

This section is relevant if you participated in the Koinify Software Token Sale hosted by Koinify back in 2015 and haven’t redeemed your Factoids \(FCT\). Although Koinify closed their operations, they never held your FCT, and you only need your 12-word master passphrase to access your FCT.

The 12-word master passphrase can be used with the factom-cli importwords command to create the crypto signatures required to reassign the Factoids to another address or purchase Entry Credits. So, go find that magical piece of paper where you wrote down your unique 12-word magic spell and follow the instructions below:

[Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

In this example, we use the word “yellow” 12 times, but you probably have a different 12-word master passphrase.

In the factom-cli Terminal window run this command:

> Terminal output for:  
> `factom-cli importwords`

```bash
> factom-cli importwords "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"
FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1
```

The operation will create a new Factoid Address in your local wallet and present the public key in the terminal output as shown above. Make a note of the FA address for your records. You will need it to verify that the FA address successfully imported with its balance.

Run the listaddresses command to list all the addresses in your wallet.

> Terminal output for:  
> `factom-cli listaddresses`

```bash
> factom-cli listaddresses
FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1 20
```

In this example, we successfully imported the FA address showing a balance of 20 factoids. The terminal output will give you a list of all FA and EC addresses in your wallet with their current balances. 

You can use the Factom Explorer to [verify your local FCT balance](https://developers.factomprotocol.org/wallets/enterprise-wallet/run-and-use-the-wallet#verify-fct-and-ec-balances). In your case, the FA address and its balance will be different.

  
The 12-word master passphrase was shown once at the time of purchase to contributors who were prompted to keep it in a safe place. Without the Master Passphrase, it is impossible to redeem Factoids, and neither Factom nor Koinify can recover it. Do not share your passphrase with anybody or they will be able to access your FCT. There is no expiry date for the 12-word master passphrase. You will be able to redeem your FCT at your leisure, anytime in the future.

## Import a Private Key

To import a Factoid Address \(FA\) created with the Factoid Papermill app or by a third party you need the Factoid Private Key for the FA you want to import.

First, [Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

Then run the following command in the factom-cli Terminal window:  


> Terminal output for:  
> `factom-cli importaddress`

```text
> factom-cli importaddress Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj
```

This will import the below address below to your local wallet.

`FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC`

{% hint style="info" %}
Note that in our example we use a sample FA address Private Key, replace it with yours.
{% endhint %}

To verify that the FA address and its balance has successfully imported, run the listaddresses command to list all the addresses in your wallet.

> Terminal output for:  
> `factom-cli listaddresses`

```text
> factom-cli listaddresses
FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC 10
```

Our FA address has a balance of 10 factoids, but your balance will likely be different.

{% hint style="success" %}
You have successfully imported a Factoid Private Key and ready to use your balances! 
{% endhint %}

## Verify FCT and EC Balances

To know how to verify your FCT and EC balances [follow this guide](https://developers.factomprotocol.org/wallets/enterprise-wallet/run-and-use-the-wallet#verify-fct-and-ec-balances).

## Create a Factom Chain

To make entries in Factom, you must create a Factom Chain where your entries will be recorded. You can create as many chains as you like. Just remember, it’s a BYOEC party. You know… _bring your own entry credit party_. \(We know…what you are thinking. This is why we do Blockchains and not Standup\)

Creating a chain in Factom has a fee of 10 Entry Credits, so make sure your EC address balance can cover it.

First, [Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

In the factom-cli Terminal window run the addchain command as shown below.

```bash
echo "my first chain" | factom-cli addchain -n {chainName} {EC_Public_Key}
```

In your case, the only differences will be the data between the quotes, the _chainName_, and the EC address.

{% hint style="warning" %}
Be sure to use your EC address \(not our example\).  
{% endhint %}

> Terminal output for:  
> `factom-cli addchain`

```text
> echo "my first chain" | factom-cli addchain -n chainName EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
Committing Chain Transaction ID: c1a2861d14b788c13d6c48f1e5603f5c53afc599d07d338deeb4c3d5012e24da
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entryhash: 232d1e54ecdfc369cc66e35dda73ce4beb7dffd3e75af94192034e79beaf6c8f
```

If you’d like to upload a file as the first entry of a chain, you can use a standard input to do so rather than a pipe. For example:

```bash
factom-cli addchain -n {chainName} {EC_Public_Key} < {fileName}
```

The result is the same either way. You’ll now have a newly minted chain sitting immutably on the Factom blockchain.

{% hint style="info" %}
Take note of the ChainID as you will need it to make Factom entries later on.
{% endhint %}

## Make a Factom Entry

Once you have created your first Factom chain and noted the ChainID, you are ready to make your first entry! 

{% hint style="info" %}
Writing an entry in Factom costs 1 Entry Credit.
{% endhint %}

First, [Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

In the factom-cli Terminal window run the addentry command as constructed below:

```bash
echo "my first entry" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
```

In your case, the only differences will be the name between quotes, the _ChainID_, and the EC address. 

The name of the entry can be anything you want. In our example “my first entry” is the name of the new entry. Our ChainID `a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791` should be replaced by your own.

Finally, the EC address above should be replaced by your own, again, make sure it has enough EC balance to cover the fee.

> Terminal output for:  
> `factom-cli addentry`

```text
> echo "my first entry" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
Commiting Entry Transaction ID: 1d6b9d7159a27b91cd389738eb2b3b01143aaaf39ef46388f47abb8b32698811
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entryhash: 2460e676d4f4c89ccf0608b2e3134421b9075fb956af76c02af78991e6faafdc
```

{% hint style="info" %}
To make additional entries, repeat these steps using the same ChainID.
{% endhint %}

## Read Factom Entries

To read your Factom entries, you need the ChainID you used while creating your first chain.

First, [Run FF](https://developers.factomprotocol.org/start/factom-cli-docs/usage#run-factom-federation).

Use the get allentries command in the factom-cli Terminal window.

```bash
factom-cli get allentries a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
```

Your ChainID will be different from the example above.

> Terminal output for:  
> `factom-cli get allentries`

```text
> factom-cli get allentries a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entry [0] {
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
ExtID: chainName
Content:
my first chain
}
Entry [1] {
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Content:
my first entry
}
```

You may notice that there are two entries in the new chain even though you only made one. This is because every time a new chain is created, it generates an entry containing its assigned name. The second entry, \*Entry \[ 1 \]\*, is the first entry we made in the new chain, the one we named “my first entry.”

This simple guide is designed to show how chains and entries work in Factom. Refer to the factom-cli help by typing the below command for more options.

`factom-cli -h`

You can then explore other ways and more command flags you can run to make entries suited for your needs. We will also release more advanced guides in the near future. Stay tuned!

## Factoid Papermill

Factoid Papermill is an app to create private and public factoid address key pairs, the equivalent to a paper wallet for Factoids.

Factoids can be managed using the command line or the GUI wallet, which is a bit prettier.

Both the command-line and GUI wallets can import private keys generated with Factoid Papermill.  
Before attempting to transact factoids read this guide fully, at least once.

The Factoid Papermill app has a different name on different platforms.

* **Mac:** factoidpapermill-mac
* **Windows:** factoidpapermill.exe
* **Linux:** factoidpapermill-linux

### **Using Factoid Papermill**

Factoid Papermill is available for [Windows](https://github.com/FactomProject/factoidpapermill/blob/master/bin/factoidpapermill.exe?raw=true), [Mac](https://github.com/FactomProject/factoidpapermill/blob/master/bin/factoidpapermill-mac?raw=true), and [Linux](https://github.com/FactomProject/factoidpapermill/blob/master/bin/factoidpapermill-linux?raw=true).

Download the appropriate version and double-click to open.

Upon launching it will automatically generate a new Factoid Private Key and its relative Factoid Address.

> Terminal output for:  
> `factoidpapermill`

```text
> ~/factoidpapermill ; exit;
New Factoid Private Key: Fs2kwahPso3AKLNhcLSAeCLaYVzQ26jZbaHWamw1FipNiH8c9Uhv
New Factoid Address: FA39PmdJiiHjNAJN9Nj2GMUnBYnqn8KqiLNnvmVAifL39PAWQjyx
logout
Saving session...
...copying shared history...
...saving history...truncating history files...
...completed.
[Process completed]
```

Take note of the FA Address and Private Key and keep them in a safe place. If you need more addresses and private keys repeat the process. You can use your newly generated Factoid Address to receive factoids from a third party or an exchange. This method of storing factoids is considered a “cold wallet” or “paper wallet.”

Your New Factoid Private Key and New Factoid Address will be different than this example. Remember you won’t be able to send from your new address until you have imported it into one of your wallets.  
Failure to backup the Private Key generated by Factoid Papermill for a given Factoid Address will cause the loss of all factoids held, sent, or received by these addresses.  


If on Mac and Linux Factoid Papermill doesn’t launch because of missing execute permissions simply open a Terminal window and type:

```bash
chmod +x 
```

Then drag and drop the app onto the Terminal window to populate its path, and click enter. You should then be able to run FactoidPapermill as described above.

## Compile Factom Federation

Quick-start guide to help you compile and run Factom Federation software.

**Requirements not covered in guide**

* GoLang \(golang 1.7.4 recommended\)

**Requirements**

* Glide Package Manager

**Getting Glide**

Automatic install method:

`curl https://glide.sh/get | sh`

Manual installation can be found here: [https://glide.sh/](https://glide.sh/)  
BEFORE BUILDING FACTOMD! Glide can use GitHub to gather all dependencies, but there is a chance your local GitHub repos could cause some errors. If glide runs into an issue downloading a dependency, try deleting that folder it complains about \(90% of dependencies are in ’$GOPATH/src/github.com/FactomProject/’\), and run glide install again.

**Compile factomd**

This will take some time and place the source code into your GOPATH:

`go get github.com/FactomProject/factomd`

Cd into factomd:

`cd $GOPATH/src/github.com/FactomProject/factomd`

By default, the master branch will be selected. If you wish to build a different branch, change it now.

Use glide to install all the dependencies:

`glide install`

Now install factomd, go install will place the binary in $GOPATH/bin:

`go install -v`

If you wish the binary to be built in the active directory:

`go build -v`

**Run factomd**

If compiled with ‘go install’:

`factomd`

If compiled with 'go build’:

`cd $GOPATH/src/github.com/FactomProject/factomd`

Then run:

`./factomd`

Open a web browser and go to [http://localhost:8090](http://localhost:8090/) to see your factomd’s status.

**Compile factom-cli**

Get the repo:

`go get github.com/FactomProject/factom-cli`

Cd into factom-cli:

`cd $GOPATH/src/github.com/FactomProject/factom-cli`  
By default, the master branch will be selected. If you wish to build a different branch, change it now.

Use glide to install all the dependencies:

`glide install`

Now install factom-cli, go install will place the binary in $GOPATH/bin:

`go install -v`

If you wish the binary to be built in the active directory:

`go build -v`

**Compile factom-walletd**

Get the repo:

`go get github.com/FactomProject/factom-walletd`

Cd into factom-walletd:

`cd $GOPATH/src/github.com/FactomProject/factom-walletd`  
By default, the master branch will be selected. If you wish to build a different branch, change it now.

Use glide to install all the dependencies:

`glide install`

Now install factom-walletd, go install will place the binary in $GOPATH/bin:

`go install -v`

If you wish the binary to be built in the active directory:

`go build -v`

## Factom CLI Commands

```text
factom-cli [OPTIONS] SUBCOMMAND [OPTIONS]
```

factom-cli is a command line interface program for interacting with factomd and factom-walletd.

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

