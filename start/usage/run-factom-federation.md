# Run Factom Federation

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

