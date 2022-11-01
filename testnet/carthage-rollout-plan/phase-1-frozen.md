---
description: The first phase of the rollout
---

# 1⃣ Phase 1 - Frozen

### Overview

* **Duration:**
  * `~24hours`
* **Consensus:**
  * `PoA`
* **Purpose:**
  * bootstrapping of `memberships`
* **Actors:**
  * Jsgenesis (as `sudo`)
  * Prospective validators and nominators
* **Filter:**
  * everything except:
    * `staking`
    * `session`
    * `sudo`
    * `multisig`

### Purpose

The main reason the chain is deployed with a `PoA` consensus algorithm is to allow a safer deployment, without having to restrict access to the chain spec.

### Community Actions

As soon as the first block is created, anyone (with tokens to cover the fees) can make any transaction they want. However, as stated previously, only transaction to the `staking` or `session` module will be executed. Note that any other action will still incur fees.

#### Validators

Go [here](../../system/validation.md) for a step by step guide to become a validator or nominator.

### Jsgenesis Actions

The actions and transactions to be made by Jsgenesis can be found, in sequence, below.

#### Bootstrapping

As soon as the chain has been deployment, Jsgenesis will run a script that creates all members on the platform as they were at the time of the migration snapshot, meaning:

* `rootAccount`
* `controllerAccount`
* `memberHandle`
* `metadata`
  * The extra data held by the query node
* `isFoundingMember`

As all members are created in sequence, so that members will keep their `memberId`.

#### Set new `sudo` key

As the script that handles the bootstrapping requires `sudo` to bypass the filter, the next step is to change the `sudo` key to a multisig key. The signer keys are stored offline, reducing the risk of loss, hacking and social engineering.

#### Set the `validatorCount`

By default, the chain sets the "ideal" number of validators, namely the `staking.validatorCount` equal to the amount of authorities - which is 9. The (new) `sudo` key will change this to 12.

#### Move to `Thawn`

Once \~24 hours have passed, giving everyone equal opportunity to deploy their nodes and configure their validator keys on chain, `sudo` will make the `staking.forceNewEra()` call, effectively changing the consensus system from PoA to PoS.
