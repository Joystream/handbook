---
description: The second phase of the rollout
---

# 2⃣ Phase 2 - Thawn

### Overview

* **Duration:**
  * `~6days`
* **Consensus:**
  * `PoS`
* **Purpose:**
  * Ensure a safe transition from `PoA` to `PoS`
* **Actors:**
  * Jsgenesis (as `sudo`)
  * Validators and nominators
* **Filter:**
  * everything except:
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
