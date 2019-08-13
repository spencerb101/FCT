# Common Tasks

## Generate a Factoid Address

To get started, [Run FF](run-factom-federation.md).

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

To proceed, [Run FF](run-factom-federation.md).

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

[Run FF](run-factom-federation.md) \(Yes, we know it’s growing on you\)

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

[Run FF](run-factom-federation.md).

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

[Run FF](run-factom-federation.md).

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

First, [Run FF](run-factom-federation.md).

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

First, [Run FF](run-factom-federation.md).

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

First, [Run FF](run-factom-federation.md).

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

First, [Run FF](run-factom-federation.md).

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

