---
description: >-
  The proposal system is the way changes to the platform state and policy are
  suggested, discussed, voted on by the council, and finalized as accepted or
  rejected.
---

# ⚖ Proposal System

## Introduction

A proposal is a motion to change the state or policy of the system in some way. There are a wide variety of such proposal types, each type having a different

* set of required input parameter values
* requirements and risks of proposing
* barrier for getting accepted
* delay to being put into motion when accepted

The reason for this differentiation across types is because different proposals have very different effects, and carry very different risks of failure or abuse. The proposal system has the responsibility of coordinating the different actors involved in the lifetime of a proposal, from submission to finalization.

## Roles

The relevant roles in the proposal system are

* **Proposer:** A member that has submitted an instance of a specific proposal type. A given member can submit multiple proposals at once, or over time.
* **Council Members:** They are tasked with voting on proposals, which determines whether the proposals are accepted or not, as well as discussing a proposal with the proposer, and leaving a rationale for their vote.

## Concepts

### Vote

Each council member can submit at most one vote per proposal, and it includes the following:

* **Rationale:** A human readable description of why they are voting as they are.
* **Type:** There three types
  * **Approve:** Proposal should be approved.
  * **Reject:** Proposal should be rejected. Additionally, it can be expressed whether it should be slashed as part of the rejection.
  * **Abstain:** Voter has no position on outcome.

### Proposal Type

A proposal type is a parametrized intention to have some effect on the platform. The set of proposal types will increase considerably in the future, and the current types are listed below.

#### Constants

All proposal types have constant values for a shared set of parameters that are common across all types, thee are called _proposal constants._ The name and semantics of each constant is listed in the table below.

| **Name**             | Description                                                                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `DECIDING_PERIOD`    | <p>Maximum number of blocks for deciding period.</p><p>Integer no less than 1.</p>                                                                |
| `GRACING_LIMIT`      | <p>Minimum number of blocks that must pass after a<br>proposal is approved until it has its intended effect.</p><p>Integer no less than 0.</p>    |
| `APPROVAL_QUORUM`    | <p>Number of votes cast below which the proposal cannot be approved.</p><p>Integer no less than 1.</p>                                            |
| `APPROVAL_THRESHOLD` | <p>Minimum percentage of approval votes as a share of<br>all cast votes that result in approval.</p><p>Integer in [0, 100].</p>                   |
| `SLASHING_QUORUM`    | <p>Number of votes cast below which the proposal<br>cannot be slashed.</p><p>Integer no less than 1.</p>                                          |
| `SLASHING_THRESHOLD` | <p>Minimum percentage of cast votes as share that slash relative<br>to those that vote approve, abstain or reject.</p><p>Integer in [0, 100].</p> |
| `STAKE`              | <p>Exact stake required to create a proposal of this type.</p><p>Integer no less than 0.</p>                                                      |
| `CONSTITUTIONALITY`  | <p>The number of councils in that must approve the proposal<br>in a row before it has its intended effect.<br>Integer no less than 1.</p>         |

#### Parameters: General & Specific

Whenever a proposal of a given type is created, the proposer must provide values for a set of parameters. The parameters fall into one of two categories: _general_ and _type-specific_. Each parameter will also have some constraint on the valid range of values. The general proposal parameters are

* **Proposer:** Member identifier of the proposer.
* **Title:** A human readable title.
* **Rationale:** A human readable description text that is intended to hold the rationale for the proposal should be accepted. It is expected that some social convention will emerge on the appropriate encoding of this text, for example markdown, that would facilitate consistent input and display across client applications.
* **Trigger:** An optional block number where the proposal is to be executed.
* **Staking Account:** The account that holds the funds that will be locked for staking, if required.

The type-specific parameters for each proposal type are listed with the proposals below.

#### Creation Conditions

When a proposal is submitted, a set of conditions on the values of the input parameters (only) are evaluated, these are called _creation conditions_, and creating the proposal fails if they are not satisfied. These are things like for example respecting the upper bound on the amount of money you are asking for in a spending proposal. Importantly, these checks are _pure_, they only depend on parameters, not the state of the system.

#### Execution Conditions

A proposal may be approved, and at some point the actual business logic that embodies its intended effect has to be executed. This is always much later than when the proposal was first created, and it may very well be possible to have a proposal which originally looked would have had its intended effect to no longer be applicable because the state of he system has changed in the intermediate. An example could be that a funding proposal requires more money than the council currently can spend due to other spending that may have occurred since the proposal was approved. These conditions are called _execution conditions_, and importantly, they are not checked at any time prior to execution of this business logic.

### Proposal

A proposal is defined by the following information

* **Id:** A unique non-negative integer identifier.
* **Type:** Which type of proposal this is.
* **General Parameters:** Values for general proposal parameters.
* **Type-Specific Parameters:** Values for type-specific proposal parameters.
* **Stage:** The life-cycle stage of a proposal, as defined precisely in the next section.
* **Votes:** The set of votes currently associated with the proposal.
* **Council Approvals:** How many prior councils have approved the proposal, starts at 0.
* **Starting Block:** The block where the deciding period was initiated.
* **Discussion:** A single threaded discussion about the proposal, as defined in the discussion section.

**Stage**

Below is a list of the stages a proposal can be in, and what each of them mean:

*   **Deciding:** Initial stage for all successfully created proposals. This is the only stage where votes submitted can actually impact the outcome. If a new council is elected, any present stake is slashed by `REJECTION_FEE` , the staking lock is removed and the proposal transitions to the rejected stage.

    When a vote is submitted it is evaluated as such:

    1. If `APPROVAL_QUORUM` and `APPROVAL_THRESHOLD` are satisfied, then increment council approvals counter. If counter now is `CONSTITUTIONALITY` then remove staking lock and transition to gracing stage, otherwise transition to dormant stage.
    2. If `SLASHING_QUORUM` and `SLASHING_THRESHOLD` are satisfied, but point (1) is not, then slash full stake, remove the lock and transition to the rejected stage.
    3. If points (1) and (2) are not and cannot be satisfied by any future a outstanding votes, then slash stake by up to `REJECTION_FEE`, remove lock and transition to rejected stage.

If `DECIDING_PERIOD` blocks pass while still in this stage, apply checks (1-3) with same transition and side-effect rules as above.

* **Dormant:** Was approved by current council, but requires further approvals to satisfy `CONSTITUTIONALITY` requirement. Transitions to deciding stage when next council is elected.
* **Gracing:** Is awaiting execution for until trigger block, or `GRACING_LIMIT` blocks since start of period if no trigger was provided. When this duration is over, the execution conditions are checked, if they are satisfied the proposal transitions to the execution succeeded stage, if they are not, it transitions to the execution failed stage.
* **Vetoed:** Was halted by SUDO, nothing further can happen. This is removed at mainnet.
* **Slashed:** Was rejected with full stake penalty by the current council.
* **Execution Succeeded:** Execution succeeded, nothing further can happen.
* **Execution Failed:** Execution failed due to unsatisfied execution conditions, nothing further can happen.
* **Rejected:** Was not approved, nothing further can happen.

It useful to designate any proposal in the stages deciding, dormant or gracing, as an _active proposal_, and any other proposal is said to be an _inactive proposal_. Votes can not be submitted for _inactive proposal_.

Before mainnet, an extra transition rule is worth bearing in mind is that, for any active proposal, SUDO can initiate veto, which results in transition to vetoed stage.

The stages and transitions, excluding SUDO dynamics, are summarized in the image below.

![Proposal life-cycle stages.](../../.gitbook/assets/proposal\_3.png)

### Staking

As described, proposals may require staking to be submitted. A single account must be used to provide the stake for a proposal, and it cannot be used to hold stake for any other proposals or purpose, except voting, at the same time. The staking is implemented as a lock with id `PROPOSAL_LOCK_ID`.

### Discussion

A single threaded discussion is opened for each successfully created discussion. A thread can be in two _discussion modes_, open or closed. In open mode, any member can post a message, while in closed mode, only the active council, the original proposer, or one among a set of whitelisted members can post. Mode can be changed by member or council member at any time, and default mode is open. Both council members and proposer can curate whitelist by adding and removing members. A poster can edit a post an unlimited number of times, but only if they have access. A thread can no longer be updated in any way (mode, posting, edits, etc.) when `DISCUSSION_LINGERING_DURATION` have passed since being rejected or executed. Lastly, at most `MAX_POSTS_PER_THREAD` can be posted in a single thread.

## Proposals

This section includes proposals that concern the platform as whole in terms intended effect and type-specific parameters.

### Signal

#### Parameters

| Name     | Description                               |
| -------- | ----------------------------------------- |
| `signal` | The actual human readable signaling text. |

Note that the distinction between `signal` and the rationale parameter is that the rationale is the _why_ and this is the _what._

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

* `signal` is non-empty.

#### Execution Conditions

None.

#### Effect

None.

### Amend Constitution

#### Parameters

| Name               | Description                                  |
| ------------------ | -------------------------------------------- |
| `new_constitution` | The actual human readable constitution text. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

None.

### Funding Request

#### Parameters

| Name       | Description                                     |
| ---------- | ----------------------------------------------- |
| `amounts`  | The amount of tokens requested to each account. |
| `accounts` | Recipients of funds.                            |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

* each `amount` is greater than zero.
* each `amount` is no more than `MAX_SPENDING_PROPOSAL_VALUE`
* there is at least one account

#### Execution Conditions

* the council budget is no less than the sum of `amounts`.

#### Effect

* the council budget is reduced by the sum of `amounts`.
* for each account in `accounts` its fund is augmented by its corresponding amount in `amounts`.

### Runtime Upgrade

#### Parameters

| Name   | Description                                               |
| ------ | --------------------------------------------------------- |
| `blob` | The raw WebAssembly object to be used as the new runtime. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

`blob` is non-empty.

#### Execution Conditions

None.

#### Effect

The block after this proposal is executed will follow the rules of the runtime captured in `blob`.

### Create Working Group Lead Opening

#### Parameters

| Name                      | Description                            |
| ------------------------- | -------------------------------------- |
| `group`                   | Identifier for working group.          |
| `description`             | Human readable description of opening. |
| `stake_policy`            | Optional staking policy.               |
| `per_block_reward_amount` | Block denominated reward.              |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

Same as when creating an opening for workers in the given group with given inputs, except signer check.

#### Effect

Same as when creating an opening for workers in the given group with given inputs, except the opening type is for lead.

### Cancel Working Group Lead Opening

#### Parameters

| Name         | Description                      |
| ------------ | -------------------------------- |
| `group`      | Identifier for working group.    |
| `opening_id` | Identifier for opening in group. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

Same as when cancelling an opening for workers in the given group with given inputs, except signer check.

#### Effect

Same as when cancelling an opening for workers in the given group with given inputs.

### Fill Working Group Lead Opening

#### Parameters

| Name             | Description                          |
| ---------------- | ------------------------------------ |
| `group`          | Identifier for working group.        |
| `opening_id`     | Identifier for opening in group.     |
| `application_id` | Identifier for successful applicant. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

Same as when filling opening in group for worker with given inputs, except `application_id` as `winners` and signer check.

#### Effect

Same as when filling opening in group for worker with given inputs, except `application_id` as `winners`.

### Slash Working Group Lead

#### Parameters

| Name              | Description                   |
| ----------------- | ----------------------------- |
| `group`           | Identifier for working group. |
| `worker_id`       | Worker identifier.            |
| `slashing_amount` | Amount to be slashed.         |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

Same as when slashing a worker in group with given inputs, except

* signer check,
* worker corresponding to `worker_id` must be lead.

#### Effect

Same as when slashing a worker in group with given inputs.

### Terminate Working Group Lead

#### Parameters

| Name              | Description                    |
| ----------------- | ------------------------------ |
| `group`           | Identifier for working group.  |
| `worker_id`       | Worker identifier.             |
| `slashing_amount` | Optional amount to be slashed. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

Same as when terminating a worker in group with given inputs, except signer check.

#### Effect

Same as when terminating a worker in group with given inputs, and removing lead designation.

### Set Working Group Lead Reward

#### Parameters

| Name               | Description                           |
| ------------------ | ------------------------------------- |
| `group`            | Identifier for working group.         |
| `worker_id`        | Worker identifier.                    |
| `reward_per_block` | New reward rate per block for worker. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

Same as when updating reward of a worker in group with given inputs, except signer check.

#### Effect

Same as when updating reward of a worker in group with given inputs.

### Decrease Working Group Lead Stake

#### Parameters

| Name           | Description                        |
| -------------- | ---------------------------------- |
| `group`        | Identifier for working group.      |
| `worker_id`    | Worker identifier.                 |
| `stake_amount` | Amount by which to decrease stake. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

`stake_amount` is greater than zero.

#### Execution Conditions

Same as when decreasing worker stake in group with given inputs, except signer check.

#### Effect

Same as when decreasing worker stake in group with given inputs.

### Update Working Group Budget

#### Parameters

| Name            | Description                     |
| --------------- | ------------------------------- |
| `group`         | Identifier for working group.   |
| `budget_update` | Signed amount change in budget. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

If `budget_update` is non-negative, then this it must be no more than the council budget, otherwise the absolute value must be no more than the current group budget.

#### Effect

If `budget_update` is non-negative, then this amount is reduced from the council budget and credited to the group budget, otherwise the reverse.

### Set Max Validator Count

#### Parameters

| Name                  | Description              |
| --------------------- | ------------------------ |
| `new_validator_count` | New max validator count. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

`new_validator_count` is no less than the `MinimumValidatorCount` value in `pallet_staking` module storage and no greater than `MAX_VALIDATOR_COUNT`.

#### Execution Conditions

None.

#### Effect

Same as `set_validator_count` in `pallet_staking` module with given input.

### Set Membership Price

#### Parameters

| Name                   | Description           |
| ---------------------- | --------------------- |
| `new_membership_price` | New membership price. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

The membership price is set to `new_membership_price`.

### Set Referral Cut

#### Parameters

| Name               | Description                  |
| ------------------ | ---------------------------- |
| `new_referral_cut` | New referral cut percentage. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

The referral cut is set to `new_referral_cut`.

### Set Initial Invitation Count

#### Parameters

| Name                       | Description                    |
| -------------------------- | ------------------------------ |
| `new_default_invite_count` | New default invitations count. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

The default invitations count is set to `new_default_invite_count`.

### Set Initial Invitation Balance

#### Parameters

| Name                          | Description                  |
| ----------------------------- | ---------------------------- |
| `new_invited_initial_balance` | New invited initial balance. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

The new invited initial balance is set to `new_invited_initial_balance`.

### Set Membership Lead Invitation Quota

#### Parameters

| Name               | Description           |
| ------------------ | --------------------- |
| `new_invite_count` | New invitation count. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

The membership working group has an assigned lead with membership id `membership_id`.

#### Effect

The invitation quota of member is set to `new_invite_count`.

### Set Council Budget Increment

#### Parameters

| Name                   | Description                   |
| ---------------------- | ----------------------------- |
| `new_budget_increment` | New council budget increment. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

The budget increment is set to `new_budget_increment`.

### Set Councilor Reward

#### Parameters

| Name                   | Description           |
| ---------------------- | --------------------- |
| `new_councilor_reward` | New councilor reward. |

#### Constants

| Constant             | Value     |
| -------------------- | --------- |
| `DECIDING_PERIOD`    | `fill-in` |
| `GRACE_PERIOD`       | `fill-in` |
| `APPROVAL_QUORUM`    | `fill-in` |
| `APPROVAL_THRESHOLD` | `fill-in` |
| `SLASHING_QUORUM`    | `fill-in` |
| `SLASHING_THRESHOLD` | `fill-in` |
| `PROPOSAL_STAKE`     | `fill-in` |
| `CONSTITUTIONALITY`  | `fill-in` |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

The councilor reward is set to `new_councilor_reward`.

### Create Blog Post

**Parameters**

| Name    | Description            |
| ------- | ---------------------- |
| `title` | Title of the blog post |
| `text`  | Text of the blog post  |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

A blog post is created.

### Edit Blog Post

**Parameters**

| Name      | Description                     |
| --------- | ------------------------------- |
| `post_id` | Id of the blog edited blog post |
| `title`   | New title of the blog post      |
| `text`    | New text of the blog post       |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

Blog post with id `post_id` with new `title` and `text`

### Lock Blog Post

**Parameters**

| Name      | Description                     |
| --------- | ------------------------------- |
| `post_id` | Id of the blog edited blog post |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

Locks the post with `post_id` for modification

### Unlock Blog Post

**Parameters**

| Name      | Description                     |
| --------- | ------------------------------- |
| `post_id` | Id of the blog edited blog post |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

Unlocks the post with `post_id` allowing for modification

## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

| Name                            | Description                                                                     |   Value   |
| ------------------------------- | ------------------------------------------------------------------------------- | :-------: |
| `MAX_RUNTIME_UPGRADE_BYTES`     | Maximum allowed number of bytes in a runtime upgrade Wasm blob.                 | `fill-in` |
| `REJECTION_FEE`                 | Up to number of tokens slashed if proposal rejected, but not with slashing.     | `fill-in` |
| `DISCUSSION_LINGERING_DURATION` | Number of blocks after proposal inactivation a proposal discussion is closed.   | `fill-in` |
| `MAX_POSTS_PER_THREAD`          | Max posts per thread.                                                           | `fill-in` |
| `MAX_ACTIVE_PROPOSALS`          | Max active proposals allowed at any given time.                                 | `fill-in` |
| `PROPOSAL_LOCK_ID`              | The lock id used for proposal staking locks.                                    | `fill-in` |
| `MAX_VALIDATOR_COUNT`           | The maximum number of validators accepted by validator staking system.          | `fill-in` |
| `MAX_WHITELIST_SIZE`            | The maximum number of whitelisted participants in a closed propsoal discussion. | `fill-in` |

## Extrinsics

### Submit Proposal

**Parameters**

| Name        | Description                                                  |
| ----------- | ------------------------------------------------------------ |
| `proposer`  | Member identifier of proposer.                               |
| `title`     | Title for proposal.                                          |
| `rationale` | Rationale for proposal.                                      |
| `trigger`   | Optional trigger block for executing proposal.               |
| `account`   | Optional staking account for proposal.                       |
| `type`      | The of proposal and all associated type specific parameters. |

#### Conditions

* Signer matches controller account of `proposer`
* Number of active proposals is no greater than `MAX_ACTIVE_PROPOSALS`.
* If `PROPOSAL_STAKE` is greater than zero, then `account` must have a free balance no less than that. Also`account` is bound to `proposer`, and only has a voting lock if anything.
* If `trigger` is provided, it must be no less than current block plus `GRACING LIMIT` + `DECIDING_PERIOD`.
* Creation conditions for `type` are satisfied.

#### Effect

A new proposal , of type `type` , is created in the deciding period stage, and a new discussion thread is opened in the open mode. Moreover, if `PROPOSAL_STAKE`is greater than zero, a new lock with id `PROPOSAL_LOCK_ID` and amount `PROPOSAL_STAKE` is set.

### Vote

**Parameters**

| Name        | Description                    |
| ----------- | ------------------------------ |
| `proposal`  | Identifier for proposal.       |
| `vote_type` | The type of vote.              |
| `rationale` | The rationale for the vote.    |
| `councilor` | Identifier for council member. |

#### Conditions

* `proposal` corresponds to an existing proposal in **Deciding** stage.
* Signer is role account of councilor identified by `councilor`.
* Councilor has not yet voted on this proposal.

#### Effect

Record vote of `councilor`, and follow steps in **Deciding** stage for processing a vote.

### Post to Thread

**Parameters**

| Name       | Description                                          |
| ---------- | ---------------------------------------------------- |
| `proposal` | Identifier for proposal.                             |
| `text`     | Post text.                                           |
| `author`   | Either identifier of council member, or of a member. |

#### Conditions

* `proposal` corresponds to an existing proposal in where discussion is active, that is either the proposal is active, or no more than `DISCUSSION_LINGERING_DURATION` blocks have passed since it became inactive.
* `author` corresponds to signer.
* If `author` is a member, either is the proposer, or the discussion mode is open, or it is closed and the `author` is on the whitelist for this thread.
* The current number of posts in this thread is less than `MAX_POSTS_PER_THREAD`.

#### Effect

Post is added to thread.

### Update Post

**Parameters**

| Name       | Description              |
| ---------- | ------------------------ |
| `proposal` | Identifier for proposal. |
| `post`     | Identifier for post.     |
| `text`     | New post text.           |

#### Conditions

* `proposal` corresponds to an existing proposal in where discussion is active, that is either the proposal is active, or no more than `DISCUSSION_LINGERING_DURATION` blocks have passed since it became inactive.
* `post` corresponds to an existing post on proposal.
* author of post corresponds to signer.

Note that editing is possible, regardless of mode, so long as the `author` is owner.

#### Effect

Update text of post.

### Change Thread Mode

**Parameters**

| Name        | Description                             |
| ----------- | --------------------------------------- |
| `proposer`  | Identifier for proposal.                |
| `member_id` | Identifier of member initiating action. |
| `mode`      | New discussion mode.                    |

#### Conditions

* `proposal` corresponds to an existing proposal in where discussion is active, that is either the proposal is active, or no more than `DISCUSSION_LINGERING_DURATION` blocks have passed since it became inactive.
* signer corresponds to member identified with `member_id`
* member is either proposal author or council member.
* `mode` respects `MAX_WHITELIST_SIZE`.

#### Effect

Update thread discussion mode to `mode`.

### Create Blog Post

**Parameters**

| Name    | Description            |
| ------- | ---------------------- |
| `title` | Title of the blog post |
| `text`  | Text of the blog post  |

#### Creation Conditions

None.

#### Execution Conditions

None.

#### Effect

A blog post is created.

### Veto Proposal

**Parameters**

| Name          | Description              |
| ------------- | ------------------------ |
| `proposal_id` | Identifier for proposal. |

#### Creation Conditions

None.

#### Execution Conditions

* Proposal corresponding to `proposal_id` is either in Vote period, Grace period or pending constitution.

#### Effect

* Proposal corresponding to `proposal_id` is automatically discarded.
