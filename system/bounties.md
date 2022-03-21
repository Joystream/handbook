---
description: >-
  Funding public goods where the community can help with financing, experts can
  help adjudicate quality of deliverables and service providers have an
  incentive to find popular initiatives.
---

# 🏹 Bounties

## Introduction

The only other way to fund the production of goods that create benefits to a broad set of platform participants is through a financing proposal or discretionary spending by a working group lead out of the group budget. These processes incur the transaction costs of beneficiaries having to convince a number of external decision-makers, such as a council financing quorum, that this is a good idea. For smaller initiatives that ideally should start and finish sooner, or where they depend on knowledge or insight that is not as broadly shared, these processes become too costly.

## Assurance Contracts and Dominant Assurance Contracts

An assurance contract is a funding scheme intended to override the inherent free-riding problem in financing public goods by allowing contributors to enter into binding conditional commitments to provide resources to fund the good if a sufficient level of funding is committed. By setting the level sufficiently high, every public good beneficiary becomes close to pivotal to getting the good produced, which generates a rationale incentive to unilaterally commit. Dominant assurance contracts are such schemes where the funding has to be deployed towards a specific service provider or entrepreneur who will produce the good using the funding, and in exchange for this privileged to possibly generate a profit from this activity, the entrepreneur has to put up an initial bounty, called a _cherry_, which is split among all contributors pro-rata. This cherry generates an incentive for contributors, as even when the funding fails, they get a benefit.

## Roles

* **Creator:** The agent responsible for creating the bounty is either a specific member, or the council.
* **Oracle:** The agent responsible for deciding the outcome of a bounty where entrants have submitted work. Is either a specific member, or the council as a whole.
* **Contributor:** An agent responsible for contributing funds that finance the bounty. It is either a specific member or the council as a whole.
* **Worker:** A member who has announced their participation in producing deliverable in a given bounty.

Notice that when the council is an actor, it means that if the lifetime of a bounty spans the boundary of two councils, then a different set of council members are likely in place to exercise control over the same bounty.

## Concepts

### Bounty Actor

The act of creating or contributing funds to a bounty can be done by either a member or the council as a whole, the concept of a _bounty actor_ refers, therefore, to either a specific member or the council, and represents this actor in a unified way.

### Funding Period Type

The funding period type refers to how funds are collected for the benefit of a bounty, and there are fundamentally two types:

* **Perpetual:** The funding has not preset termination date, and new contributors can join on an ongoing basis. There is however a _target_ which sets the upper bound for how much can be contributed.
* **Limited:** The funding lasts for no longer than a given number of blocks, called the _funding period_. There is a lower bound and upper bound for how much must be contributed

### Bounty Type

There are two types of bounties in terms of who can participate as a worker. There are _open_ bounties, where any member can participate, and _closed_ bounties, where the creator can pre-select a set of members who can participate. The primary purpose of closed bounties is to enable dominant assurance contracts, where the creator combines setting themselves as the only feasible worker with also providing a cherry.

### Work Entry

For someone to be able to participate as a worker, with the opportunity to capture some portion of the funds accumulated for the bounty, they have to announce their participation in the bounty in the form of a _work entry_. It describes the status of the involvement of a worker in a bounty, and it is defined by the following information:

* **EntryId:** Unique non-negative integer identifier across all entries.
* **Worker:** Member Id of a worker.
* **Staking Account:** Account holding funds used to stake for participation in bounty.
* **Work:** List of work submissions made during the `Working Period`, encoded as structure data in a standardized format.
* **Status:** The status of an entry has the following disjoint variants.
  * **Working:** Initial status during creation in `Working Period`.
  * **Withdrawn:** When withdrawn during the `Working Period`.
  * **Winner:** Selected as winner during `Judgement Period` , and therefore is due an outstanding share of the bounty funds, called _reward_ .
  * **Passed:** Not referenced by oracle in `Judgement Period` judgement, and therefore is not owed any share of the bounty funds, but has outstanding stake that can be recovered.
  * **Rejected:** Rejected by oracle in `Judgement Period` as a malicious entry, and thus has had stake slashed.
  * **CashedOut:** Worker cashed out stake and/or share of bounty reward.

### Bounty

A bounty is defined by the following information

* **BountyId:** Unique non-negative integer identifier across all bounties.
* **Oracle:** Bounty oracle, is either a member or the council.
* **Type:** Bounty type, is open or closed.
* **Creator:** Bounty creator, is a bounty actor.
* **Cherry:** Amount of funds contributed by creator as cherry.
* **Oracle Cherry:** Amount of funds contributed by creator as oracle cherry.
* **Work Period Length:** The number of blocks which must pass, from the end of the funding stage, before the oracle for the bounty can adjudicate the outcome of the bounty.
* **Judging Period Length:** The maximum number of blocks which can pass, from the end of the working period, while the oracle does not adjudicate a the outcome and funds cannot be withdrawn.
* **Contributions:** The set of all contributions made, each identified with a unique bounty actor, and having an associated positive balance contribution.
* **Entries:** The set of all active entries in the bounty.
* **Metadata:** Structured data encoding the purpose and terms of the bounty.
* **Stage:** The stage of the bounty see next subsection

#### Stage

Below is a list of the stages a bounty can be in, and what each of them mean:

* **Funding Period:** This is the initial stage of a bounty once it is created, during this stage the bounty can accept funding contributions. It is also during this stage the bounty can be vetoed by the council. The creator can also cancel the bounty in this stage if there are no contributions. If a contribution is made that brings the cumulative funding equal to or above the upper bound, then the difference is returned, and the bounty proceeds to the `Working Period` stage. Lastly, if the funding period is limited and the time passes this time, then the bounty proceeds to the `Bounty Failed` stage if there was at least one contribution made, otherwise it proceeds to the `Expried Funding Period` stage.
* **Expired Funding Period:** During this stage, the bounty is only waiting to get cancelled by the creator, terminating the bounty.
* **Working Period:** This is the stage where workers announce their entries and submit their work, and optionally also withdraw. After the working period length has expired since the initiation of the working period, the stage transitions to the `Judgement Period`.
* **Judgement Period:** This is the stage during which the oracle can evaluate the submitted work entries during the working periods. The judgement identifies a set of winning contributors, possibly empty, each with a non-zero number of tokens as a reward. The total reward must perfectly consume the contributed funding to the bounty, but reward distribution need not be uniform. Such a successful outcome also automatically returns the cherry to the creator if it exists. If the oracle selects an empty set of winners, or does not provide a judgement within the end of the judgement period, a transition is made to the `Bounty Failed` stage, otherwise a transition to `Bounty Successful` stage is made if the set is non-empty. Cherry is not returned to creator in this case.
* **Withdrawal Period:** This represents the stage where funds can be withdrawn from the bounty, eventually leading to the bounty getting terminated.
  * **Bounty Successful:** This represents the case where the some subset of workers have been selected as winners, and each must cash out to claim their reward. Workers who did not win also have to cash out their possible prior stake. When the last cashout is made, the bounty is terminated.
  * **Bounty Failed:** This represents the case where no winners were selected, and all contributed funds need to be returned to fund contributors, including a portion of a possible cherry. Workers who did not win also have to cash out their possible prior stake.

The stages and transitions are summarized in the image below.

![Bounty life-cycle stages.](../.gitbook/assets/bounties\_statechart.png)

## Constants

Hard-coded values are defined _for each working group_, and they can only be altered with a runtime upgrade.

| Name                      | Description                                                                                            |
| ------------------------- | ------------------------------------------------------------------------------------------------------ |
| `ClosedContractSizeLimit` | Max work entry number for a closed assurance type contract bounty.                                     |
| `MinCherryLimit`          | Min cherry for a bounty.                                                                               |
| `MinOracleCherryLimit`    | Min oracle cherry for a bounty.                                                                        |
| `MinFundingLimit`         | Min funding amount for a bounty.                                                                       |
| `MinWorkEntrantStake`     | Min work entrant stake for a bounty.                                                                   |
| `ModuleAccountId`         | The Account id of a built-in account, used to hold funds and cherries contributed across all bounties. |
| `LOCK_ID`                 | The Id for the lock used to stake in the bounty system.                                                |

## Extrinsics

### Create Bounty

**Parameters**

| Name                    | Description                                                         |
| ----------------------- | ------------------------------------------------------------------- |
| `origin`                | Caller origin.                                                      |
| `oracle`                | Bounty actor that is oracle.                                        |
| `bounty_type`           | Bounty type.                                                        |
| `creator`               | Bounty actor that is creator.                                       |
| `cherry`                | Amount of funds dedicated as cherry.                                |
| `oracle_cherry`         | Amount of funds dedicated as oracle cherry.                         |
| `entrant_stake`         | Amount of stake required for prospective workers to create entry.   |
| `funding_period_type`   | The number of blocks in the funding period.                         |
| `working_period_length` | The number of blocks in the working period.                         |
| `judging_period_length` | The number of blocks in the judging period.                         |
| `metadata`              | Structured metadata describing the bounty in a human readable form. |

#### Conditions

* `origin` corresponds to `bounty_actor`.
* If `creator` is
  * a member, then the controller account of the member must have sufficient balance for the `cherry` and the `oracle cherry`.
  * the council, then the council budget must accommodate the `cherry` and the `oracle cherry`.
* `cherry` is no less than `MinCherryLimit`.
* `oracle cherry` is no less than `MinOracleCherryLimit`.
* `entrant_stake` is no less than `MinWorkEntrantStake`.
* If `bounty_type` is closed, the number of members is no greater than `ClosedContractSizeLimit`, and not zero.
* If `funding_period_type` is
  * perpetual, then the target is greater than zero.
  * limited, then the minimum funding amount, max amount and funding period length all must be non-zero, and the max funding amount must be greater than the minimum funding amount.

#### Effect

* A new bounty is created in the `Funding Period`.
* Deduct `cherry` and `oracle cherry` from either the council budget or controller account of the creator, and credited to account `ModuleAccountId`.

### Cancel Bounty

**Parameters**

| Name        | Description               |
| ----------- | ------------------------- |
| `origin`    | Caller origin.            |
| `creator`   | Bounty actor for creator. |
| `bounty_id` | Bounty identifier.        |

#### Conditions

* `origin` corresponds to `creator`.
* `bounty_id` corresponds to an existing `bounty`.
* `creator` created bounty identified by `bounty_id`.
* `bounty` is either in stage `Funding Period` without any contributions, or is in stage `Expried Funding Period`.

#### Effect

* `cherry` is credited to `creator` and deducted from `ModuleAccountId`.
* `oracle cherry` is credited to `creator` and deducted from `ModuleAccountId`.
* `bounty` is terminated.

### Fund Bounty

**Parameters**

| Name        | Description                                                   |
| ----------- | ------------------------------------------------------------- |
| `origin`    | Caller origin.                                                |
| `funder`    | Bounty actor for the funder.                                  |
| `bounty_id` | Identifier for the bounty to be funded.                       |
| `amount`    | Balance to be contributed towards the bounty from the funder. |

#### Conditions

* `origin` corresponds to the `funder`.
* `bounty_id` corresponds to an existing `bounty`.
* `bounty` is in stage `Funding Period`.
* `funder` can cover `amount`.
* `amount` is no less than `MinFundingLimit`.

#### Effect

* `amount` would bring the total amount funded so far, denoted by `current_funding`, equal to or over the target or max value, denoted by `limit`, and transition to the `Working Period` . Let `_amount` denote the quantity of funds that can be contributed to the bounty without overflowing the limit, that is `min(limit - current_funding, amount)` .
* `_amount` is debited from `funder` and credited towards account \*\*\*\* `ModuleAccountId`.
* If `funder` has already contributed to the bounty, then add `_amount` to their net contribution, otherwise note their total contribution to be `_amount`.

### Withdraw Funding

**Parameters**

| Name        | Description                             |
| ----------- | --------------------------------------- |
| `origin`    | Caller origin.                          |
| `funder`    | Bounty actor for the funder.            |
| `bounty_id` | Identifier for the bounty to be funded. |

#### Conditions

* `origin` corresponds to the `funder`.
* `bounty_id` corresponds to an existing `bounty`.
* `bounty` is in stage `Bounty Failed`.
* `funder` has made a contribution to the `bounty` that has not been withdrawn.

#### Effect

* Remove contribution of balance `amount` made by `funder` to `bounty`.
* Credit `funder` with `amount` and debit `ModuleAccountId` the corresponding amount.
* If there is no outstanding contributions or entries to the bounty, then terminate the bounty.

### Announce Work Entry

**Parameters**

| Name                 | Description                                                             |
| -------------------- | ----------------------------------------------------------------------- |
| `origin`             | Caller origin.                                                          |
| `member_id`          | Member identifier of prospective worker.                                |
| `bounty_id`          | Identifier for the bounty in which member wants to join.                |
| `staking_account_id` | Account balance.                                                        |
| `metadata`           | Structured metadata describing the work entry in a human readable form. |

#### Conditions

* `origin` corresponds to identifier `member_id` for a member.
* `bounty_id` corresponds to an existing `bounty`.
* `bounty` is in stage `Working Period`.
* `member_id` does not have an active work entry on `bounty`.
* If `bounty` is a closed bounty, then `memeber_id` is among the permitted participants.
* `staking_account_id` is a staking account associated with the member, and has a free balance no less than `MinWorkEntrantStake` and no conflicting staking locks present.

#### Effect

* A work entry is added for the member to the bounty, in the `Working` state.
* Account with id `staking_account_id` has lock with Id `LOCK_ID` and of size `MinWorkEntrantStake` set.

### Withdraw Work Entry

**Parameters**

| Name        | Description                                            |
| ----------- | ------------------------------------------------------ |
| `origin`    | Caller origin.                                         |
| `member_id` | Member identifier for worker.                          |
| `bounty_id` | Identifier for bounty to which work entry corresponds. |
| `entry_id`  | Identifier for work entry.                             |

#### Conditions

* `origin` corresponds to identifier `member_id` for a member.
* `bounty_id` corresponds to an existing `bounty`.
* `bounty` is in stage `Working Period`.
* `entry_id` corresponds to an entry `entry` with status `Working` and where the worker has identifier

#### Effect

* The `entry` status is set to `Withdrawn`.
* The staking account of the entry has lock with Id `LOCK_ID` removed, and the account is slashed a share of the staked balance equal to the share of the working period length for which the entry had the status `Working`.

### Submit Work

**Parameters**

| Name        | Description                                            |
| ----------- | ------------------------------------------------------ |
| `origin`    | Caller origin.                                         |
| `member_id` | Member identifier for a worker.                        |
| `bounty_id` | Identifier for bounty to which work entry corresponds. |
| `entry_id`  | Identifier for work entry.                             |
| `work_data` | Encoded work metadata.                                 |

#### Conditions

* `origin` corresponds to identifier `member_id` for a member.
* `bounty_id` corresponds to an existing `bounty`.
* `bounty` is in stage `Working Period`.
* `entry_id` corresponds to an entry `entry` with status `Working` and where the worker has identifier

#### Effect

`None`.

### Submit Oracle Judgement

**Parameters**

| Name        | Description                                                                                  |
| ----------- | -------------------------------------------------------------------------------------------- |
| `origin`    | Caller origin.                                                                               |
| `oracle`    | Bounty actor that is oracle.                                                                 |
| `bounty_id` | Identifier for bounty for which judgement is being submitted.                                |
| `judgement` | Set of entries to be identified as winners, and set of entries to be identified as rejected. |

#### Conditions

* `origin` corresponds to identifier `member_id` for a member.
* `bounty_id` corresponds to an existing `bounty`.
* `bounty` is in stage `Working Period`.
* `judgement` references two disjoint sets of entries that all have status `Working`
  * a, possibly empty, set of entries designated as winners, each having submitted at least one work submission, and each with an associated non-zero balance designated as the reward, and where all rewards add up to the total funding of the bounty.
  * a set of entries designated as rejected, to be slashed.

#### Effect

* for each winner entry referenced by `judgement`, credit worker account and debited from `ModuleAccountId`, remove lock with Id `LOCK_ID`, and set status to `Winner`.
* for each rejected entry referenced by `judgement`, apply slashing, remove lock with Id `LOCK_ID`, and set status to `Rejected`.
* transition bounty to stage `Bounty Failed` if there are no winners, otherwise transition to `Bounty Successful`.
* credit oracle account with oracle cherry, and debited from `ModuleAccountId`.

### Cashout Work Entrant Funds

**Parameters**

| Name        | Description                                            |
| ----------- | ------------------------------------------------------ |
| `origin`    | Caller origin.                                         |
| `member_id` | Member identifier for a worker.                        |
| `bounty_id` | Identifier for bounty to which work entry corresponds. |
| `entry_id`  | Identifier for work entry.                             |

#### Conditions

* `origin` corresponds to identifier `member_id` for a member.
* `bounty_id` corresponds to an existing bounty `bounty`.
* `entry_id` corresponds to an entry `entry` where worker has identifier `member_id` and the status is not `CashedOut`or `Rejected` or `Withdrawn` .
* `bounty` is in stage`Withdrawal Period`.

#### Effect

* if `entity` has status `Winner`, then the associated reward is credited to `member_id` controller account and debited from `ModuleAccountId`.
* `entity` staking account has lock with Id `LOCK_ID` removed.
* `entity` status is updated to `CashedOut`.
