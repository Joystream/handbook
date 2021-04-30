---
description: >-
  Working groups organize subcommittees of incentivized and staked contributors
  around making a subsystem of the platform to work.
---

# Working Groups

## Introduction

A working group is an organizational body, subject to the oversight of the council, which is responsible for the day to day functioning of some subsystem of the platform. There is exactly one working group per subsystem. The rationale for having a working group for this purpose, rather than having the council directly involved, has three parts. First, since all council members are supposed to be fully informed on all matters the cumulative workload of overseeing all subsystems would not be feasible for a single council. Second, even if it was feasible, voting is not a sound means of making such decisions, because there is a lack of guaranteed coherence in the decisions over time. Third, each subsystem will over time likely require a differentiated skill set, knowledge base and social capital. The appropriate analogy for understanding the role of the working groups in the overall operation of the system would be a commission or agency body in a political institution.

## Roles

The relevant roles in a working group are

* **Applicant:** A member who has submitted an application to join an opening for a worker role in the working group. A given member may apply more than once to a given opening, and also if they already occupy the role as worker the same group. Openings are created by the lead \(see below\), or by the council when wanting to fill the lead role.
* **Worker:** A member who has, through an application, entered the working group.The worker may or may not be staked, and is receiving payouts to a designated account at regular intervals. The worker role gives some ability to act in a domain specific way within the given subsystem. So for example in the context of the forum, a worker in the forum working group can be assigned to be a moderator in certain forum categories, and have associated moderation privileges. Lastly, a member may act as multiple works simultaneously, or over time, in the same working group.
* **Lead:** A designated worker who is responsible for hiring and managing the other workers, as well as allocating funds from a budget towards purposes that support the success of the subsystem. Also the leader could set the general working group status, like: 
  * a one line status message on the subsystem,
  * new upcoming expected positions,
  * a link to a subsection of the forum devoted to the subsystem,
  * a message feed including information updates.

## Concepts

### Worker

A has the following information associated

* **Id:** A unique non-negative integer identifier.
* **Membership**: The membership to which this role corresponds. Comes from the initial application to the opening by which worker is hired.
* **Role account**: The account currently used to authenticate as this role in the relevant subsystem. Authentication in the working group is done using the controller account of the member, so as to allow for division of labor behind a single membership across multiple roles, while not requiring full trust. Is updatable by member.
* **Staking profile:**
  * **Staking account:** Holds the stake currently associated with the role. .
  * **Leaving unstaking period:** The number of blocks required from a worker initiating leaving the group until their staked funds are unlocked.
* **Reward account**: The destination account to which periodic rewards are paid out.

  All roles have the following information associated.

* **Reward rate per block:** The number of tokens the worker earns per block, although payouts do not occur per block, but every `REWARD_PAYOUT_PERIOD` blocks. This is earned for every block from being hired to being terminated, or initiating leaving the group. It is not earned during unstaking.
* **Owed reward:** The total reward this worker was not paid over a number of payout periods where there was not sufficient funds in the working group budget.
* **Unstaking status:** Is either _normal_, or _unstaking_. The initial status is the former, and the latter is only entered into when the worker attempts to leave.

### Lead

A designated worker may be identified as the lead at any time, let `current_lead` represent the worker id of this worker when set. It is the role of the council to manage what worker, if any, is the lead in a given working group.

### Budget

The budget is the root resource pool for all token minting in the working group, and the size of the pool is denoted by `budget`. The budget can be increased or reduced by the council. Whenever rewards are paid, or the leader does discretionary spending, it drains the budget, and these events can only take place if the budget allows it. There may be other additional subsystem specific expenditures that depend on the budget, such as minting initial balances for new invited members in the membership system.

### Rewards

All workers are paid every `REWARD_PAYOUT_PERIOD` blocks, and each worker is to be credited according to their own reward rate, and any possibly outstanding owed reward. During this payout, where workers are processed in some consistent order \(for a given set of workers\), the crediting only occurs while the budget is respected. Also, workers unstaking are ignored. For each payout, the budget is tightened. If a worker cannot be paid out in full, then the difference is added to their owed reward. The budget will then have to be reset by the council. When a worker is terminated, or leaves, any owed reward and outstanding reward from the last payout, are attempted paid out, however if the budget does not allow it, then the worker suffers the loss.

### Spending

In addition to rewards, the lead can spend from this budget for arbitrary purposes, to fund expenses and initiatives that are in line with the purpose of the group.

### Staking

Worker roles require staking in order to apply and remain in the role. Staking for worker roles is done using a designated working group lock on a single account per worker role. The amount required is set by the discretion of the lead. The staking requirement could be decreased by the lead \(or by the council for leaders\). The worker is able to increase their own stake, for example, in response for leader demand. Consult the [Staking](../key-concepts/staking.md#reuse) article to see a list of other staking purposes, and corresponding locks, which can be combined with staking for a given working group.

#### Staking Policy

A _staking policy_ describes the requirements involved in staking for a role. It has two components, it has an _amount_, the minimum number of tokens required to stake, and a _leaving unstakig period,_ the unstaking period incurred form the time a worker initiates leaving the group.

### Slashing

Slashing is initiated by the council, or the lead, by pure discretion. The full staked amount is at risk of getting slashed, but need not be, and there is no limit to the number of times one may get slashed. Importantly, slashing can also occur while a worker is unbonding. This is of particular importance to avoid a lead attempting to leave the role the moment a slashing proposal is observed. Such last minute exits cannot avoid slashing so long as the unbonding period chosen by the council for the lead, is sufficiently long compared to the inherent delays in the proposal system. There is a similar, but much less severe, concern about workers trying to race with slashing transactions submitted by the lead by attempting to preempt slashing by observing the pool of unconfirmed transactions. The unbonding period required to make this infeasible can be much shorter, essentially just however long is required to have a sufficiently high certainty that the slashing transaction is included in a block.

### Hiring

Hiring is the process by which a worker enters the group. Both normal workers and the lead worker, are hired, in the latter case the council initiates the hiring. Hirings are organized into _openings_, where zero or more _applicants_ may be selected as winners, and becoming workers. An opening for the lead position will always result in hiring at most one worker, and this worker becomes the lead.

#### Application

An application has the following information

* **Id:** A unique immutable non-negative integer identifying an individual application across all openings, is automatically assigned when an application is created.
* **Role account:** A required account that is used to authenticate as the worker if selected, in other parts of the platform. Need not be unique across workers, but in practice probably will be.
* **Staking account:** The account holding the stake of the application.
* **Member:** Identifier of member from which application originates.
* **Description:** [Application metadata](/key-concepts/encodings.md#working-group-application-metadata).

#### Opening

An opening has the following information associated

* **Id:** A unique immutable non-negative integer identifying an individual opening, is automatically assigned when an opening is created.
* **Type:** Whether the opening is for the lead or for a non-lead worker.
* **Description:** [Opening metadata](/key-concepts/encodings.md#working-group-opening-metadata).
* **Staking policy:**
  * **Balance:** The required non-zero balance required.
  * **Leaving unstaking period:** The number of blocks required from a worker initiating leaving the group until their staked funds are unlocked.
* **Applications:** All applications created, but not yet withdrawn.

### Status

A working group has an associated _status_ that is updatable by the lead. The status is modified through text signals (see: [Set Status](#set-status)), which follow a standardized [WorkingGroupAction](/key-concepts/encodings.md#working-group-action) encoding.

Sending an encoded [WorkingGroupAction](/key-concepts/encodings.md#working-group-action) message allows signaling one of the following actions:
- Setting or updating the basic [group metadata](/key-concepts/encodings.md#workinggroupmetadata) (for example: `statusMessage`, `description`)
- Creating an _Upcoming Opening_ (for the purpose of signaling that an actual [opening](#opening) may be created in the future)
- Removing existing _Upcoming opening_.

Those signals are processed by _Query nodes_, which update the status in the database in case the signalled action is valid.

## Constants

Hard-coded values are defined _for each working group_, and they can only be altered with a runtime upgrade.

| Name | Description |
| :--- | :--- |
| `MAX_NUMBER_OF_WORKERS` | The maximum number of workers that can be part of the working group simultaneously. |
| `REWARD_PAYOUT_PERIOD` | The number of blocks between each time workers are paid their total reward for the period. |
| `LOCK_ID` | The Id for the lock used to stake in this working group. |
| `MIN_UNSTAKING_PERIOD_LIMIT` | Minimum unstaking period in this working group. |
| `MINIMUM_STAKE_FOR_OPENING` | Minimum stake required for any opening. |

## Extrinsics

### Creating an Opening for Workers

**Parameters**

| Name | Description |
| :--- | :--- |
| `description` | Encoded [opening metadata](/key-concepts/encodings.md#working-groups-opening-metadata). |
| `staking_policy` | Staking policy of new opening. |
| `reward_per_block` | Initial per reward block. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `stake` for `staking_policy` is equal to or more than `MINIMUM_STAKE_FOR_OPENING`
* `leaving_unstaking_period` is more than `MIN_UNSTAKING_PERIOD_LIMIT`

#### Effect

A new opening is added with the given information and for hiring a worker, not lead.

### Apply on Opening

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `opening_id` | Identifier of opening being applied to. |
| `role_account` | Role account of future worker. |
| `staking_account` | Account holding stake. |
| `staking_balance` | Balance to stake. |
| `description` | Encoded [application metadata](/key-concepts/encodings.md#working-group-application-metadata). |

#### Conditions

* Signer uses controller account of member corresponding to `member_id`.
* `opening_id` corresponds to an existing opening.
* `staking_account`is set and
  * `staking_balance` is no less than balance in staking policy
  * is bound to the member,
  * has free balance no `staking_balance`
  * there are no conflicting staking locks present.

#### Effect

A new application is created for the opening, using the provided information, and `staking_account` has lock with Id `LOCK_ID` and of size`staking_balance` if set, otherwise of staking policy of opening.

### Withdraw Application

**Parameters**

| Name | Description |
| :--- | :--- |
| `application_id` | Identifier for application to be withdrawn. |

#### Conditions

* `application_id` corresponds to an existing application.
* Signer uses role account of of application.

#### Effect

The staking is removed by removing the lock on the staking account. The application is removed.

### Fill an Opening for Workers

**Parameters**

| Name | Description |
| :--- | :--- |
| `opening_id` | Identifier of opening. |
| `winners` | Set of application identifiers of winners. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `opening_id` corresponds to existing opening.
* opening is for hiring a worker, not lead.
* all identifiers in `winners` correspond to existing applications.
* Opening type is for worker, and the number of workers in the opening plus the number of  `winners` does not exceed `MAX_NUMBER_OF_WORKERS`.

#### Effect

Create a worker for each application in `winners`, each having a reward rate per block associated with the opening and no owed reward, and remove opening.

NB: Notice that all losing applications are still around in order to allow recovering stake later.

### Cancel an Opening for Workers

**Parameters**

| Name | Description |
| :--- | :--- |
| `opening_id` | Identifier of opening. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `opening_id` corresponds to existing opening.
* opening is for workers, not lead.

#### Effect

The opening is removed.

NB: Notice that all applications are still around in order to allow recovering stake later.

### Update Role Account

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `role_account` | New role account of worker. |

#### Conditions

* `worker_id` corresponds to existing worker.
* Signer uses controller account of member corresponding to member identifier in worker.

#### Effect

Worker role account is updated to `role_account`.

### Update Reward Account

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `reward_account` | New reward account of worker. |

#### Conditions

* `worker_id` corresponds to existing worker.
* Signer uses controller account of member corresponding to member identifier in worker.

#### Effect

Worker reward account is updated to `reward_account`.

### Update Reward Amount for Worker

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `reward_per_block` | New reward rate per block for worker. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `worker_id` corresponds to existing worker, not lead.

#### Effect

Worker reward rate per block is set to `reward_per_block`.

### Leave Worker Role

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `rationale` | Human readable text. |

#### Conditions

* `worker_id` corresponds to existing worker.
* Signer uses controller account of member corresponding to member identifier in worker.
* worker unstaking status is normal.

#### Effect

* Staking status is set to unstaking - where final removal of worker and staking lock occurs after leaving unstaking period.
* When the worker leaves, if worker has owed reward, then as much as is possible under the current budget is paid out, and whatever could be paid out is used to updated the owed field.

### Terminate Worker

**Parameters**

| Name | Description |
| :--- | :--- |
| `member_id` | Member identifier. |
| `slashing_amount` | Optional amount to be slashed. |
| `rationale` | Human readable text. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `worker_id` corresponds to existing worker, not lead.
* If `slashing_amount` is set, then it is greater than zero and the worker
  * staked balance is no less than `slashing_amount`,
  * staking status is normal.

#### Effect

* If worker has owed reward, then as much as is possible is paid out of the current budget, and whatever could be paid out is used to updated the owed field.
* If `slashing_amount` is set, it's slashed from the staking account.
* Worker is removed.

### Slash Worker

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `slashing_amount` | Amount to be slashed. |
| `rationale` | Human readable text. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `worker_id` corresponds to existing worker, not lead.
* `slashing_amount` is greater than zero.
* staked balance is no less than `slashing_amount`.

#### Effect

The staking account is slashed by `slashing_amount`.

### Decrease Worker Stake

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `stake_amount` | Amount to decrease staked balance by. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `worker_id` corresponds to existing worker, not lead.
* worker has staking profile set.
* `stake_amount` is greater than zero.

#### Effect

Staking lock is reduced by `slashing_amount`.

### Increase Stake

**Parameters**

| Name | Description |
| :--- | :--- |
| `worker_id` | Worker identifier. |
| `stake_amount` | Amount to increase staked balance by. |

#### Conditions

* `worker_id` corresponds to an existing worker.
* Signer uses role account of worker.
* worker has staking profile set.
* `stake_amount` is greater than zero.

#### Effect

Staking lock is increased by `stake_amount`.

### Leader Spending

**Parameters**

| Name | Description |
| :--- | :--- |
| `account_id` | Account to get the tokens. |
| `amount` | Transfer amount. |
| `rationale` | Spending rationale. |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.
* `amount` is greater than zero.
* `budget` is not less than `amount`.

#### Effect

Account balance is increased by `amount`, and `budget` is reduced correspondingly.

### Set Status

**Parameters**

| Name | Description |
| :--- | :--- |
| `new_status` | Encoded [working group action metadata](/key-concepts/encodings.md#working-group-action). |

#### Conditions

* A lead worker is set.
* Signer uses role account of lead worker.

#### Effect

Assuming the encoded action metadata is valid – the signalled action should be executed by _Query nodes_ (see: [Status](#status))

