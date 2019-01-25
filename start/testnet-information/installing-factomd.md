# Interacting with Factom blockchain

The test net can be interacted with in much the same manner as the Factom main net.

Testoids \(equivalent to Factoids\) can be transferred or converted to Test credits \(equivalent to Entry credits\), chains and entries created, information on transfers and account balances pulled and APIs interfaced.

If you are interested in interacting with the Factom Community test net, download the latest appropriate [binary release](https://github.com/FactomProject/distribution/releases). This will install the `factomd`, `factom-cli` and `factom-walletd` command line tools. Now download `factomd.conf` from the [testnet toolkit](https://github.com/FactomProject/factomd-testnet-toolkit) and place it in the appropriate folder. For Ubuntu, this will be in your home folder `~/.factom/m2`. For Windows, look in your AppData/Roaming folder.

Open a terminal window and start your local `factomd` node:

```bash
factomd -customnet=fct_community_test
```

This command will start a full factom test net node. You should allow it to sync with the network \(this can/will take hours\) before you start interacting with the blockchain. Leave this running and start a new terminal in order to interact with the daemon. Open the control panel at http://localhost:8090 to check the status, or try `factom-cli get heights`

A full list of CLI commands is available by executing:

```text
factom-cli help
```

In addition to the command line tools, you can download the enterprise wallet from [https://github.com/FactomProject/distribution\#factom-enterprise-wallet](https://github.com/FactomProject/distribution#factom-enterprise-wallet)

This is a GUI application you can install on any machine, including the one running your node. Go to Settings and uncheck `Custom Factomd Location` if you are running your node locally. If you are running your `Factomd` node on a Linux server and want to connect to it using the enterprise wallet on your Windows computer, simply check "Custom Factomd Location" on your Windows wallet and type in your server's IP-address followed by the TCP port \(8088 is the default testnet API port\), for example `192.168.105.55:8088`

### Some useful commands <a id="page_Some-useful-commands"></a>

| Task | Command | Information |
| :--- | :--- | :--- |
| Add Chain | `factom-cli addchain [-fq] [-n NAME1 -n NAME2 -h HEXNAME3] [-CET] ECADDRESS <STDIN>` | Create a new Factom Chain. Read data for the First Entry from stdin. Use the Entry Credits from the specified address. -C ChainID. -E EntryHash. -T TxID. |
| Add Entry | `factom-cli addentry [-fq] [-n NAME1 -h HEXNAME2 ... -c CHAINID] [-e EXTID1 -e EXTID2 -x HEXEXTID ...] [-CET] ECADDRESS <STDIN>` | Create a new Factom Entry. Read data for the Entry from stdin. Use the Entry Credits from the specified address. -C ChainID. -E EntryHash. -T TxID. |
| Check Balance | `factom-cli balance [-r] ADDRESS` | If this is an EC Address, returns number of Entry Credits. If this is a Factoid Address, returns the Factoid balance. |
| Convert Testoids to Test Credits | `factom-cli buyec [-fqrT] FCTADDRESS ECADDRESS ECAMOUNT` | Buy ECAMOUNT number of entry credits. -f force. -q quiet. -r Netki DNS resolve. -T TxID. |
| Export private addresses | `factom-cli exportaddresses` | List the private addresses stored in the wallet |
| Get data | `factom-cli get allentries / chainhead / dblock / eblock / entry / firstentry / head / heights / walletheight / pendingentries / pendingtransactions / raw / dbheight / abheight / fbheight / ecbheight` | Get data about Factom Chains, Entries, and Blocks |
| New TC address | `factom-cli newecaddress` | Generate a new Entry Credit Address in the wallet |
| New Testoid address | `factom-cli newfctaddress` | Generate a new Factoid Address in the wallet |
| Reciept query | `factom-cli receipt ENTRYHASH` | Returns a Receipt for a given Entry |
| Send Testoids | `factom-cli sendfct [-fqrT] FROMADDRESS TOADDRESS AMOUNT` | Send Factoids between 2 addresses. -f force. -q quiet. -r Netki DNS resolve. -T TxID. |

* 
