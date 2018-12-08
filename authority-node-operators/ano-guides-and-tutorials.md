# ANO Guides & Tutorials

## Getting started

[![Factom protocol: Getting started with the basics](http://img.youtube.com/vi/luJucKvHsB4/0.jpg)](https://www.youtube.com/watch?v=luJucKvHsB4)

{% hint style="info" %}
This tutorial is fully covered in the video shown above.
{% endhint %}

In this tutorial you will learn how to setup:

* A full factomd node with a wallet daemon
* Factom-cli 
* Docker

You need these to be able to get started with interacting with the Factom Blockchain. This tutorial is relevant for both mainnet and testnet and assumes that you've already setup an updated latest LTS version of Ubuntu. Minimum specifications for a node is listed below.

####  Minimum system requirements

* A modern CPU
* 16 GB RAM
* At least 50 GB storage
* 20 Mbit/s synchronous
* Up to 1TB / month data transfer
* Static IP-address

{% hint style="info" %}
The specifications are subject to change at any time as the network matures.
{% endhint %}

### Setting up a factomd node

Setting up a factomd node is very easy, download the latest release by running the following:

`wget` [`https://github.com/FactomProject/distribution/releases/download/v6.0.1/factom-amd64.deb`](https://github.com/FactomProject/distribution/releases/download/v6.0.1/factom-amd64.deb)\`\`

{% hint style="danger" %}
The version in the above command may be outdated, be sure to check what the [latest release](https://github.com/FactomProject/distribution/releases) is. 
{% endhint %}

After the download is finished, install the package:

```text
sudo dpkg -i factom-amd64.deb
```

Once installation is complete you have access to the Factom daemon, wallet daemon and the Factom CLI. 

To start the Factom daemon simply run:

```text
factomd
```

You also have access to the wallet daemon and cli tools:

```text
factom-walletd
factom-cli
```

### The Docker way

You can use the above deb package to interact with the protocol and complete the tutorial, but as an ANO your factom daemon will run within a Docker container. Install Docker by following [the official Docker guides](https://docs.docker.com/install/linux/docker-ce/ubuntu/). Make sure to allow your non-root user to use Docker:

```text
sudo usermod -aG docker <username>
```

Create the Factomd volumes:

```text
docker volume create factom_keys
docker volume create factom_database
```

Place the factomd.conf in the correct folder:

```text
wget https://raw.githubusercontent.com/FactomProject/factomd/master/factomd.conf
sudo cp factomd.conf /var/docker/volumes/factom_keys/_data/factomd.conf
```

Run Factomd in Docker:

```text
docker run -d --name "factomd" -v "factom_database:/root/.factom/m2" -v "factom_keys:/root/.factom/private" -p "8088:8088" -p "8090:8090" -p "8108:8108" -l "name=factomd" factominc/factomd:v6.0.1-alpine -startdelay=600 -faulttimeout=120 -config=/root/.factom/private/factomd.conf
```

{% hint style="danger" %}
The version in the above command may be outdated, be sure to check what the [latest release](https://github.com/FactomProject/distribution/releases) is.
{% endhint %}

### Setting up the wallet daemon

Now we want a wallet daemon running. You can easily just run factom-walletd above, but you might want to run it as a system service:

{% code-tabs %}
{% code-tabs-item title="/etc/systemd/system/factom-walletd.service" %}
```text
[Unit]
Description=Run the Factom Wallet service
Documentation=https://github.com/FactomProject/factom-walletd
After=network-online.target

[Service]
User=<username>
Group=<username>
EnvironmentFile=-/etc/default/factom-walletd
ExecStart=/usr/bin/factom-walletd $FACTOM_WALLETD_OPTS
KillMode=control-group
Restart=on-failure

[Install]
WantedBy=multi-user.target
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```text
sudo systemctl daemon-reload
sudo systemctl enable factom-walletd
sudo systemctl start factom-walletd
```

{% hint style="success" %}
Congratulations, you now have a basic Factom daemon running in a docker container. You should be able to use this to complete the rest of the tutorial.
{% endhint %}

## Generating your server identity

[![Factom protocol: Generating your server identity](http://img.youtube.com/vi/g9FzNtSB7I4/0.jpg)](https://www.youtube.com/watch?v=g9FzNtSB7I4)

{% hint style="info" %}
This tutorial is fully covered in the video shown above.
{% endhint %}

This tutorial assumes that you've setup Ubuntu that is running the _Factom Daemon_. If you haven't, please check out the _getting started with the basics_ tutorial first.

You can check if the daemon is up by running `docker ps` . A container with the image `factominc/factomd:vX.xx` should show up where `vX.xx` is your current Factomd version. 

{% hint style="info" %}
Latest version of the Factom Daemon can be found [here.](https://github.com/FactomProject/distribution/releases)
{% endhint %}

Furthermore you will need Entry Credits to create your identity to the blockchain, so make sure you have at least 24 EC in your Factom wallet before moving on with the tutorial.

Lastly, it is **highly** suggested that you have two USB flash drives ready:

* One that will be used to boot a temporary Linux to perform the operations. This USB stick will be referenced as BOOT stick in the tutorial.
* The second one will be used to store data related to the operations. This USB flash drive will be referenced as DATA stick in the tutorial. Copy this tutorial onto the DATA stick to be able to follow the instructions on the offline system as well. 

{% hint style="danger" %}
The keys generated as part of this tutorial are highly sensitive, do not EVER share any of the keys you hold or generate. Losing these keys means you will lose your server. Keep these secure and safe, preferably written down on a piece of paper.  

Thus, doing parts of this tutorial on an offline computer greatly reduces the risk of these keys being compromised by either key loggers,  screen capture software, viruses or by other malicious means.
{% endhint %}

### Building the serveridentity tool

The identity is generated using the serveridentity tool, but first you need to build said tool.

Start off by installing _git_, _golang-go_ and _golang-glide_:

```bash
sudo apt-get install git golang-go golang-glide
```

next up edit `~/.profile` with for example nano:

```bash
nano .profile
```

and add the following lines to the bottom:

{% code-tabs %}
{% code-tabs-item title=".profile" %}
```bash
export GOPATH=$HOME/go
export PATH=$PATH:$GOPATH/bin
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="warning" %}
Open a new terminal for these changes to take effect. You might even need to re-log.
{% endhint %}

Next up clone the serveridentity tool:

```bash
mkdir -p $GOPATH/src/github.com/FactomProject/
cd $GOPATH/src/github.com/FactomProject/
git clone https://github.com/FactomProject/serveridentity.git
cd serveridentity
glide install
go install
cd signwithed25519
go install
```

Now you should have two files in the `go/bin/`folder named `serveridentity` and `signedwithed25519`. These are the files you need to generate your server identity. 

Copy the files `serveridentity` and `signedwithed25519` into your USB DATA flash drive and continue the process on your offline system. 

### Creating the server identity 

For the next steps you will need some Entry Credits as you'll be storing your identities on the blockchain itself.  

{% tabs %}
{% tab title="Using the Enterprise wallet" %}
* Create a new Entry Credit address in your Address Book
* Verify that it has been funded by checking the balance in the wallet
* Click the pencil-icon on your EC wallet and click "Display Private Key", you will need this for the next step.
* If you dont have one then create a new Factoid address to set up efficiency and payouts.
{% endtab %}

{% tab title="Using the CLI wallet" %}
&lt;temp&gt;
{% endtab %}
{% endtabs %}

First, make sure the files are executable:

```bash
chmod +x serveridentity
chmod +x signwithed25519
```

Now run the following:

`./serveridentity full elements {ENTRY_CREDIT_PRIVATE_KEY} -n={OPTIONAL_FILENAME}`

This will generate numerous keys which are printed to stdout, two files will also be produced:

* Script to add the Identity to the blockchain
  * Script that utilizes factom-cli
  * Name of script is by default `fullidentity.sh` or `{OPTIONAL_FILENAME}.sh` if provided.
* Config file needed for the server
  * Place in `~/factom/m2` and rename to `factomd.conf`
  * Name of config is by default `fullidentity.conf` or `{OPTIONAL_FILENAME}.conf` if provided

Write down the keys that are printed in stdout and copy the two new files to the DATA stick, eject it and shut down and destroy the Ubuntu session. Continue the tutorial on your server again.

### Importing your server identity

Copy your fullidentity.sh file to your server, make it executable and run it. Make sure `signedwithed25519` is available on the sytem.

```text
factom-cli importaddress {ENTRY_CREDIT_PRIVATE_KEY}
chmod +x fullidentity.sh
./fullidentity.sh
```

Your server identity chain is now generated. You can now paste the contents of the important.conf file into your factomd.conf, normally located at /var/docker/volumes/factom\_keys/\_data/factomd.conf 

## Setting the coinbase address and node efficiency

[![Factom protocol: Setting the coinbase address and node efficiency](http://img.youtube.com/vi/Q9AXt0UHoHM/0.jpg)](https://www.youtube.com/watch?v=Q9AXt0UHoHM)

{% hint style="info" %}
This tutorial is fully covered in the video shown above.
{% endhint %}

This tutorial will guide you through the process of setting your coinbase address and node efficiency. If you've followed the previous tutorials you should have a system with Factomd running as well as a wallet with some Entry Credits in it. 

### Requirements

First off you will need two USB flash drives ready. 

* One that will be used to boot a temporary Linux to perform the operations. This USB stick will be referenced as BOOT stick in the tutorial.
* The second one will be used to store data related to the operations. This USB flash drive will be referenced as DATA stick in the tutorial. Copy this tutorial onto the DATA stick to be able to follow the instructions on the offline system as well. 

Additionally, you will need your Factom identity information ready:

* Your identity root chain ID \(starts with `888888`\)
  * You will find this in the important.conf file you made when generating your server identity 
* Your server management subchain ID \(starts with `888888`\)
* Your secret level 1 identity key \(starts with `SK1` \)

The value of the server management subchain ID can be found by looking at the identity root chain ID in a Factom explorer: it is the value of the 3rd external id of the entry whose 2nd external id is equal to 'Register Server Management'.

You will also need a valid main-net Entry Credit address funded with ECs \(maybe a hundred to be safe\). Write down the corresponding private EC address \(that starts with `Es`\) or you can store it on the DATA stick. You also need a main-net public Factoid address \(that starts with `FA` \) that will be used as the receiving coinbase address.

### The steps

First create the Ubuntu 18.04 bootable BOOT stick. Google "create Ubuntu 18.04 bootable USB flash drive" if you're unsure how to.

Then, boot Ubuntu 18.04 from the BOOT stick and connect to the internet.

Open a terminal and run the following commands \(this will install node.js 10 and the factom-identity CLI\):

```bash
sudo apt-get update
sudo apt install -y git curl
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install -y nodejs
git clone https://github.com/PaulBernier/factom-identity-cli.git
cd factom-identity-cli
npm install
```

Now turn **off** the internet connection. From now on your Ubuntu should _never_ get connected to the Internet. You can double check by typing `ping 8.8.8.8`, or you can unplug your wifi/Ethernet if you really want to be sure.

Proceed by generating the update scripts by running the following in a terminal:

**Updating the coinbase address**:

```
# Parameters: <Identity root chain ID> <FCT public address> <SK1 private key> <Paying private EC address>
# Example:
node bin/factom-identity-cli update-coinbase-address --offline -s courtesy-node.factom.com:80 8888889822cf1d5889aa8dc11ad210b67d582812152de568fabc5f8505989c0f FA3HZDE4MdXAthauFoA3aKYpx33U4fT2kAABmfwk7NBqyLT2zed5 sk12tdaziBoFyBHG56Ery3bPFFBDpy7Y3VymduGPfoj66cGhH4mHZrw Es3ytEKt6t5Jm9juC4kR7EgKQSX8BpRnM4WADtgFoq7j1WgbeEGW
```

{% hint style="danger" %}
Be sure to replace the parameters in the command above with your own:

* Identity root chain ID
* FCT public address
* SK1 private key
* Paying private EC address
{% endhint %}

**Updating the node efficiency**:

```bash
# Parameters: <Identity root chain ID> <Efficiency> <SK1 private key> <Paying private EC address> <Server Management Subchain ID>
# Example:
node bin/factom-identity-cli update-efficiency --offline -s courtesy-node.factom.com:80 8888889822cf1d5889aa8dc11ad210b67d582812152de568fabc5f8505989c0f 50.1 sk12tdaziBoFyBHG56Ery3bPFFBDpy7Y3VymduGPfoj66cGhH4mHZrw Es3ytEKt6t5Jm9juC4kR7EgKQSX8BpRnM4WADtgFoq7j1WgbeEGW 8888887c01c12c72052f9c99b45782013feadb20c46ca86dc6e3a9730835848a
```

{% hint style="danger" %}
Be sure to replace the parameters in the command above with your own:

* Identity root chain ID
* Efficiency
* SK1 private key
* Paying private EC address
* Server Management Subchain ID
{% endhint %}

Those two commands will create two scripts if successful:

* `update-coinbase-address.sh`
* `update-efficiency.sh`

Copy these scripts to your DATA stick, eject it and shut down and destroy the Ubuntu session. 

{% hint style="danger" %}
 **Important:** the scripts generated contain timestamped data which means they have a limited time of validity. You must execute the scripts **within 1 hour** of their creation to be certain that the entries contained in them will be accepted by the network.
{% endhint %}

Continue now on the previous system you were working on and plugin the DATA stick. Locate the files and make sure they are executable:

```bash
chmod +x update-coinbase-address.sh
chmod +x update-efficiency.sh
```

Now execute both bash scripts. 

```bash
./update-coinbase-address.sh
./update-efficiency.sh
```

The scripts simply use `curl` command lines that should be available on most unix based systems. The scripts will make the requests to the Factom Inc. courtesy node \(`courtesy-node.factom.com:80`\). 

{% hint style="info" %}
You can edit the scripts to choose another endpoint by changing the  `HOST=` parameter at the top to localhost or a test-net node for instance.
{% endhint %}

After executing, the scripts should output success messages if done correctly. You can check in an explorer that your identity root chain and server management subchain have been updated after 10 minutes \(next block\).

Finally, format the boot stick, or even better, do a secure erase with specialized tools. 

## Joining the docker swarm

[![Factom protocol: Choose VPS and join the Docker Swarm](http://img.youtube.com/vi/Qghv05RCMcE/0.jpg)](https://www.youtube.com/watch?v=Qghv05RCMcE)

{% hint style="info" %}
This tutorial is fully covered in the video shown above.
{% endhint %}

### Installing docker

First you need to install docker. Please follow the instructions [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/) to install docker-CE \(Community Edition\) to your system. Once it's installed run the following:

```bash
usermod -aG docker $USER
```

{% hint style="warning" %}
Make sure you logout / login again, as otherwise your current terminal session will not be updated.
{% endhint %}

### Storing the docker swarm certificate and key

Make sure you store the docker swarm main-net key and certificate on your system. The files can be found here. 

{% hint style="info" %}
If you're trying to join the test-net swarm the keys can be found [here](https://github.com/FactomProject/factomd-testnet-toolkit/tree/master/tls).
{% endhint %}

You can store these files in the directory /etc/docker for instance: 

```bash
sudo mkdir -p /etc/docker
sudo wget https://raw.githubusercontent.com/FactomProject/factomd-authority-toolkit/master/tls/cert.pem -O /etc/docker/factom-mainnet-cert.pem
sudo wget https://raw.githubusercontent.com/FactomProject/factomd-authority-toolkit/master/tls/key.pem -O /etc/docker/factom-mainnet-key.pem
sudo chmod 644 /etc/docker/factom-mainnet-cert.pem
sudo chmod 440 /etc/docker/factom-mainnet-key.pem
sudo chgrp docker /etc/docker/*.pem
```

Now you should  have the files with the correct permissions set.

{% hint style="warning" %}
**Please note** that in the rest of this tutorial it's assumed you stored the files using the `/etc/docker` location and with the above names. If not, please adjust the commands below involving the certificate and keys.
{% endhint %}

### Configuring and running the docker engine

Configure the docker daemon using a default config file, located at `/etc/docker/daemon.json` . Create this file if it does'nt exist. Copy the following into the file:

{% code-tabs %}
{% code-tabs-item title="/etc/docker/daemon.json" %}
```bash
{
  "tls": true,
  "tlscert": "/etc/docker/factom-mainnet-cert.pem",

  "tlskey": "/etc/docker/factom-mainnet-key.pem",
  "hosts": ["tcp://0.0.0.0:2376", "unix:///var/run/docker.sock"]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
If your system has multiple IP addresses you can select which IP it should listen on by editing `"hosts".` 
{% endhint %}

Now you'll need to replace the standard docker start command. Run the following command:

```bash
sudo systemctl edit docker.service
```

 The above command creates an override directory at `/etc/systemd/system/docker.service.d/` and an override file called `override.conf` \(which is open on your terminal now\).  Copy and paste the following:

{% code-tabs %}
{% code-tabs-item title="override.conf" %}
```bash
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Exit and save the file. Now reload the docker configuration and the `docker.service`:

```bash
sudo systemctl daemon-reload
```

Docker should now be configured and ready. You can test if it runs correctly with the following:

```bash
sudo systemctl restart docker
sudo systemctl status docker
```

It should restart with no errors appearing and you should see that the `override.conf` file has been loaded. 

### Creating the Factomd volumes

Factomd relies on two volumes, `factom_database` and `factom_keys`. Please create these before joining the swarm:

```bash
docker volume create factom_database
docker volume create factom_keys
```

These volumes are there to make sure that you can remove or delete the container itself but the database and the keys are still persistent on the system.

For running a main-net authority node we strongly recommend syncing the database from scratch. If you do already have a recently synced main-net node and would like to avoid re-syncing, run:

```bash
sudo cp -r <path to your database> /var/lib/docker/volumes/factom_database/_data .
```

The directory in \_data after the copy should be main-database, as the volume is mounted at `$HOME/.factom/m2`.

### Joining the docker swarm

Finally, to join the swarm, run the following command:

```bash
docker swarm join --token SWMTKN-1-5ct5plmbn1ombbjqp8ql8hq93jkof6246suzast5n1gfwa083b-1ui6w6fupe45tizz0tv6syzrs 52.48.130.243:2377
```

{% hint style="info" %}
As a reminder, joining as a worker means you have no ability to control containers on another node.
{% endhint %}

Once you have joined the network, you will be issued a control panel login by a Factom employee after messaging one of the Factom engineers on discord. You should private message the following for each node:

* NodeID \(found by running `docker info` \)
* IP address 
* Docker engine listening port \(2376\)

{% hint style="danger" %}
Only accept logins at federation.factomd.com. Any other login endpoints are fraudulent and not to be trusted.
{% endhint %}

### Starting Factomd Container from the Docker CLI

{% hint style="warning" %}
**Please note**: There is a version for the Factom software in the next command. Make sure you run the correct and latest announced version from the Discord \#operators-announcement channel
{% endhint %}

Run the following command _exactly:_

`docker run -d --name "factomd" -v "factom_database:/root/.factom/m2" -v "factom_keys:/root/.factom/private" -p "8088:8088" -p "8090:8090" -p "8108:8108" -l "name=factomd" factominc/factomd:v6.0.1-alpine -startdelay=600 -faulttimeout=120 -config=/root/.factom/private/factomd.conf`

{% hint style="info" %}
If you want the Factomd container to start at system boot \(reboots\) you can add the following parameter to the command above:

`--restart unless-stopped`
{% endhint %}

After this your node will be started. You can check for the existence of a Factom container using the command `docker ps` . 

You're now almost ready to be included in the main-net. Stop the Factomd container with `docker stop factomd` and download the factomd.conf file [here](https://raw.githubusercontent.com/FactomProject/factomd/master/factomd.conf). 

There are some required edits that are needed, among them you're required to enter a few special peers here. You will get more information about this if you're accepted as an ANO.

In the `important.conf` file generated earlier you'll find the following three lines:

```bash
IdentityChainID
LocalServerPrivKey
LocalServerPublicKey
```

Paste these into the `factomd.conf` and save. Now place the config file in `/var/lib/docker/volumes/factom_keys/_data`  by running \(if the file is where you're currently at\):  
  
`sudo mv factomd.conf /var/lib/docker/volumes/factom_keys/_data/factomd.conf`

Now you're free to start the `factomd` container again with `docker start factomd` . 

If you check the currently running docker containers you'll see a container named `factominc/filebeat:m3-debug` , this is generally a good sign as it means the portainer system has successfully connected and started a container remotely. 

{% hint style="warning" %}
Please wait for your node to be fully synced by checking the control panel node sync statuses to be 100% before performing any next steps. Please also regard the initial wait period of 20 minutes before doing anything with your node. Also note that the `factomd:v6.0.1-alpine` version may have changed since the time of writing.
{% endhint %}

## Securing your node with SSH and iptables

[![Factom protocol: Securing your node with SSH and iptables](http://img.youtube.com/vi/VIr9OT7ZRp0/0.jpg)](https://www.youtube.com/watch?v=VIr9OT7ZRp0)

{% hint style="info" %}
This tutorial is fully covered in the video shown above.
{% endhint %}

Now it's time to secure your node by hardening SSH access and setting up the firewall. This tutorial covers what is considered minimum level of security for your node, or any production server in general \(subjective opinion\). 

### SSH key-pair based login

First off you should be using a SSH key-pair when you log into your node. Go ahead and make a folder called ssh:

`mkdir .ssh`

Create a file named `authorized_keys`

`nano .ssh/autorized_keys`

Now generate a public key, with for example PuTTY Key generator, and paste it into the `authorized_keys` file. 

{% hint style="info" %}
For added security you can limit the SSH access by IP as well, preferably you'll be managing your node from only one IP address. Instead of pasting your key into the file do the following:

`from="YOUR_IP" SSH-KEY`
{% endhint %}

Once you have your keys setup continue with editing the SSH config file.

```text
nano /etc/ssh/sshd_config
```

Recommended changes are:

* `AddressFamily` set to `inet` , this will prevent your node from listening on IPv6.
* `PermitRootLogin` set to `no`. Self-explanatory, denies root login.
* `PasswordAuthentication` set to `no` , once you have setup key-based login you won't be login in with username/password. 

### Setting up the firewall with iptables

All docker swarm communications occur over TLS using a self-signed TLS certificate. Due to the way iptables and docker work you can't use the `INPUT` chain to block access to apps running in a docker container as it's not a local destination but a `FORWARD` one. By default when you map a port into a docker container it opens up to `any` host. To restrict access we need to add our rules in the `DOCKER-USER` chain. More info can be found [here](https://docs.docker.com/network/iptables/). 

Open TCP port `2376` _only to_ `52.48.130.243` & `18.203.51.247` for secure Docker engine communication. This port is required for Docker Machine to work. Docker Machine is used to orchestrate Docker hosts, as this is a local service we use the `INPUT`chain.

In addition, the following ports must be opened for `factomd` to function which we add to the `DOCKER-USER` chain:

* `2222` to `52.48.130.243` & `18.203.51.247`, which is the SSH port used by the `ssh` container
* `8088` to `52.48.130.243` & `18.203.51.247`, the `factomd` API port
* `8090` to `52.48.130.243` & `18.203.51.247`, the `factomd` Control panel
* `8108` to the world, the `factomd` main-net port

In the above video, we changed the INPUT policy to drop and included a management IP, this would create the basic ruleset:

```bash
sudo iptables -A INPUT -s 52.48.130.243/32 -p tcp -m tcp --dport 2376 -j ACCEPT
sudo iptables -A INPUT -s 18.203.51.247/32 -p tcp -m tcp --dport 2376 -j ACCEPT
sudo iptables -A INPUT -s <management-ip>/32 -p tcp -m tcp --dport 22 -j ACCEPT
sudo iptables -A INPUT -i lo -j ACCEPT
sudo iptables -P INPUT DROP

sudo iptables -F DOCKER-USER
sudo iptables -A DOCKER-USER -p tcp -m tcp --dport 8108 -j ACCEPT
sudo iptables -A DOCKER-USER -s <management-ip>/32 -j ACCEPT
sudo iptables -A DOCKER-USER -s 52.48.130.243/32 -p tcp -m tcp --dport 8090 -j ACCEPT
sudo iptables -A DOCKER-USER -s 52.48.130.243/32 -p tcp -m tcp --dport 2222 -j ACCEPT
sudo iptables -A DOCKER-USER -s 52.48.130.243/32 -p tcp -m tcp --dport 8088 -j ACCEPT
sudo iptables -A DOCKER-USER -s 18.203.51.247/32 -p tcp -m tcp --dport 8090 -j ACCEPT
sudo iptables -A DOCKER-USER -s 18.203.51.247/32 -p tcp -m tcp --dport 2222 -j ACCEPT
sudo iptables -A DOCKER-USER -s 18.203.51.247/32 -p tcp -m tcp --dport 8088 -j ACCEPT
sudo iptables -A DOCKER-USER -p tcp -m tcp --dport 8090 -j DROP
sudo iptables -A DOCKER-USER -p tcp -m tcp --dport 2222 -j DROP
sudo iptables -A DOCKER-USER -p tcp -m tcp --dport 8088 -j DROP
sudo iptables -A DOCKER-USER -j RETURN
```

Last, but not least don't forget to [**save the rules**](https://www.digitalocean.com/community/tutorials/iptables-essentials-common-firewall-rules-and-commands#saving-rules).

## Updating and brainswapping your node

[![Factom protocol: Updating and brainswapping your node](http://img.youtube.com/vi/od1P_QXk91M/0.jpg)](http://www.youtube.com/watch?v=od1P_QXk91M)

{% hint style="info" %}
This tutorial is fully covered in the video shown above.
{% endhint %}

### What is a brainswap

Brainswappingis the idea of having two nodes switch identities at the same time. We call it "brainswapping" because a node's identity dictates how it behaves.

It was implemented as a way to update the network without having to bring it down, as federated servers can "brainswap" with standby nodes that have already been updated with the new code.

The network will not perceive this as a node going offline, as the identity \(and thus the associated federated server\) is still online.

After transferring the Authority identity the node operator can now shutdown their original node, perform necessary updates, bring it back online and finally brainswap the identity back into the original server.

The procedure can also be used for migrating the Authority identity to a new physical server, by not performing the brainswap a second time to reverse the first swap .

### Updating your node

First check if your node is running the latest version. This can be done by comparing your nodes version with the latest found here, usually at the top. If your follower is not running the latest version, you can proceed by stopping and removing the current `factomd` docker container.

```text
docker stop factomd
docker rm factomd
```

{% hint style="info" %}
Dont worry, this will not delete or remove the synchronised database.
{% endhint %}



This is also a good time to update and reboot the system if you have any pending updates or reboots. To update simply run the following commands.

```text
sudo apt-get update
sudo apt-get upgrade
```

Now, run the following command exactly:

```text
docker run -d --name "factomd" -v "factom_database:/root/.factom/m2" -v "factom_keys:/root/.factom/private" -p "8088:8088" -p "8090:8090" -p "8108:8108" -l "name=factomd" factominc/factomd:v6.1.0-alpine -startdelay=600 -faulttimeout=120 -config=/root/.factom/private/factomd.conf
```

{% hint style="info" %}
If you're updating or brainswapping a node on the testnet you need to add the following parameters to the command above, before `startdelay=600`:

```text
-broadcastnum=16 -network=CUSTOM -customnet=fct_community_test
```
{% endhint %}

After this your node will be started. You can check for the existence of a factom container using the command `docker ps`.

{% hint style="warning" %}
Please wait for your node to be fully synced by checking the control panel node sync statuses to be 100% before performing any next steps. Please also regard the initial wait period of 20 minutes before doing anything with your node. Furthermore, note that the `factomd:v6.1.0-alpine` version may have changed since the time of writing.
{% endhint %}

### Preparing the brain swap

{% hint style="info" %}
For experienced and seasoned brain swappers there's an automated brain swap script made by Stamp-IT found [here](https://github.com/Stamp-IT-io/brainswap). **Do not try this, if this is the first time you're doing a brainswap**.
{% endhint %}

To perform the brain swap you will need one standby node that is ready. The standby node should be running the most recent Factomd software version if you've completed the previous steps.

#### Definitions

* **Federated Node** is the node that holds your authority identity, and needs to be updated. 
* **Standby Node** is a follower node on the network that you control.

#### Determining if you Standby Node is ready

If your standby node is not in sync with the network, performing the brainswap will result in your authority server going offline and likely to be demoted, so it is crucial to first check the health of the standby node.

* Check if the `DBHeight` matches that of the network.
  * This is done by comparing `DBHeight` in your control panel \(localhost:8090\) with the `DBHeight` of your federated server.
* Check if the minutes are following that of the network.
  * This is done by comparing the control panel of the Stanby node to that of the Federated. On the summary tab of the more Detailed Node Information you will see something similar to this:

    ```text
      ===SummaryStart===
     FNode04[f0b7e3] L___vm01  0/ 0  0.0%  0.000 165[e0b9f8] 163/166/167  7/ 7 0/0/0/0 43400/0/0/0    0 0 2/40/100 0/0/0 0.07/0.00 0/0 - 309415
    ```

      The `7/7` means you are on minute 7. You will want to make sure this number is the same on the Standby `(_/7)` and the Federated `(7/7)`
* Check the process list for , that indicates some network instability. 
  * Process list is located in the control panel \(localhost:8090\) -&gt; "more detailed node information". If any entries show you should not move on with the brainswap.

Once you've confirmed that the standby node is ready, it's time to start the swap process.

### Performing the Brain Swap

{% hint style="danger" %}
If you haven't done a brain swap before, it is highly recommended that you read through this tutorial and watch the complete video before proceeding with the actual process.
{% endhint %}

The swap requires both config files \(located on Federated Node and Standby Node\) to be modified.

Open both config files in parallel in a text editor of your choice. The config files are located at `/var/lib/docker/volumes/factom_keys/_data`. Some examples with vim and nano: 

**vim:** `vi /var/lib/docker/volumes/factom_keys/_data/factomd.conf` 

**nano:** `nano /var/lib/docker/volumes/factom_keys/_data/factomd.conf`

Swap the following lines in the two config files:

```text
IdentityChainID         = FA1E000000000000000000000000000000000000000000000000000000000000
LocalServerPrivKey      = 4c38c72fc5cdad68f13b74674d3ffb1f3d63a112710868c9b08946553448d26d
LocalServerPublicKey    = cc1985cdfae4e32b5a454dfda8ce5e1361558482684f3367649c3ad852c8e31a
```

{% hint style="info" %}
If you prefer to do a brain-transfer instead of a swap, you can just comment out the lines in your Federated node by placing a `;` in front of these lines.
{% endhint %}

Then add an additional line: `ChangeAcksHeight = 0`

This additional line is the brainswap logic. You will want to set the `ChangeAcksHeight` to some block height in the future \(remember the block height on the control panel is the last saved height, not the current working height!\).

**The safe height is the one you see in the control panel + 4**. \(localhost:8090\). If you know how to read the more detailed page, you can get away with a closer number.

Once you set the `ChangeAcksHeight` to `DBHeight+4`, save both files.

At the block height `ChangeAcksHeight` you should see both nodes change identities. If none of your nodes crash, and the identities change, the swap was successful.

