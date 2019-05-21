---
description: This section describes how to use the Factom explorer
---

# Usage

### Search for FCT/EC addresses <a id="search-for-fct-ec-addresses"></a>

To use Explorer to verify balances, copy and paste the FA address you wish to verify into the search bar and hit Enter.

![](../../.gitbook/assets/factom_explorer_search_bar.PNG)

The explorer displays the balance for the FA address, in this example 1.892 FCT, along with previous transactions.

![Factom explorer wallet search result](../../.gitbook/assets/factom_explorer_search_result.PNG)

Similarly, to verify the balance of an EC address, copy and paste the EC address you wish to verify in the search bar and hit Enter.

![Factom explorer EC wallet search](../../.gitbook/assets/factom_explorer_search_bar_ec.PNG)

Explorer displays the balance for the EC address, in this example 3999 EC, along with previous transactions.

![Factom explorer EC wallet search result](../../.gitbook/assets/factom_explorer_search_result_ec.PNG)

### Search for a Transaction ID <a id="search-for-a-transaction-id"></a>

When sending FCT to a third party or exchange, the transaction ID is the proof that the transaction took place and that it is unique. It is important to note and keep them for your records. To search for transaction IDs, copy and paste it into the search bar and hit Enter.

![Factom explorer - transaction ID search](../../.gitbook/assets/factom_explorer_tx_id_search.PNG)

Explorer displays [details of the transaction](http://explorer.factom.org/tx/e41ebc5be64aa06cb4cdeb8d5c14ded4ae12c2a0630aa89c2fc001c086c73bdd) such as the time it was made and Inputs and Outputs. This example shows that 100 FTC were sent from the input address to the output address, with a transaction fee of 0.006 FCT debited to the sender.

![Factom explorer - Factoid transaction result](../../.gitbook/assets/factom_explorer_factoid_tx.PNG)

### Search for a Factom Chain <a id="search-for-a-factom-chain"></a>

Once a Factom chain is created, Explorer can provide an overview of the chain and the entries made to it. The example below shows the [Gutenberg Chain](http://explorer.factom.org/chain/00511c298668bc5032a64b76f8ede6f119add1a64482c8602966152c0b936c77), containing a few thousand entries. The Chain ID is entered into the search bar.

![Factom explorer - Factom chain search](../../.gitbook/assets/factom_explorer_factom_chain.PNG)

Explorer returns the Project Gutenberg Chain with all its entries.

![Factom explorer - Project Gutenberg chain](../../.gitbook/assets/factom_explorer_factom_chain_gutenberg.PNG)

### Search for a Block ID <a id="search-for-a-block-id"></a>

Specific blocks can be pulled up by entering the Block ID \(also known as Block Height\) into the search bar. The example below shows [block 7740](http://explorer.factom.org/dblock/d89e94a62c49efe3874745dff51e17a9fcfe486085ed2319a0a49b4463d0e9df).

![Factom explorer - Block ID search](../../.gitbook/assets/factom_explorer_7740_block_search.PNG)

After hitting Enter, the Explorer will find the block and present its information.  


![Factom explorer - Block information](../../.gitbook/assets/factom_explorer_7740_block.PNG)

Searching for a block is very useful particularly to look for a Block ID that was created sometime in the past, by searching for a Block Height you can go back in time in Factom very rapidly.

{% hint style="success" %}
You are now equipped to use Factom Explorer to search the Factom Blockchain.
{% endhint %}

