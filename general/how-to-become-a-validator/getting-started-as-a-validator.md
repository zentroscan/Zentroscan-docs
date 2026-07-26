# Getting started as a validator

## Pre-requirements

In order to be a Zentroscan Coin validator, you first must see that you meet the pre-requirements:

* You know what it means to be a Zentroscan Coin validator - How to become a validator
* You have at least 20K Zentroscan tokens or you will have an aggregated delegation of at least 20K Zentroscan tokens.

## How to become a Zentroscan Coin validator

To quickly become a validator, follow this steps:

Read more at: [https://github.com/zentroscan/Become-Validator](https://github.com/zentroscan/Become-Validator)

## Run a Zentroscan Validator



### Setting up a node



1. Git clone [https://github.com/zentroscan/Become-Validator](https://github.com/zentroscan/Become-Validator)
2. Create an Account

```
chmod +x openethereum
./openethereum account new --config ./node.toml
```

Returned address like that 0x00aa39d30f0d20ff03a22ccfc30b7efbfca597c2

Copy result address to node.toml Ex:

```
...
[account]
unlock = ["0x00aa39d30f0d20ff03a22ccfc30b7efbfca597c2"]
password = ["password"]

[mining]
force_sealing = true
engine_signer = "0x00aa39d30f0d20ff03a22ccfc30b7efbfca597c2"
reseal_on_txs = "none"
...
```

3. Run the authority nodes

```
./openethereum --config ./node.toml

```

4.  Stake

    Stake

    To stake ZNTC coin, all you should do is sending your ZNTC coin to the Zentroscan Consensus contract address over the Zentro network from the validator address. The Zentroscan Consensus contract address: 0x617D8362243C34c3D6f0399998D855963Db03B3d The easiest way to do so, is to import your private key or key-store file to your favourite wallet (for example Metamask), switch network to ZentroScan and send the ZNTC coin to the Consensus contract address.

    You can find your key-store (containing your private key) and the password for the created account in: /node/keys/zentro-blockchain/UTC--xxxx /node.pwd
5.  Wait for 1 cycle (approximately 48 hours).

    Wait until the next cycle gets started.

