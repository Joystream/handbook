---
description: Outlining the launch phases for the Carthage testnet and mainnet.
---

# 🧨 Launch Process

## Introduction

Launching a new blockchain secured by a new PoS validator set, which comes to consensus using a time sensitive BFT protocol, is a vulnerable process which easily can end up with liveness failure as a result of networking or operational malfunctioning. For this reason, it should be happen in a gradual process, starting very centralised  and small, and opening up to a broader set of stakeholders while block production is monitored. It also has to be a fair process which does not bias in favor of early or arbitrary participants. Lastly, there must be some room for small scale coordination to handle any unforunforeseenseen catastrophic errors which may occur early, and with minimal if any side-effects. The process for launching the Joystream blockchain was designed based on these requirements.

## Carthage and Mainnet

This process will be used for the upcoming launch of the `Carthage`  network, where runtime is feature frozen - and genesis block is largely locked in, and only unforseen circumstances will result in further changes to the process described herein.

## Overview

The launch of the final joystream testnet - `Carthage`, intended as the final test of the runtime and our intended deployment plan for the Joystream mainnet, will be rolled out as outlined in the table below:

| Stage (Runtime) | Duration | Sudo                        | Consensus | Calls Allowed                                                                                         | Main Jsgenesis Actions                  | Staking Rewarded | #Validators     |
| --------------- | -------- | --------------------------- | --------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------- | ---------------- | --------------- |
| **Frozen**      | \~24h    | <p>Yes <br>(Single Key)</p> | PoA       | <p><code>sudo,</code><br><code>staking,</code><br><code>session,</code><br><code>multisig*</code></p> | <p>Bootstrap <br>-> Thawn</p>           | No               | 9-12            |
| **Thawn**       | \~6days  | <p>Yes<br>(Multisig)</p>    | PoS       | <p><code>sudo,</code><br><code>staking,</code><br><code>session,</code><br><code>multisig*</code></p> | <p>Set #Validators<br>-> Supervised</p> | Yes              | 12-24           |
| **Supervised**  | Weeks    | <p>Yes<br>(Multisig)</p>    | PoS       | Everything`**`                                                                                        | <p>Set #Validators<br>-> Liberated</p>  | Yes              | 24-?            |
| **Liberated**   | NA       | No                          | PoS       | Everything`**`                                                                                        | NA                                      | Yes              | council decides |

* `*` All transaction related to the `sudo`, `staking`, `session` and `multisig` modules will not be filtered, regardless of origin. This means:
  * Prospective validators and nominators can prepare and configure their validator (on chain), and/or nominate. There will be no changes to the actual set however during the `Frozen` stage.
  * Any `multisig` transactions can be initiated and approved, but the actual call will be filtered unless the call is:
    * `sudo.*`
    * `staking.*`
    * `session.*`
  * Although any `sudo.*` will get through the filter, unless the caller of the extrinsic is actually `sudo`, the transaction will, of course, still fail.
* `**` Some filters will still apply, but they are only applied to certain features that are in the runtime, but not properly integrated. The main example being the `bounty` module.

## Frozen Phase

### Overview

* **Duration:** `~24hours`
* **Consensus:**`PoA`
* **Purpose:** bootstrapping of `memberships`
* **Actors:**
  * Jsgenesis (as `sudo`)
  * Prospective validators and nominators
* **Filter:** everything except
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

## Thawn Phase

### Overview

* **Duration:** `~6days`
* **Consensus:** `PoS`
* **Purpose:** Ensure a safe transition from `PoA` to `PoS`
* **Actors:**
  * Jsgenesis (as `sudo`)
  * Validators and nominators
* **Filter:** everything except
  * `staking`
  * `session`
  * `sudo`
  * `multisig`

### Purpose

To ensure a safe transition from `PoA` to `PoS`, Jsgenesis will gradually increase the size validator set (ie. the maximum amount of validators in each `era`).

The benefits of doing relatively small increases of the size:

* Higher competition for slots -> higher stakes required -> actors will be more careful and diligent
* Lower chances of a single bad faith actor occupying a critical amount of slots
* Easier to reach, assist and recover in case of issues

### Community Actions

With the filter still intact, the main action the community can do is to get involved with validation and nomination.

#### Validators

During this stage, validators and nominators can come and go as they like. They will earn rewards, but are also at the risk of being slashed.

### Jsgenesis Actions

The actions and transactions to be made by Jsgenesis can be found, in sequence, below.

#### Set the `validatorCount`

As we see more and more competition for slots, and that the current validator set are performing well, Jsgenesis will increase the amount of slots allowing new actors to join.

More specifically, some of the metrics we will look at are:

* Are all validators online, and producing blocks when called upon
* Are all validators contributing to finalization
* Are validators well connected to each other, maintaining acceptable latency and the blocktime stays at \~6s.
* Is there a sufficiently "deep" bench to ensure the stake requirements are "acceptable", and that there will still be a queue afterwards.

How many times this will be done depends on the above.

#### Move to `Supervised`

Once \~6 days have passed, and we are now assuming that the validators are performing well, Jsgenesis will do a runtime upgrade to the `Supervised` stage, that effectively removes the transaction filter.

## Supervised Phase

### Overview

* **Duration:** `unknown`
* **Consensus:** `PoS`
* **Purpose:**
  * Remove the transaction filter, thus opening for "normal" operations and governance.
  * Maintain `sudo` power for potential emergencies
* **Actors:**
  * Jsgenesis (as `sudo`)
  * Everyone
* **Filter:** nothing except
  * `bounty`
  * a few calls in proposals and content directory

### Purpose

Although "no" transactions will be blocked by the filter, the first 8 days of the `Supervised` stage will still be rather limited.

New members can register and anyone can transfer tokens, but nothing interesting can happen before the council is set and Leads are hired. Together, they are required to "open" up:

* proposals
* the forum
* content creation, storage and distribution
* hiring of workers
* etc.

Once election, the council can do whatever they want, but Jsgenesis will retain `sudo` power for the time being.

### Community Actions

Pretty much everything!

The "required" actions are listed below:

* Elect a council
* Establish working groups
  * Set budgets
  * Create openings
  * Hire Leads
    * Storage/content Leads enables content creation
    * Distributor Lead enables content distribution
    * Forum Lead enables the forum
    * Hire Workers

After a couple days, we should be in a place where everyone can participate by creating content, build, host infrastructure and earn a little $JOY before mainnet.

### Jsgenesis Actions

The actions and transactions to be made by Jsgenesis can be found, in sequence, below.

#### Set the `validatorCount`

Although the council will, and shall, take over this role fairly soon, it will take at least 3 councils due to the constitutionality.

In the meantime, Jsgenesis have the option to increase or decrease the number based on the metrics listed for `Thawn`.

#### Move to `Liberated`

Although the exact timeline is not clear, on the `Carthage` network Jsgenesis will make their final transaction with `sudo` before the second council is elected. The only change will be to remove `sudo`, thus giving full control to the council.

Hopefully, nothing else will be required.

## Liberated Phase

### Overview

* **Duration:**`forever`
* **Consensus:** `PoS`
* **Purpose:** `Video platform DAO`
* **Actors:** Everyone
* **Filter:** Same as prior
