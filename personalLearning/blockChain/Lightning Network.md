The easiest way to think of the lightning network is as if it's a "tab", in which the owance of that tab is through a network of users.
The network allows the creation of "channels" between *pairs* of users, to which the users can create transactions *off* the blockchain, and then close that channel to "settle" the tab/balance on the blockchain. 

It's a condensed form of creating blockchain entries, because only the opening and closing of payments is recorded on the blockchain, to which the closing means that the final transaction is settled, and that single transaction is the result of many smaller transactions. 
> This is in contrast to having all transactions broadcast on the main blockchain.

[Technical Details](http://lightning.network/how-it-works/)

Basically, by using an off-chain ledger, the two users that are a part of the transaction will constantly update that ledger. Almost like a mini-blockchain, which is secure because it uses the same protocol as the native blockchain. An analogy is the ability to form legal contracts without the enforcement of the court, because both parties know the law, so each party can enforce it in the case that the other tries to manipulate.

It's called a "network" because it forms a graph-based network through these pairs of users. User A -> B, B -> C, means that A -> C (transference rules).
