# Lightning Network Problems ([Emin Gün Sirer](https://twitter.com/el33th4xor)'s version)

> The content is based on [this tweet](https://twitter.com/mindstatex/status/977005396203196417).

### Limited Capacity

* Depends entirely on the credit relationships between LN users.

### Economically broken

* No benefit unless the endpoints frequently exchange funds.
* An exchange needs to have O(N * k) coins tied up in channels

### Insecure and requires new intermediates

* Requires malleability fix
* Requires keys to kept online
* "Watchguards" need to watch the chain 24x7, or else you lost funds
* Counterparty misbehavior can lock your fund

### Erodes privacy

* Routing involves inherent trade-off between efficiency and privacy
* Routing is difficult, except for hub-and-spoke
* Route discovery reveals credit relationships between participants

### User experience is a mess
