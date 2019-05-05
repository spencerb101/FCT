# Before you begin

## Introduction

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

## Backup Your Wallet File!

#### **If you’ve used Factom Genesis \(FG\)**

Our previous software release, you should have a local wallet file. We highly recommend you backup your \(FG\) wallet file every time you import or generate a new address. Do read this guide fully, at least once.

#### **If you have never run Factom Genesis \(FG\)**

You can skip the backup right now, but we strongly recommend backing up your new FF wallet once you get FF running.

Get back to this guide when you are ready to do your backup, don’t forget!  
Factom Federation \(FF\) introduced a new way to generate addresses compared to our FG release. Simply put, it generates all new addresses from a seed. The seed is a 12-word passphrase which allows you to recover all your addresses, created with the seed in question, at a later date even if you lose your wallet file. There are many reasons why you may have misplaced your original wallet file such as because you changed computer, your hard drive failed, have overwritten the wallet file by mistake, and so on.  
  
The seed comes to the rescue because if you ever lose your wallet file, you can always re-generate your addresses from it. However, some of you may have imported a Private Key generated with the Factoid Papermill app, or have imported a 12-word Koinify passphrase, or generated addresses with our previous FG wallet, these types of addresses are called “External Addresses.” Please remember that a seed file will only allow you to recover addresses that were created with the same seed, external addresses will not be recovered.  
  
So how to recover External Addresses?  
The simple way: if you have any balances on addresses not generated from your wallet seed, you may want to transfer them to an address generated from your seed.  
The easy way: keep a backup of your wallet file, whatever addresses are in there will always be, no need to recover them.   
The alternative way: make sure to keep your external addresses’ Private Keys safe, write them down or copy/paste them to a file, you can always import them even if you create a new wallet.  
  
Keep this in mind especially if you are migrating from our FG wallet to our FF wallet. If you are not careful, you may lose access to your Factoids and Entry Credits!

### **Backup your Factom Genesis \(FG\) wallet file**

Make sure to backup your FG wallet file before you run the new Factom Federation software. The wallet file is called “factoid\_wallet\_bolt.db” and is located in the .factom folder at the following locations:

* **Mac** `/Users/YourUsername/.factom/factoid_wallet_bolt.db`
* **Windows** `C:\Users\YourUsername\.factom\factoid_wallet_bolt.db`
* **Linux** `~/.factom/factoid_wallet_bolt.db`

  
Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for “how to show hidden files and folders on YOUR OS”, replacing YOUR OS with Mac or Linux accordingly.

**To backup** your FG wallet file, locate the factoid\_wallet\_bolt.db file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.  
By having a backup somewhere safe, if something goes wrong, you can always try again, but most importantly, you’ll be able to import all your FG addresses and their balances into your new FF wallet the first time you run FF. We will explain to you how to do that when “we cross that bridge” in the Run Factom Federation guide.

### **Backup your Factom Federation \(FF\) wallet file**

The wallet file is called “factom\_wallet.db” and is located in the .factom folder at the following locations:

* **Mac** `/Users/YourUsername/.factom/wallet/factom_wallet.db`
* **Windows** `C:\Users\YourUsername\.factom\wallet\factom_wallet.db`
* **Linux** `~/.factom/wallet/factom_wallet.db`

Note that the .factom folder is a hidden folder on Mac and Linux so perform a Google search for “how to show hidden files and folders on YOUR OS,” replacing YOUR OS with Mac or Linux accordingly.

**To backup** your FF wallet file, quit factomd and factom-walletd, locate the factom\_wallet.db file, make a copy, and save it to a location outside the .factom folder such as your documents folder, an external drive, a USB stick, or cloud storage.

**To create a fresh** FF wallet file, quit factomd and factom-walletd then move your wallet file to a safe location out of the .factom folder. There should be no wallet file in the .factom folder. Restart factomd and factom-walletd and a new empty wallet will be generated.

**To restore** a previous FF wallet file backup, quit factomd and factom-walletd, make sure you have a backup of the current wallet first, then drag & drop the previous backup in the .factom folder, overwrite if needed. Restart factomd and factom-walletd and your previous wallet will now be used instead.  
Pay attention when performing backups and restores. Each wallet file has its unique seed and addresses. Overwriting a wallet may result in losing all your Factoids and Entry Credits. Not cool.

