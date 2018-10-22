# Factom CLI Docs

This is the Factom CLI documentation. The following guides will allow you to install, run and/or compile and build the command line apps and tools necessary to run Factom Federation software.

These new Factom guides replace all our previous ones. The Factom CLI guides are intended for users who know their way around the command line \(you should know enough to be dangerous and get yourself out of trouble\).

## Factom CLI Guides <a id="factom-cli-guides"></a>

### Before We Begin <a id="before-we-begin"></a>

Before attempting to transact factoids \(FCT\) read these guides thoroughly \(at least once\). The software is still in beta, so use the instructions at your risk. Do not use a large number of Factoids in case there are issues, bugs, or you mistype a command. Phoning a friend after the damage is done will not fix things. Sorry, this is just the way of the Blockchain. If you are unsure how to use the command line, we suggest you try our Factom Foundation Wallet instead which is simpler to use and has a Graphic User Interface \(GUI\).

The following directions and commands are optimized for Linux but should work with minor modifications for Mac or Windows. Be aware of slight differences in commands on different platforms:

**Mac**

`./factom-cli < rest of the command >`

**Windows**

`factom-cli.exe < rest of the command >`

**Linux**

`factom-cli < rest of the command >`

Make sure to modify the commands accordingly.

The interface you will be using to run Factom Federation software related commands is called:

* “Terminal” on the Mac and Linux
* “CMD Prompt” or “Windows Power Shell” on Windows

Give it a try and get familiar before you go any further. Going forward we will use “Terminal” to describe the interface where you type commands, just don’t forget it has a different name in Windows.

FF is composed of three main components:

* factomd
* factom-walletd
* factom-cli

To run Factom Federation via command line, you need factomd, factom-walletd, and factom-cli. Each one of these apps needs to be run in separate Terminal windows.  
Pop quiz  
How many windows will you need?  
Answer: Three Terminal windows.  
What your tech-savvy mother would say?  
Do not run Factom Federation while connected to an unsafe network, like at a cafe, an airport, public wifi hotspot, etc. The wallet is not encrypted, and hackers could potentially steal your precious Factoids. You do not want to feel like Gollum without his ring.

#### Starting Factom Via Bootstrap <a id="starting-factom-via-bootstrap"></a>

Factom takes a while to download the blockchain. It can be expedited by downloading the first 70k blocks via HTTP. Factomd still checks the blockchain on each boot, so it will check for inconsistencies in the download.  
Note: currently factomd uses a lot of drive accesses when running. It is recommended to hold the blockchain on a solid state drive. Running factomd on a spinning hard drive will be arduously slow. Since factomd currently scans the entire blockchain each time it is started, bootup takes a while \(~30 min on an SSD\). You can watch the progress on the Control Panel.

Download the blockchain [here](https://www.factom.com/assets/site/factom_bootstrap.zip).

Extract the zip file to your home directory. It will create files in the location:

~/.factom/m2/main-database/ldb/MAIN/factoid\_level.db/  
The newly created .factom folder is an invisible folder on Mac and Linux so you won’t be able to see it unless you browse to it via Terminal. On Mac, in Finder, you can also use Go/Go to Folder… and type ~/.factom to see its content.

The blockchain is currently about 12 GB at the time of writing.  
After factomd boots for the first time and is 100% synced, you will have your own local copy of the Factom blockchain. Successive restarts will only require you to download new blocks and not the entire blockchain.

### Backup Your Wallet File! <a id="backup-your-wallet-file"></a>

**If you’ve used Factom Genesis \(FG\)**, our previous software release, you should have a local wallet file. We highly recommend you backup your \(FG\) wallet file every time you import or generate a new address. Do read this guide fully, at least once.

**If you have never run FG** you can skip the backup right now, but we strongly recommend backing up your new FF wallet once you get FF running.

Get back to this guide when you are ready to do your backup, don’t forget!  
Factom Federation \(FF\) introduced a new way to generate addresses compared to our FG release. Simply put, it generates all new addresses from a seed. The seed is a 12-word passphrase which allows you to recover all your addresses, created with the seed in question, at a later date even if you lose your wallet file. There are many reasons why you may have misplaced your original wallet file such as because you changed computer, your hard drive failed, have overwritten the wallet file by mistake, and so on.  
  
The seed comes to the rescue because if you ever lose your wallet file, you can always re-generate your addresses from it. However, some of you may have imported a Private Key generated with the Factoid Papermill app, or have imported a 12-word Koinify passphrase, or generated addresses with our previous FG wallet, these types of addresses are called “External Addresses.” Please remember that a seed file will only allow you to recover addresses that were created with the same seed, external addresses will not be recovered.  
  
So how to recover External Addresses?  
The simple way: if you have any balances on addresses not generated from your wallet seed, you may want to transfer them to an address generated from your seed.  
The easy way: keep a backup of your wallet file, whatever addresses are in there will always be, no need to recover them.   
The alternative way: make sure to keep your external addresses’ Private Keys safe, write them down or copy/paste them to a file, you can always import them even if you create a new wallet.  
  
Keep this in mind especially if you are migrating from our FG wallet to our FF wallet. If you are not careful, you may lose access to your Factoids and Entry Credits!

**Backup your Factom Genesis \(FG\) wallet file**

Make sure to backup your FG wallet file before you run the new Factom Federation software. The wallet file is called “factoid\_wallet\_bolt.db” and is located in the .factom folder at the following locations:

* **Mac** `/Users/YourUsername/.factom/factoid_wallet_bolt.db`
* **Windows** `C:\Users\YourUsername\.factom\factoid_wallet_bolt.db`
* **Linux** `~/.factom/factoid_wallet_bolt.db`

  
Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for “how to show hidden files and folders on YOUR OS”, replacing YOUR OS with Mac or Linux accordingly.

**To backup** your FG wallet file, locate the factoid\_wallet\_bolt.db file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.  
By having a backup somewhere safe, if something goes wrong, you can always try again, but most importantly, you’ll be able to import all your FG addresses and their balances into your new FF wallet the first time you run FF. We will explain to you how to do that when “we cross that bridge” in the Run Factom Federation guide.

**Backup your Factom Federation \(FF\) wallet file**

The wallet file is called “factom\_wallet.db” and is located in the .factom folder at the following locations:

* **Mac** `/Users/YourUsername/.factom/wallet/factom_wallet.db`
* **Windows** `C:\Users\YourUsername\.factom\wallet\factom_wallet.db`
* **Linux** `~/.factom/wallet/factom_wallet.db`

  
Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for “how to show hidden files and folders on YOUR OS,” replacing YOUR OS with Mac or Linux accordingly.

**To backup** your FF wallet file, quit factomd and factom-walletd, locate the factom\_wallet.db file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.

**To create a fresh** FF wallet file, quit factomd and factom-walletd then move your wallet file to a safe location out of the .factom folder. There should be no wallet file in the .factom folder. Restart factomd and factom-walletd and a new empty wallet will be generated.

**To restore** a previous FF wallet file backup, quit factomd and factom-walletd, make sure you have a backup of the current wallet first, then drag & drop the previous backup in the .factom folder, overwrite if needed. Restart factomd and factom-walletd and your previous wallet will now be used instead.  
Pay attention when performing backups and restores. Each wallet file has its unique seed and addresses. Overwriting a wallet may result in losing all your Factoids and Entry Credits. Not cool.

### Install Factom Federation <a id="install-factom-federation"></a>

If you got this far, you are doing well Grasshopper. Ready to get your hands on FF? You will be up and running in a few minutes. Promise.

Here is a step by step guide on how to install FF binaries on Mac, Windows, and Linux.

**Step 1** Download the installer for Mac, Windows, or Linux on [GitHub](https://github.com/FactomProject/distribution). There are various versions, make sure to select the one best suited for your system.

**Step 2** Save it to your desktop or downloads folder on your local hard drive.

**Step 3** Follow the instructions for your OS.

#### Mac <a id="mac"></a>

This installer is for factomd, factom-walletd, factom-cli, the 3 binaries will be installed in /Applications/Factom/ together with a .factom folder in the root of the local user Home Folder. These are all required to run Factom via command line or the Factom Foundation Wallet.

Before you start, go to System Preferences/Security & Privacy, click on the lock at the bottom left of the window, type your username and password, then select “Allow apps downloaded from: Anywhere.” At the prompt click on “Allow From Anywhere.”

![Security &amp; Privacy](https://docs.factom.com/images/wallet_005.png)  
Note that after running the Factom installer it is recommended you revert back your Security & Privacy settings to their original state.

Next, locate the “factom.mpkg.zip” file you just downloaded, double-click to unzip it, then double-click the “factom.mpkg” file to run the installer.

The installer will open, click continue.

![Installer Step 1](https://docs.factom.com/images/wallet_006.png)

Then click install.

![Installer Step 2](https://docs.factom.com/images/wallet_007.png)

The installer will prompt for your username and password; you need to have Admin privileges on the Mac \(means you need to be able to install applications on your Mac\).

Enter your username and password then click Install Software.

![Installer Step 3](https://docs.factom.com/images/wallet_008.png)

The installer will proceed with the installation and once finished it will prompt with “The installation was successful.” Then click close.

![Installer Step 4](https://docs.factom.com/images/wallet_009.png)

You made it so far! Wasn’t that hard, was it?

You are now ready to [run Factom Federation](https://docs.factom.com/cli#run-factom-federation).

#### Windows <a id="windows"></a>

This installer is for factomd, factom-walletd, factom-cli, the three binaries will be installed in c:\Program Files \(x86\)\Factom\ or c:\Program Files\Factom\ \(depending on your system\) together with a .factom folder in the root of the local user Home Folder. These are all required to run Factom via command line or the Factom Wallet GUI.

Next, locate the “FactomInstall-amd64.msi” or “FactomInstall-i386.msi” file you just downloaded in Step 1.

Double click the .msi installer to run it, but you may be prompted with the following message.

![Windows Prompt 1](https://docs.factom.com/images/wallet_010.png)

Click on “more info” to expand it then select “Run anyway.”

![Windows Prompt 2](https://docs.factom.com/images/wallet_011.png)

The Installer will open, click “Next.”

![Installer Step 1](https://docs.factom.com/images/wallet_012.png)

Select “I accept the terms in the Licence Agreement” and click “Next” to continue.

![Installer Step 2](https://docs.factom.com/images/wallet_013.png)

Make sure Factom is installed into c:\Program Files \(x86\)\Factom\ folder and click “Next” to continue.

![Installer Step 3](https://docs.factom.com/images/wallet_014.png)

Then click “Install.”

![Installer Step 4](https://docs.factom.com/images/wallet_015.png)

Select “Yes” to continue if you get the following message.

![Windows Prompt 3](https://docs.factom.com/images/wallet_016.png)

When the installation is over select “Finish” to exit the installer.

![Installer Step 5](https://docs.factom.com/images/wallet_017.png)

You made it so far, and ready to [run Factom Federation](https://docs.factom.com/cli#run-factom-federation) on Windows!

#### Linux <a id="linux"></a>

This installer is for factomd, factom-walletd, factom-cli, the three binaries will be installed on your local drive together with a .factom folder in the root of the local user Home Folder ~/.factom. These are all required to run Factom via command line or the Factom Foundation Wallet.

Download the “factom-amd64.deb” or “factom-i386.deb” installer that suits your system as per Step 1 then run the following command to install.

`sudo dpkg -i ./factom-amd64.deb`

or

`sudo dpkg -i ./factom-i386.deb`

We are aware Linux users are hardcore, so we made sure one command is all they need to be ready to [run Factom Federation](https://docs.factom.com/cli#run-factom-federation).

#### Docker <a id="docker"></a>

If you’ve made it this far, you may not have an operating system. This will make it very difficult to run Factom Federation since, at this point, we do still require you to use a computing device. However, if you’re simply looking for a way to get started in ANY environment, you’ve come to the right place.

Because we are a very modern organization, we’ve made arrangements for you to get started in a containerized environment. All you need is [Docker](https://www.docker.com/) at minimum v17 and a clone of the [factomd repo](https://github.com/FactomProject/factomd).

**Build**

From wherever you have cloned the factomd repo, run

`docker build -t factomd_container .`

\(yes, you can replace **factomd\_container** with whatever you want to call the container. e.g. **factomd**, **foo**, etc.\)  
**Cross-Compile**   


To cross-compile for a different target, you can pass in a `build-arg` as so   
  
`docker build -t factomd_container --build-arg GOOS=darwin .`

**Run**

**No Persistence**

`docker run --rm -p 8090:8090 factomd_container`

* This will start up **factomd** with no flags.
* The Control Panel is accessible at port 8090 
* When the container terminates, all data will be lost

 In the above, replace **factomd\_container** with whatever you called it when you built it - e.g. **factomd**, **foo**, etc.

**With Persistence**

1. `docker volume create factomd_volume`
2. `docker run --rm -v $(PWD)/factomd.conf:/source -v factomd_volume:/destination busybox /bin/cp /source /destination/factomd.conf`
3. `docker run --rm -p 8090:8090 -v factomd_volume:/root/.factom/m2 factomd_container`

* This will start up **factomd** with no flags.
* The Control Panel is accessible at port 8090 
* When the container terminates, the data will remain persisted in the volume **factomd\_volume**
* The above copies **factomd.conf** from the local directory into the container. Put _your_ version in there, or change the path appropriately.

 In the above

* replace **factomd\_container** with whatever you called it when you built it - e.g. **factomd**, **foo**, etc.
* replace **factomd\_volume** with whatever you might want to call it - e.g. **myvolume**, **barbaz**, etc.

**Additional Flags**

In all cases, you can startup with additional flags by passing them at the end of the docker command, e.g.

`docker run --rm -p 8090:8090 factomd_container -port 9999`

**Copy**

```text
docker run --rm --entrypoint='' \
    -v <FULLY_QUALIFIED_PATH_TO_TARGET_DIRECTORY>:/destination factomd_container \
    /bin/cp /go/bin/factomd /destination
```

> The following will copy the binary to `/tmp/factomd`

```text
docker run --rm --entrypoint='' \
-v /tmp:/destination factomd_container \
/bin/cp /go/bin/factomd /destination
```

So yeah, you want to get your binary _out_ of the container. To do so, you basically mount your target into the container and copy the binary over as shown.You should replace **factomd\_container** with whatever you called it in the [build](https://docs.factom.com/cli#build) section above e.g. **factomd**, **foo**, etc.

**Cross-Compile Copy**

> Cross-Compile copy

```text
docker run --rm --entrypoint='' \
-v <FULLY_QUALIFIED_PATH_TO_TARGET_DIRECTORY>:/destination \
factomd_container \
/bin/cp /go/bin/darwin_amd64/factomd /destination
```

> To copy the darwin\_amd64 version of the binary to `/tmp/factomd`…

```text
docker run --rm --entrypoint='' 
-v /tmp:/destination factomd_container \
/bin/cp /go/bin/darwin_amd64/factomd /destination
```

If you cross-compiled to a different target, your binary will be in `/go/bin/<target>/factomd`. e.g. If you built with `--build-arg GOOS=darwin`, then you can copy out the binary using the commands shown on the right.You should replace **factomd\_container** with whatever you called it in the **build** section above e.g. **factomd**, **foo**, etc.

### Run Factom Federation <a id="run-factom-federation"></a>

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

![node 01](https://docs.factom.com/images/wallet_018.png)  
If this is the first time you are running FF, and haven’t downloaded the blockchain via HTTP as recommended above, now’s a very good time to check your Facebook feed or take your dog for a walk. The blockchain is… big. Syncing the Factom blockchain may take a little while. The Factom Control panel will display the progress and notify you when it has finished syncing. This will also occur when it has been a while since the last time you have run factomd. However, after the first full sync is complete, successive syncs are faster and you will only have to sync blocks since the last full sync.   
You can alternatively download the first 70,000 blocks via disk image by following our [Bootstrap Guide](https://docs.factom.com/cli#starting-factom-via-bootstrap).

Once you are synced, in a new Terminal window browse \(cd\) to the location of your FF installation as you did above \(Mac and Windows only\).  
There are two options now, one for people who have run Factom Genesis \(FG\), our previous software release, and one for people who haven’t. The former has to import their old FG wallet file; the latter doesn’t. Choose the next step accordingly.

#### If you have used FG <a id="if-you-have-used-fg"></a>

If you have run our previous software release “Factom Genesis \(FG\)” you need to import your FG wallet file \(named _factoid\_wallet\_bolt.db_\) the first time your run _factom-walletd_ to make sure all its previous addresses and balances are transferred over. You have learned how to backup your wallet file in our [Backup Your Wallet File!](https://docs.factom.com/cli#backup-your-wallet-file) guide and you should know if still in the default location within the .factom folder at ~/.factom/factoid\_wallet\_bolt.db.

Simply run the next command with a special flag and the path to your wallet file:

factom-walletd -i=PATH\_TO\_YOUR\_FGWALLETFILE.

For example, if your FG wallet file is still in the .factom folder, run:

`factom-walletd -i=~/.factom/factoid_wallet_bolt.db`

This command will tell factom-walletd to look for the file at the specified path and import all its addresses into the new wallet. The file can be located in a different location on your hard drive, just make sure to specify the path properly.

If by any chance the operation fails, quit factom-walletd, delete the new wallet file located at ~/.factom/wallet/factoid\_wallet.db and try again until you get all your addresses back.  
Remember, you only need to do this once the first time you run factom-walletd, after that you can run it normally.

Once you are happy, continue by following the instructions to run the factom-cli command below.

#### If you have never used FG <a id="if-you-have-never-used-fg"></a>

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

Sample Terminal output is shown on the right.   
  


You are now ready to use factom-cli to run commands in your third Terminal window. Run the command -h \(help\) to see all the available commands and their descriptions. cd to the location of your FF installation first, then run:

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

Sample Terminal output is shown on the right.   
  


Pat yourself on the back for making it this far! You have now “Run FF” for the first time. \(thumbs up\)  
Now it’s a good time to [Backup Your Wallet File!](https://docs.factom.com/cli#backup-your-wallet-file)

### Generate a Factoid Address <a id="generate-a-factoid-address"></a>

To get started, [Run FF](https://docs.factom.com/cli#run-factom-federation).

You are now ready to use factom-cli to generate a new Factoid Address \(FA\).

Run:

`factom-cli newfctaddress`

> Terminal output for:  
> `factom-cli newfctaddress`

```text
> factom-cli newfctaddress
FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S
```

Sample Terminal output is shown on the right.   
  
 The new factoid address will be unique to your wallet and different from our example.

You are on a roll and a proud owner of a Factoid address! \#Winning

### Generate an Entry Credit Address <a id="generate-an-entry-credit-address"></a>

Perform this step only if you intend to make entries into Factom or want to stock up on Entry Credits \(EC\) for future use. Remember, ECs are non-transferrable and cannot be sold or traded on an exchange. Make sure you need them before you go ahead.

To proceed, [Run FF](https://docs.factom.com/cli#run-factom-federation).

You are now ready to use factom-cli to generate a new Entry Credit \(EC\) address.

Run:

`factom-cli newecaddress`

> Terminal output for:  
> `factom-cli newecaddress`

```text
> factom-cli newecaddress
EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
```

Sample Terminal output is shown on the right.   
  
 The new EC address will be unique to your wallet and different from the above.

Congratulations on your first EC address. You are seriously killing it.

### Send and Receive Factoids <a id="send-and-receive-factoids"></a>

**To send Factoids** \(FCT\) from your local wallet to an external Factoid Address \(FA\) you will need a source address and a destination address to execute the necessary command.

You need to perform this action when you want to send FCT to an exchange, a friend, or a third party.  
Assuming you have already [created a local FA address](https://docs.factom.com/cli#generate-a-factoid-address) \(source address\) and have a destination address, you will need to:

[Run FF](https://docs.factom.com/cli#run-factom-federation) \(Yes, we know it’s growing on you\)

Then type the sendfct command with:

Here is an example.

`factom-cli sendfct FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.234` Note that your FA addresses and FCT amount will be different.

> Terminal output for:  
> `factom-cli sendfct`

```text
> factom-cli sendfct FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S 1.234
TxID: 0de09676c65ad18179c5a27cfbfae4f0392a42773b4024aed71eca937f7ce7a6
```

Sample Terminal output is shown on the right.   
  


In this example, the sendfct command moved 1.234 FCT from the source address to the destination address. You should be able to see the Transaction ID \(TxID\) on the terminal.

**To receive Factoids** use the same command as above. For instance, you may move FCT between two FA addresses within your local wallet.

However, if you are sending yourself FCT from an exchange or want to receive FCT from a third party, just provide your FA Address. Once sent you can [verify your local FCT balance](https://docs.factom.com/cli#verify-fct-and-ec-balances). The TxID is a very useful way to verify that FCT have moved to the correct address. We recommend noting it down especially when sending or receiving to and from a third party.

### Convert Factoids to Entry Credits <a id="convert-factoids-to-entry-credits"></a>

_“It’s still magic even if you know how it’s done.”_  
_― Terry Pratchett, A Hat Full of Sky_

Before we automagically convert Factoids \(FCT\) to Entry Credits \(EC\), here is how the spell works. FCT are burned to create ECs. The number of FCT used will be deducted from your wallet’s balance, so don’t freak out when you see your FCT balance reduced. Just look for the newly created ECs on the EC address. Now if you don’t see the newly created ECs, it’s time to freak out and repeat these words, “Houston, we have a problem.” \(Disclaimer: Factom has no customer service center in Houston.\)

Moving on…and getting down to business.

You will need a source address containing some FCT and a destination EC address to be able to execute the necessary command.

In this example, we assume that you have already created a local EC address \(destination\) and you have some FCT in your local FA address \(source\).

To get ECs proceed as follows.

[Run FF](https://docs.factom.com/cli#run-factom-federation).

Then use the buyec command with: .

`factom-cli buyec FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 30` Remember this is an example, and your FA and EC address, as well as the amount, will be different.

> Terminal output for:  
> `factom-cli buyec`

```text
> factom-cli buyec FA28PitepUziaDrLeVAcioNfzHdBc7mvyJJHvag2vyhWm7JR3t8S EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX 30
TxID: f378ef393897d5cc5ef910eb3c9aeea5988dfdbb8b94a6cc6a31c5876f629b6a
```

Sample Terminal output is shown on the right.   
  


The buyec command burned some Factoids from the FA address and deposited 30 EC in the specified EC address. The Terminal also presented the TxID \(Transaction ID\). The TxID is useful for checking that ECs have moved to the right address. Take note of it for your records.

### Redeem Factoids from Koinify <a id="redeem-factoids-from-koinify"></a>

This section is relevant if you participated in the Koinify Software Token Sale hosted by Koinify back in 2015 and haven’t redeemed your Factoids \(FCT\). Although Koinify closed their operations, they never held your FCT, and you only need your 12-word master passphrase to access your FCT.

The 12-word master passphrase can be used with the factom-cli importwords command to create the crypto signatures required to reassign the Factoids to another address or purchase Entry Credits. So, go find that magical piece of paper where you wrote down your unique 12-word magic spell and follow the instructions below:

[Run FF](https://docs.factom.com/cli#run-factom-federation).

In this example, we use the word “yellow” 12 times, but you probably have a different 12-word master passphrase.

In the factom-cli Terminal window run this command:

`factom-cli importwords "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"`

> Terminal output for:  
> `factom-cli importwords`

```text
> factom-cli importwords "yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow yellow"
FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1
```

Sample Terminal output is shown on the right.   
  


The operation will create a new Factoid Address in your local wallet and present the public key in the terminal output. Make a note of the FA address for your records. You will need it to verify that the FA address successfully imported with its balance.

Run the listaddresses command to list all the addresses in your wallet.

`factom-cli listaddresses`

> Terminal output for:  
> `factom-cli listaddresses`

```text
> factom-cli listaddresses
FA3cih2o2tjEUsnnFR4jX1tQXPpSXFwsp3rhVp6odL5PNCHWvZV1 20
```

Sample Terminal output is shown on the right.   
  


In this example, we successfully imported the FA address showing a balance of 20 factoids. The terminal output will give you a list of all FA and EC addresses in your wallet with their current balances. You can use the Node Visualizer or the Factom Explorer to [verify your local FCT balance](https://docs.factom.com/cli#verify-fct-and-ec-balances). In your case, the FA address and its balance will be different.

You can now trade your factoids on an exchange or use them to purchase Entry Credits. Life is good. \(thumbs up\)  
The 12-word master passphrase was shown once at the time of purchase to contributors who were prompted to keep it in a safe place.   
Without the Master Passphrase, it is impossible to redeem Factoids, and neither Factom nor Koinify can recover it. We really meant what we said.   
Do not share your passphrase with anybody or they will be able to access your FCT.   
There is no expiry date for the 12-word master passphrase. You will be able to redeem your FCT at your leisure, anytime in the future.

### Import a Private Key <a id="import-a-private-key"></a>

To import a Factoid Address \(FA\) created with the Factoid Papermill app or by a third party you need the Factoid Private Key for the FA you want to import.

First, [Run FF](https://docs.factom.com/cli#run-factom-federation).

Then run the following command in the factom-cli Terminal window:

`factom-cli importaddress Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj`  
Note that in our example we use a sample FA address Private Key, replace it with yours.  


This will import the below address below to your local wallet.

FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC

> Terminal output for:  
> `factom-cli importaddress`

```text
> factom-cli importaddress Fs1KWJrpLdfucvmYwN2nWrwepLn8ercpMbzXshd1g8zyhKXLVLWj
```

Sample Terminal output is shown on the right.   
  


  
  
To verify that the FA address and its balance has successfully imported, run the listaddresses command to list all the addresses in your wallet.

`factom-cli listaddresses`

> Terminal output for:  
> `factom-cli listaddresses`

```text
> factom-cli listaddresses
FA1zT4aFpEvcnPqPCigB3fvGu4Q4mTXY22iiuV69DqE1pNhdF2MC 10
```

Sample Terminal output is shown on the right.   
  
  
Our FA address has a balance of 10 factoids, but your balance will likely be different.

You have successfully imported a Factoid Private Key and ready to use your balances! \(thumbs up\)

### Verify FCT and EC Balances <a id="verify-fct-and-ec-balances"></a>

After sending or receiving factoids, importing secret keys, or redeeming your 12-word master passphrase, you may want to verify your address balances. We’ve provided two easy ways to check your Factoid \(FCT\) or Entry Credit \(EC\) balances.

**1\) With the Factom Control Panel**

The Factom Control Panel is easy to use and perfect for verifying your FA or EC balances. Simply [run FF](https://docs.factom.com/cli#run-factom-federation) and open the Control Panel web page in your browser: [http://localhost:8090/](http://localhost:8090/)

Find the search bar on the upper right-hand corner of the Factom Control Panel.

![Wallet 89](https://docs.factom.com/images/wallet_074.png)

Paste the FA address you wish to verify in the search bar.

![Wallet 90](https://docs.factom.com/images/wallet_075.png)

Click GO.

![Wallet 91](https://docs.factom.com/images/wallet_076.png)

The Control Panel will display the factoid balance for the FA address under “Amount Available.” In this example, we have a balance of 2 FCT.

Repeat the steps above to verify the balance of an EC address. Paste the EC address you wish to check in the search bar.

![Wallet 92](https://docs.factom.com/images/wallet_077.png)

Click GO.

![Wallet 93](https://docs.factom.com/images/wallet_078.png)

The Control Panel will display the Entry Credit balance for the EC address under “Amount Available.” In this example, we have a balance of 20 EC.

You may also use the Control Panel to get more info about Transaction IDs, Block Numbers, Chain IDs, and more.

**2\) With the Factom Explorer**

The Factom Explorer provides information about our blockchain including FA and EC addresses, blocks, entries, and more. From here you may verify your FA or EC balances without running our software. Find the Factom Explorer at [https://explorer.factom.org](https://explorer.factom.org/).

![Wallet 94](https://docs.factom.com/images/wallet_079.png)

Paste the FA address you wish to verify in the search bar.

![Wallet 95](https://docs.factom.com/images/wallet_080.png)

Hit Enter on your keyboard.

![Wallet 97](https://docs.factom.com/images/wallet_081.png)

The Explorer will display the balance of the FA address, in this example 1.892 FCT, along with previous transactions.

Now, let’s repeat the steps above to verify the balance of an EC address.

Paste the EC address you wish to verify in the search bar.

![Wallet 97](https://docs.factom.com/images/wallet_082.png)

Hit Enter on your keyboard.

![Wallet 98](https://docs.factom.com/images/wallet_083.png)

The Explorer will display the balance of the EC address, in this example 3999 EC, along with its previous transactions.  
To run the Factom Control Panel, you need some basic command line knowledge while the Factom Explorer doesn’t require you to run any Factom apps. Choose the verification method that suits you best.

You made it this far and got the knowledge, now is time to teach others how to use Factom! \(big grin\)

### Create a Factom Chain <a id="create-a-factom-chain"></a>

To make entries in Factom, you must create a Factom Chain where your entries will be recorded. You can create as many chains as you like. Just remember, it’s a BYOEC party. You know… _bring your own entry credit party_. \(We know…what you are thinking. This is why we do Blockchains and not Standup\)

Here is how to create your first Factom Chain.

Creating a chain in Factom has a fee of 10 Entry Credits, so make sure your EC address balance can cover it.

First, [Run FF](https://docs.factom.com/cli#run-factom-federation).

In the factom-cli Terminal window run the addchain command as shown below.

`echo "my first chain" | factom-cli addchain -n {chainName} {EC_Public_Key}`  
In your case, the only differences will be the data between the quotes, the chainName, and the EC address.  
Be sure to use your EC address \(not our example\).

> Terminal output for:  
> `factom-cli addchain`

```text
> echo "my first chain" | factom-cli addchain -n chainName EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
Committing Chain Transaction ID: c1a2861d14b788c13d6c48f1e5603f5c53afc599d07d338deeb4c3d5012e24da
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entryhash: 232d1e54ecdfc369cc66e35dda73ce4beb7dffd3e75af94192034e79beaf6c8f
```

If you’d like to upload a file as the first entry of a chain, you can use a standard input to do so rather than a pipe. For example:

`factom-cli addchain -n {chainName} {EC_Public_Key} < {fileName}`

The result is the same either way. You’ll now have a newly minted chain sitting immutably on the Factom blockchain.

Sample Terminal output is shown on the right.   
  
  
Take note of the ChainID as you will need it to make Factom entries later on.

### Make a Factom Entry <a id="make-a-factom-entry"></a>

Once you have created your first Factom chain and noted the ChainID, you are ready to make your first entry! Writing an entry in Factom costs 1 Entry Credit.

First, [Run FF](https://docs.factom.com/cli#run-factom-federation).

In the factom-cli Terminal window run the addentry command as constructed below:

`echo "my first entry" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX`  
In your case, the only differences will be the name between quotes, the ChainID, and the EC address. The name of the entry can be anything you want. In our example “my first entry” is the name of the new entry.  
Our ChainID a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 should be replaced by your own.  
Finally, the EC address above should be replaced by your own, again, make sure it has enough EC balance to cover the fee.

> Terminal output for:  
> `factom-cli addentry`

```text
> echo "my first entry" | factom-cli addentry -c a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791 EC27kDNpFcJQwvdpFXaXjPqhtDSf6VK8kRN8Fv7EkhvS9tVkuAfX
Commiting Entry Transaction ID: 1d6b9d7159a27b91cd389738eb2b3b01143aaaf39ef46388f47abb8b32698811
ChainID: a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791
Entryhash: 2460e676d4f4c89ccf0608b2e3134421b9075fb956af76c02af78991e6faafdc
```

Sample Terminal output is shown on the right.   
  
  
To make additional entries, repeat these steps using the same ChainID.

You are now officially a Factom Jedi!

### Read Factom Entries <a id="read-factom-entries"></a>

To read your Factom entries, you need the ChainID you used while creating your first chain.

First, [Run FF](https://docs.factom.com/cli#run-factom-federation).

Use the get allentries command in the factom-cli Terminal window.

`factom-cli get allentries a4ab1e2ef212208b3513c5f06fcdcfa79b7c2b610526ce2dc374bb789700a791`  
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

Sample Terminal output is shown on the right.   
  
  
You may notice that there are two entries in the new chain even though you only made one. This is because every time a new chain is created, it generates an entry containing its assigned name. The second entry, \*Entry \[ 1 \]\*, is the first entry we made in the new chain, the one we named “my first entry.”

This simple guide is designed to show how chains and entries work in Factom. Refer to the factom-cli help by typing the below command for more options.

`factom-cli -h`

You can then explore other ways and more command flags you can run to make entries suited for your needs. We will also release more advanced guides in the near future. Stay tuned!

### Using Factoid Papermill <a id="using-factoid-papermill"></a>

Factoid Papermill is an app to create private and public factoid address key pairs, the equivalent to a paper wallet for Factoids.

Factoids can be managed using the command line or the GUI wallet, which is a bit prettier.

Both the command-line and GUI wallets can import private keys generated with Factoid Papermill.  
Before attempting to transact factoids read this guide fully, at least once.

The Factoid Papermill app has a different name on different platforms.

* **Mac:** factoidpapermill-mac
* **Windows:** factoidpapermill.exe
* **Linux:** factoidpapermill-linux

**Using Factoid Papermill**

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

Sample Terminal output is shown on the right.   
  


Take note of the FA Address and Private Key and keep them in a safe place. If you need more addresses and private keys repeat the process. You can use your newly generated Factoid Address to receive factoids from a third party or an exchange. This method of storing factoids is considered a “cold wallet” or “paper wallet.”  
Your New Factoid Private Key and New Factoid Address will be different than this example. Remember you won’t be able to send from your new address until you have imported it into one of your wallets.  
Failure to backup the Private Key generated by Factoid Papermill for a given Factoid Address will cause the loss of all factoids held, sent, or received by these addresses.  
If on Mac and Linux Factoid Papermill doesn’t launch because of missing execute permissions simply open a Terminal window and type:  
  
chmod +x \(with a space after the x\)   
  
Then drag and drop the app onto the Terminal window to populate its path, and click enter. You should then be able to run FactoidPapermill as described above.

## Compile Factom Federation <a id="compile-factom-federation"></a>

Quick-start guide to help you compile and run Factom Federation software.

**Requirements not covered in guide**

GoLang \(golang 1.7.4 recommended\)

**Requirements**

Glide Package Manager

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

## Factom CLI Commands <a id="factom-cli-commands"></a>

```text
factom-cli [OPTIONS] SUBCOMMAND [OPTIONS]
```

factom-cli is a command line interface program for interacting with factomd and factom-walletd.

### Flags <a id="flags"></a>

#### -f <a id="f"></a>

```text
$ echo hello | factom-cli addchain -f -n moe -n larry \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The f flag, used with the addchain, addentry, buyec, composechain, composeentry, sendfct, sendtx, and signtx subcommands, tells factom-cli to continue on with processing without waiting for acknowledgment of the success of the subcommand to be generated. This can be useful for scripts where you can execute a long string of subcommands in a fraction of the time it would take if you had to wait for an acknowledgment of each command individually.

#### -q <a id="q"></a>

```text
$ echo goodbye | factom-cli addentry -q -n moe -n larry -e curly \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The q flag specifies “quiet” execution of the addchain, addentry, addtxecoutput, addtxfee, addtxinput, addtxoutput, buyec, newtx, sendfct, sendtx, signtx, and subtxfee subcommands. This means that no output will be returned back to the user. This again can be useful for scripts where there is no need for feedback from factom-cli.

#### -e -x <a id="e-x"></a>

```text
$ factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] \
[-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>
```

The addentry subcommands support the -e and -x flags for adding external ids to the Entries they create. Multiple -e and -x flags may be used, and -e and -x may be used in combination. -e string will encode the string as binary and set it as the next external id. -x hexstring will decode the hexstring into binary and set it as the next external id.

#### -n -h <a id="n-h"></a>

```text
$ factom-cli get chainhead -n test -h 3031
```

The get firstentry, get chainhead, and get allentries subcommands support the -n and -h flags for using Chain Names as an alternative for providing a ChainID. The Chain Name is the combination of External IDs on the first Entry in the Chain.

#### -r <a id="r"></a>

```text
$ factom-cli sendfct -r $my_factoid_address factom.michaeljbeam.me
```

The r flag tells factom-cli to try and resolve a public Factoid or Entry Credit Address from a DNS name registered through Netki.

#### -C <a id="c"></a>

```text
$ echo hello | factom-cli addchain -n moe -n larry -C \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The C flag, used with the addchain subcommand, limits the subcommand output to a single field, the ChainID with no headers. This means that a variable can be assigned to the value of the executed command directly.

#### -E <a id="e"></a>

```text
$ echo goodbye | factom-cli addentry -n moe -n larry -e curly -E \
 EC2DKSYyRcNWf7RS963VFYgMExoHRYLHVeCfQ9PGPmNzwexample
```

The E flag, used with the addchain and addentry subcommands, limits the subcommand output to a single field, the Entry Hash with no headers. This means that a variable can be assigned to the value of the executed command directly.

#### -T <a id="t"></a>

```text
$ factom-cli get pendingtransactions -T
```

The T flag, used with the addchain, addentry, buyec, get pendingtransactions, listtxs address, listtxs subcommands, limits the subcommand output to a single field, the Entry Hash with no headers. This means that a variable can be assigned to the value of the executed command directly.

### Commands <a id="commands"></a>

#### status <a id="status"></a>

```text
factom-cli status TxID|FullTx
```

Returns information about a factoid transaction, or an entry / entry credit transaction

#### addchain <a id="addchain"></a>

```text
factom-cli addchain [-fq] [-n NAME1 -n NAME2 -h HEXNAME3 ] [-CET] /
ECADDRESS <STDIN>
```

Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address.

#### addentry <a id="addentry"></a>

```text
factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ...|-c CHAINID] /
 [-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>
```

Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address.

#### addtxecoutput <a id="addtxecoutput"></a>

```text
factom-cli addtxecoutput [-r] TXNAME ADDRESS AMOUNT
```

Add an Entry Credit output to a transaction in the wallet

#### addtxfee <a id="addtxfee"></a>

```text
factom-cli addtxfee TXNAME ADDRESS
```

Add the transaction fee to an input of a transaction in the wallet

#### addtxinput <a id="addtxinput"></a>

```text
factom-cli addtxinput TXNAME ADDRESS AMOUNT
```

Add a Factoid input to a transaction in the wallet

#### addtxoutput <a id="addtxoutput"></a>

```text
factom-cli addtxoutput [-r] TXNAME ADDRESS AMOUNT
```

Add a Factoid output to a transaction in the wallet

#### backupwallet <a id="backupwallet"></a>

```text
factom-cli backupwallet
```

Backup the running wallet

#### balance <a id="balance"></a>

```text
factom-cli balance [-r] ADDRESS
```

If this is an EC Address, returns the number of Entry Credits. If this is a Factoid Address, returns the Factoid balance.

#### buyec <a id="buyec"></a>

```text
factom-cli buyec FCTADDRESS ECADDRESS ECAMOUNT
```

balance Buy entry credits

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

