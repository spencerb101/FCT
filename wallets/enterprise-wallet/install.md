---
description: Installation instructions for the Factom Enterprise Wallet
---

# Install

{% tabs %}
{% tab title="Windows" %}
### [Enterprise-wallet.exe](https://github.com/FactomProject/distribution/releases/download/v0.4.2.11/enterprise-wallet-setup-amd64.exe)

sha256sum: 6b6248da07a3a3d7a60480f99013b0e35f09a3ace484569bb24f44730d61ff70
{% endtab %}

{% tab title="Mac" %}
### [Enterprise-wallet.dmg](https://github.com/FactomProject/distribution/releases/download/v0.4.2.11/enterprise-wallet-setup.dmg)

sha256sum: 4af4a6ded4a74e8e38e194d9648248314d8671ed381e35f0e969b87625f1d601
{% endtab %}

{% tab title="Ubuntu/Debian" %}
### [Enterprise-wallet.deb](https://github.com/FactomProject/distribution/releases/download/v0.4.2.11/enterprise-wallet-setup-amd64.deb)

sha256sum: 22c7bce469e5f2d1051a4d9c6ad5d94cf2b79ce3f7cf6073f7e971fb692b44e5
{% endtab %}

{% tab title="Redhat/Centos" %}
### [Enterprise-wallet.zip](https://github.com/FactomProject/distribution/releases/download/v0.4.2.11/enterprise-wallet-linux.zip)

sha256sum: ce0ab4bf4d446bf5a3c5b0b25d68719d6dffa1005ad31781a0da3719c088111f
{% endtab %}
{% endtabs %}

1. Download and install the latest version for your operating system above. If you prefer, you can install the wallet directly from [Github](https://github.com/FactomProject/distribution#factom-enterprise-wallet).
2. Once installed, open the wallet and review the license agreement. 
3. Next, choose your wallet type. A 'Secure' wallet will encrypt your keys when at rest. This is probably the right option for most people. If you select 'Not Secure', jump to step 5.
4. Read the warnings then input a wallet password. Be careful, if you lose this password and do not have your seed backed up \(see[ Backup-Wallet](https://developers.factomprotocol.org/wallets/enterprise-wallet/backup-wallet) for more information\), then you will permanently lose your keys. 
5. The wallet will now begin syncing. You can still [create addresses](https://developers.factomprotocol.org/wallets/enterprise-wallet/create-fct-address) and [receive FCT](https://developers.factomprotocol.org/wallets/enterprise-wallet/send-and-receive-fct#receiving-factoids) whilst this is happening, but your balances will remain at 0 until the sync has reached 100%.

