# Voting Protocols

The Factom Voting Protocols are basic protocols for named \(i.e. not anonymous\) voting using Factom chains that can be used for conducting publicly verifiable polls in any organization, such as a department inside a company, an online community or, more generally, any group of decentralized entities which want to come to a decision on a given topic.  
  
The voting protocol is separated into three main phases: vote initiation, vote commitment and vote reveal.  


During initiation, the vote initiator creates a list of eligible voters and stores it on-chain. They also \(optionally\) produce a description of the vote proposal in a document stored off-chain. Finally, they create a vote proposal entry on-chain, which contains the terms of the poll. The off-line document contains a \(longer\) description of the poll and together with the on-chain entry the two form a holistic view of the proposed vote.  


During the commitment phase, the participants can record a coded version of their vote on-chain and during the reveal phase they record the plaintext of their vote. Such commit-reveal schemes are common for on-chain voting as they solve the problem of information asymmetry for voters: having voters record their vote in plaintext would mean people voting later already have access to the running tally.

[Full Specifications](https://docs.google.com/document/d/137gw8JTqKZdfe-AF0e02pFgyLsPCTjYbX0mguC_N3GE/edit#heading=h.tjh7in888zn)

[Javascript Implementation](https://github.com/PaulBernier/factom-vote)



