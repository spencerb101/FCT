# Frequently Asked Questions \(FAQ\)

## General questions

### Why does my node need to have a fixed IP address? <a id="page_Why-does-my-node-need-to-have-a-fixed-IP-address"></a>

The requirement for a fixed IP address is not a requirement for the Factom protocol itself. It is a requirement for the Testnet authority set, so Factom engineers can do easier debugging and deployment of updates.

### What would happen if two machines with the same identity were to be on the network at the same time? <a id="page_What-would-happen-if-two-machines-with-the-same-identity-were-to-be-on-the-network-at-the-same-time"></a>

If two machines with the same identity but different IP addresses would enter the Factom network, one would kill itself to avoid causing issues.

### How come that 4 level of keys are issued when doing key generation? <a id="page_How-come-that-4-level-of-keys-are-issued-when-doing-key-generation"></a>

Having 4 levels of keys allows you to change the lower level keys while retaining the higher-level ones. If your block signing key is compromised, you can use your level 4 key to change it. If your level 4 key gets compromised you can use your level 3 key, etc.

With this scheme in place, you can cold storage your level 1 key somewhere very secure but inaccessible, your level 2 key somewhere less secure but more accessible and so on, to the point where your block singing key is available to sign every minute, however is most susceptible to being stolen.

## Technical questions

### Why does my node take so long time after boot to start progressing its block height?

In the control panel, you can see the [More Detailed Node Info Page](https://developers.factomprotocol.org/start/factomd-control-panel#the-more-detailed-node-information-page).

At the top left corner in the more detailed node information page, looking at the underscores to the right of `FNode0`, there will be a W \(Wait mode\) for 10 minutes, then an I \(Ignore mode\) for another 10 minutes.

**Wait mode** is the mode the servers stay at while booting to give the other nodes a chance to finish booting. It is collecting messages, but not sending acknowledgements.

**Ignore mode** is where the server is sending out acknowledgements and EOMs \(End Of Messages\), but is not requesting missing messages. The intent is to see only fresh messages, but it is fragile because it cannot get any messages that it had missed, which is one of the things that helps keep the network robust.

After the Wait - and Ignore modes go away, your node will request new blocks and process list items from its peers, and will catch up.

### Why can't I see the Test Credits that were just transferred to my address? <a id="page_Why-can-t-I-see-the-Test-Credits-that-were-just-transferred-to-my-address"></a>

Your node needs to be fully synced before you can see any transactions to or from your address.

### Why do I get a "No such file or directory" error when trying to run the script for publishing my new ID to the blockchain? <a id="page_Why-do-I-get-a-No-such-file-or-directory-error-when-trying-to-run-the-script-for-publishing-my-new-ID-to-the-blockchain"></a>

This error often happens because the command to generate an ID and public and private keys is missing flags at the end of the command. When you run:

```bash
docker exec factomd serveridentity full elements EsXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX -n create -f
```

Be sure to include `-n create -f`.

### Why do I get an error trying to modify my node to utilize its new identity? <a id="page_Why-do-I-get-an-error-trying-to-modify-my-node-to-utilize-its-new-identity"></a>

This can be caused by using an older pdf version of the installation instructions where it seems there is a line break in the command right after 'A-2'. This gives the error 'no such command as create.conf'. However, the command is one single line. Try running the command:

```bash
docker exec factomd bash -c "sed -i '/Node Identity Information/q' /root/.factom/m2/factomd.conf && grep Identity -A 2 create.conf >> /root/.factom/m2/factomd.conf"
```

### How come I get an error about not being able to connect to the docker when adding the configuration file? <a id="page_How-come-I-get-an-error-about-not-being-able-to-connect-to-the-docker-when-adding-the-configuration-file"></a>

When running the command to add the configuration file to the docker the error 'docker: Got permission denied while trying to connect to the Docker daemon socket...' can occur. This is because the user do not have the proper rights to use the docker program.

When setting up your docker and providing user rights by running the command:

```bash
sudo usermod -aG docker USERNAME
```

It is needed to log out of the server before the changes take effect.

### I have set my firewall as instructed, but ports that should be closed are still open. How do I fix that? <a id="page_I-have-set-my-firewall-as-instructed-but-ports-that-should-be-closed-are-still-open-How-do-I-fix-that"></a>

Docker bypasses firewall settings created using Uncomplicated Firewall \(ufw\). For people who do not use a firewall from their cloud provider, that means that all of the ports the Factom daemon might use will automatically be opened, including ports that you do not want to be exposed to the internet.

To fix that problem, we need to create a file which tells Docker not to bypass ufw settings:

```bash
sudo nano /etc/docker/daemon.json
```

In the daemon.json file insert and save:

`{ "iptables": false }`

After saving, run the following commands:

```bash
sudo service docker stop
sudo ufw reload
sudo service docker start
```

### The "invalid character 'S' looking for beginning of value" error message <a id="page_The-invalid-character-S-looking-for-beginning-of-value-error-message"></a>

This is something that comes up when there's an unhandled exception. It's becoming more rare, but any time there's code without 100% exception handling this will occasionally happen. No real solution for this except.. Trying again.

