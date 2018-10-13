# Overview

## What is Factom

Factom is a blockchain protocol built to leverage the security and immutability of Bitcoin \(and other\) blockchains for the purpose of recording data. Factom exists as a layer above the Bitcoin blockchain, allowing for data to be committed to the blockchain continuously and in real-time, secured by the consensus mechanism of the Factom protocol itself. The Factom protocol takes this security one step further by anchoring the results of this consensus to the Bitcoin blockchain every 10 minutes using a data-efficient Merkle tree. Factom’s native tokens are called Factoids, or FCT.

Bitcoin is the largest, most secure, and most trusted distributed ledger that exists in the world today. This is a function of network value and hash power. Bitcoin leads all cryptoassets on both. Data contained in the Bitcoin blockchain is immutable and auditable in a way that was impossible before Bitcoin was created. While the majority of development within the Bitcoin ecosystem has focused on Bitcoin as a payment or value transfer mechanism, the security and immutability of the Bitcoin blockchain can be leveraged in novel ways. Outside of payments, one of the most compelling use cases for blockchain technology is the ability to record and secure arbitrary kinds of data.  


## **Why Factom and not just Bitcoin?** 

There are several reasons why enterprise clients, especially those dealing with large amounts of data, would not want to record that data directly onto the Bitcoin blockchain:

* Bitcoin’s 10-minute average block times create forced delays that slow down the securing of data \(usually up to 60 minutes per entry for full confirmation\).
* Adding data directly to the Bitcoin blockchain is expensive and the cost is unpredictable. Bitcoin network fees are denominated in Bitcoin. Therefore increases in BTC-USD prices increase the USD cost to commit data to the Bitcoin blockchain.
* The Bitcoin blockchain cannot currently support the number of transactions needed for record keeping. Bitcoin supports about 7 transactions per second \(TPS\). This is far too low for organizations that need to secure large amounts of data to the blockchain.
* With Bitcoin, the entire ledger is needed to verify individual pieces of data. This is computationally expensive. Factom allows for data to be grouped and examined at the group level, reducing the computational and storage cost for an individual organization.
* Using Bitcoin \(the currency\) has implications for enterprise users, both legally and financially. Some businesses, nonprofits, and other enterprise clients will not want to transact or hold cryptocurrencies. Not only would this present a financial risk \(due to volatility\), it may also present regulatory risk.

Factom was built to address these issues, especially when it comes to the needs to enterprise clients. Factom has its own protocol that allows for continuous time-stamping and securing of data. Because this data is compressed using merkle trees, even huge amounts of data entered into Factom chains can be secured onto the Bitcoin blockchain with a single data point. This greatly reduces both transaction costs and blockchain congestion.

In the Factom network, data is organized into specific groups, and each group can be tracked or examined individually \(although grouping is possible in Bitcoin using colored coins, verification requires the entire ledger back to the genesis block\). In Factom, users write to and read from groups that they’re interested in. This is extremely valuable to users, especially as the size of the overall data set grows. Users do not need to sift through a huge data set, most of which is irrelevant to them. They can simply identify the subset they are interested in and focus on that.Factom also utilizes an innovative dual token system that accomplishes two things. First, it provides a way for individuals to utilize the Factom protocol without having to hold or transact cryptocurrencies. This is good for businesses for both financial reasons \(due to volatility\) and regulation. Secondly, it provides USD-denominated price stability by setting a network-wide price per kilobyte of data entered. This allows for enterprise clients to better estimate costs.

