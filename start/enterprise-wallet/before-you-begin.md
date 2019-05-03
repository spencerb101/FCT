# Before you begin

Before attempting to transact factoids \(FCT\) read these guides thoroughly \(at least once\). The software is still in Beta, so use the instructions at your risk. Do not use a lot of Factoids in case there are issues, bugs, or you mistype a command. Phoning a friend after the damage is done will not fix things. Sorry, this is just the way of the Blockchain.

The following directions and commands are optimized for Linux but should work with minor modifications for Mac or Windows. Be aware of slight differences in commands on different platforms:

**Mac**

`./factomd < rest of the command >`

**Windows**

`factomd < rest of the command >`

**Linux**

`factomd < rest of the command >`

Make sure to change the commands accordingly.

The interface you will be using to run Factom Federation software related commands is called:

* “Terminal” on the Mac and Linux
* “CMD Prompt” or “Windows Power Shell” on Windows

Give it a try and get familiar before you go any further. Going forward we will use “Terminal” to describe the interface where you type commands, just don’t forget it has a different name in Windows.

FF is composed of three main components:

* factomd
* factom-walletd
* factom-cli

However, to run the wallet you only need the new desktop app \(Enterprise Wallet\) if used online or the app + factomd if running locally, factom-walletd and factom-cli are only required if you want to run the command line wallet.

{% hint style="warning" %}
Do not run Factom Federation while connected to an unsafe network, like at a cafe, an airport, public wifi hotspot, etc. The wallet is not encrypted, and hackers could potentially steal your precious Factoids. You do not want to feel like Gollum without his ring.
{% endhint %}

