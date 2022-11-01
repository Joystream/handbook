---
description: Deciding who gets to be a validator.
---

# 🗳 Nomination

## Introduction

\
The Joystream platform state lives on a blockchain consensus system. This consensus system is a variant of classical BFT consensus combined with Proof-of-Stake to determine who gets to be a consensus participant, i.e. validator. A validator is an actor which checks the validity of newly constructed blocks, proposes new blocks and participates in the consensus process for committing new block to the chain. This role has a purpose very similar to the miners in the Bitcoin blockchain. Importantly, anyone can fully check the validity of the blockchain, not just validators, and this is called validation.

## Nomination

### Responsibilities

* Run and maintain screening nodes that are always available and performant
* Help enforce the consensus rules of the network

### Requirements

* Experienced with how to setup and maintain high performance IT infrastructure
* Access to highly performant and reliable IT infrastructure, with high storage, (up & down) bandwidth and processing capacity
* Able to securely store keys
* Hold sufficient amount of the native platform token to put at stake

## Risks and Rewards

xxx

## Selecting Validators

xxx

## Meet Some Validators

`add list of validators here`

## Guides

### Configure Nominator on Chain

For the time being, we will only show how to do this with [polkadot-js](https://polkadot.js.org/apps/#/explorer). This requires that you have your accounts stored in the app itself, or in the [Polkadot{.js} extension](https://polkadot.js.org/extension/).

We will add another option for doing this, using the joystream-cli and (optionally) signing offline, if you don't want to expose them on the internet.

### **With Polkadot-js**

Go to [polkadot-js](https://polkadot.js.org/apps/#/explorer), where you may have to set the correct endpoint to connect to.

Unless it says `Joystream - joystream-node/7` (update for mainnet) in the top left corner, click on whatever it says, and select the Joystream network you want to connect to.

You need two keys for this, one to be the `controller` and one as the `stash`. The latter holds the stake and must sign at least once to "delegate" to the `controller` which is running the "day to day" operations.

#### **Steps:**

1. Go to the [staking actions tab](https://polkadot.js.org/apps/#/staking/actions), and click the "+ Nominator" button in the top right corner.
2. Select a `stash` and `controller` account from the dropdown, set the "value bonded" as the amount you want to stake, and choose a "payment destination", then hit "next".
3. Select which candidates you want to nominate, and click "Bond & Nominate"

If you are preparing this for later, click the "+ Stash" button instead.

### **With joystream-cli**

`TODO`

### Being a Nominator

Assuming the transaction went through, you will now appear under the "waiting" tab [here](https://polkadot.js.org/apps/#/staking). That means you are in the queue for joining the validator set, but when (and whether) you actually join depends on the competition for getting a slot.

At all times, there is a limit to how many can become validators. What that number is set by the council. The current value can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "validatorCount".

Suppose that number is `n`, and that there are `m` validators that, towards the end of each `era` were already validating or joined the queue:

* If `n >= m`, all will be elected
* If `n<m`, the `n` validators with the highest **total active stake** will be elected for the upcoming `era`

_Notes:_

* An `era` lasts \~6h (on mainnet, \~1h on the current testnet).
* **total active stake** refers to the active stake for the validator itself, plus all of their nominators.

### **Transaction Rejected**

There is a minimum threshold of funds required to stake as a validator. As you can get slashed, that means you can not "re-use" tokens that are staked for other "slashable" purposes, such as role stake.

That number can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "minValidatorBond". (In base value `HAPI` = 1\*10^-10 JOY)

Another reason the transaction can be rejected is if the maximum number of `bonded` accounts have declared as validators. That number can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "maxValidatorsCount". How many there are currently can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "counterForValidators".

There are of course a limitless amount of other reasons the transaction could be rejected if you constructed it yourself in the cli.
