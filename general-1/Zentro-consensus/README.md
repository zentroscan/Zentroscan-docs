# Zentroscan Coin Consensus

Consensus is a fault-tolerant mechanism that is used in blockchain systems to achieve the necessary agreement on the single state of the network. Zentroscan Coin network is using a [Delegated Proof of Stake](https://en.bitcoinwiki.org/wiki/DPoS) (DPoS) consensus model. DPoS is a variation of [Proof of Stake](https://en.bitcoinwiki.org/wiki/Proof-of-stake) consensus. In PoS there are a set of validators that are responsible for keeping the network updated and validating the network's state. They do this in turns, every validator has their turn in line. On their turn the validator updates the network's state, and the rest of the validators check that the update is valid.

![](<../../.gitbook/assets/image (3).png>)

Consensus contract is used to manage the list of the network validators and delegators

BlockReward contract is calculates the reward amount that validators and delegators will receive on each block validation. The reward size is proportional to validator's stake.

With Voting contract validators are vote on various changes on these 3 base level contracts. All those contracts are proxied with implementation that handles the logic. The implementations can be changed only by the Voting process.&#x20;

The bridge is used to transfer the Zentroscan Coin native token between Zentroscan Coin and Ethereum networks.&#x20;

## [Consensus - 0x617D8362243C34c3D6f0399998D855963Db03B3d](https://Zentroscan.com/address/0x617D8362243C34c3D6f0399998D855963Db03B3d

This contract is responsible for handling the network DPos consensus. The contract stores the current validator set and chooses a new validator set at the end of each cycle. The logic for updating the validator set is to select a random snapshot from the snapshots taken during the cycle.

The snapshots are taken of pending validators, who are those which staked more than the minimum stake needed to become a network validator. Therefore the contract is also responsible for staking, delegating and withdrawing those funds.

Stake amount for a validator is the sum of staked and delegated amount to it's address.

This contract is based on `non-reporting ValidatorSet` [described in Parity Wiki](https://wiki.parity.io/Validator-Set.html#non-reporting-contract).

{% hint style="info" %}
minimum stake amount = 100,000 Zentroscan Coin token

cycle duration blocks = 57600 (approximately 2 days)
{% endhint %}

## [Block Reward - 0xf01F5fDeBCC710b394cDbF0119f16BF8528d6C17](https://Zentroscan.com/address/0x7059164Fe471f0410B8a2CF5d960E9B3DC0d0F7F)

This contract is responsible for generating and distributing block rewards to the network validators according to the network specs (5% yearly inflation).

Another role of this contract is to call the snapshot/cycle logic on the Consensus contract

This contract is based on `BlockReward` [described in Parity Wiki](https://wiki.parity.io/Block-Reward-Contract).

## [Voting - 0x658b7b80eea7dd143687B8E7ba54A60Bcf858c6f](https://Zentroscan.com/address/0x23a0f3370F7dCc4203c3F7f588856f388F3274e8)

This contract is responsible for opening new ballots and voting to accept/reject them. Ballots are basically offers to change other network contracts implementation.

Only network validators can open new ballots, everyone can vote on them, but only validators votes count when the ballot is closed.

Ballots are opened/closed on cycle end.

{% hint style="info" %}
max number of open ballots = 100

max number of open ballots per validator = 100 / number of validators

minimum ballot duration (cycles) = 2

maximum ballot duration (cycles) = 14
{% endhint %}

## [Proxy Storage](https://Zentroscan.com/address/0x258aAF236D185119e363b941d232F76bDbe9B61D)

This contract is responsible for holding network contracts implementation addresses and upgrading them if necessary (via voting).

