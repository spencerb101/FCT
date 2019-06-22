---
description: Restore your Factom Enterprise Wallet using a backup seed.
---

# Restore From a Backup Seed

Restoring your backed up wallet is just a matter of plugging in your seed phrases. To recall a wallet using this method do the following:

1. Go to the settings page found on the sidebar.
2. Scroll down and you'll see a section named _RESTORE A SEED_ with an orange "_RESTORE SEED_" button, click it.
3. Enter the seed phrase of the wallet you want to restore. If done properly, your seed will change to the one you've entered.
4. Now you need to regenerate your addresses:
   1. Head over to your address book and create a new address by clicking the yellow **+** button at the bottom right.
   2. Add a nickname to your address and click "_ADD TO ADDRESS BOOK_", leave the rest of the options on their defaults.
   3. Do the step above \(2.\) for each missing address.

{% hint style="info" %}
Addresses are generated deterministically from your seed, so each time you create a new address, it is simply regenerating your old addresses.
{% endhint %}

