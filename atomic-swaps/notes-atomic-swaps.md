# Notes on Atomic Swaps

## Scenario

### Scenario1

* Alice has 5 ETH, but she prefers 1 BTC.
* Bob has 1 BTC, but he prefers 5 ETH.

Therefore, Alice and Bob decide to make a trade. Alice is going to exchange her 5 ETH with Bob's 1 BTC. However, Alice and Bob want to make this exchange **without any trusted third party**, either the centralized or decentralized exchange. Moreover, Alice and Bob don't trust each other. So neither Alice nor Bob is willing to give their property to the counterparty first, and waiting for the counterparty to pay the corresponding amount of money back.

## Algorithm

> Rewrite of the algorithm proposed by Tier Nolen at [here](https://bitcointalk.org/index.php?topic=193281.msg2224949#msg2224949). I believe this would be a better-explained version. :)


Alice wants to exchange her 1 BTC with Bob's 10 LTC. So let's suppose Alice will initiate the atomic-swaps process.

1. Alice randomly selects a **secret** number `x`, and computes the hash of that secret number `H = hash(x)`.

    Alice only gives the hashed value `H` to Bob. (The secret value `x` should be kept secretly!)

2. Alice creates `Tx1` that **conditionally** pays Bob 1 BTC. This is a conditionally payment, meaning that Bob can only redeem the amount which is 1 BTC once he met one of the conditions:
    * the secret `x` is revealed and `signature of Bob` is attached.
    * `both the signature of Alice and Bob` are provided. i.e., the transaction is both signed by Alice and Bob.

3. Alice creates `Tx2` that **conditionally** pays 1 BTC to A, i.e., **refund** transaction, with the condition that
    * this transaction is **timelocked** by `OP_CheckSequenceVerify (CSV)` within T hours and also requires `Alice's & Bob's signature`.

    What it means is that Alice can only redeem/*refund* her 1 BTC when Tx2 is mined into blockchain PLUS T hours.

    ```
    NOT SURE it's using CLTV or CSV
        * If CLTV, A can refund when T hours **after the transaction is created**. (Absolute timelock)
        * If CSV, A can refund when t hours **after this transaction is put/mined into the blockchain**. (Relative timelock)
    ```

 *For more info about Bitcoin Timelock, check out my [blog post](http://robinhung.org/2018-02-14-bitcoin-timelock/)*

4. Alice sends `Tx2` to Bob. After Bob signing this transaction, sends it back to Alice.

    Now, Bob's signature is attached. Meaning that Alice can get her refund after the timelock is expired.

5. *[1]* A submits `Tx1` to the network.

6. Bob ....

[TODO]
