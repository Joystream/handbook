---
description: Scaleable governance powered creator payouts
---

# 💸 Creator Payouts

## Introduction

The council may find it appropriate to reward some channels based on various merits, such as most viewed content, etc... The payout functionality allows the channel owner (or a content actor with sufficient permission) to cash out a particular sum of JOY rewarded by the council to the channel. This document will discuss the runtime design of it. For how to steps please refer to [gleev documentation](https://joystream.notion.site/Gleev-Operation-2ee6319c7688464c8800ecbfa3b17abd#0ca570ef32cc4226b8289503551f343e)

## Concepts

### Payout & Payouts Commitment

By payout amount we mean the amount of $JOY the council has decided to award to a particular channel at a particular point in time. New payouts will be added as time passes via council proposals. By cumulative payout earned, we will refer to the cumulative amount of payouts awarded by the council to a particular channel since the genesis block. Herein we will refer to as _payment element_ the triple consisting of:

* channel id
* cumulative payout earned
* human-readable reason for the latest payout added At any given time the set of payment elements (representing the channel awarded by the council with the respective payout amounts) is stored in the content pallet chain state as its Merkle proof root hash. This value is called _payouts commitment_

#### Claim

By claim we refer to the action of the channel owner (or a delegate) to claim and cash out the payout. The delegate can be whoever has sufficient permission to perform this action. From here on we'll say that a claim is made by the channel to avoid distinguishing between owner & non-owner. The channel can claim the amount via Merkle proof verification. In particular, the claiming at a particular block height is allowed if:

1. The payment element provided by the channel must be verified via Merkle proof verification against the payouts commitment value
2. The claiming channel must not have `CreatorCashout` among its paused features
3. The payout amount must be in the range `[MinCashoutAllowed, MaxCashoutAllowed]` (see param section)
4. The channel is not being transferred to another owner
5. The actor doing the claiming has sufficient permissions, as explained previously. Specific permission references are described in the next section

## Parameters

The following are mutable parameters updated via council proposal

| Name                | Type      | Description                                                              |
| ------------------- | --------- | ------------------------------------------------------------------------ |
| `PayoutsCommitment` | `Hash`    | Payouts commitment hash value at any given time                          |
| `MinCashoutAllowed` | `Balance` | Minimum amount of JOY a channel is allowed to cash out at any given time |
| `MaxCashoutAllowed` | `Balance` | Maximum amount of JOY a channel is allowed to cash out at any given time |
| `CashoutEnabled`    | `boolean` | Whether payout claiming is enabled or not                                |

## Constants

The following constants are hard coded into the system, and they can only be changed via runtime upgrade

| Name                       | Description                                                 | Value     |
| -------------------------- | ----------------------------------------------------------- | --------- |
| `MIN_CASHOUT_ALLOWED`      | minimum payout amount that a channel is allowed to cash out | `fill-in` |
| `MAX_CASHOUT_ALLOWED`      | maximum payout amount that a channel is allowed to cash out | `fill-in` |
| `CHANNEL_CASHOUTS_ENABLED` | Whether payout claiming is enabled or not                   | `TRUE`    |

## Extrinsics

### Payout Parameters Update

Allows the council to update parameters that regulate the action of claiming a payout via a proposal. This also allows the council to set a new value for the payouts commitment, thus endowing new payouts to channels

**Parameters**

| Name                                    | Descripion                                                                                                      |
| --------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `new_payout_commitment`                 | hash for the merkle root (optional)                                                                             |
| `object_creation_list`                  | list of `(ipfs_id, object_mb_size)` containing information about object size and creation                       |
| `uploader_account`                      | account from which all the expenses for the storage upload are charged to                                       |
| `expected_data_size_fee`                | expected price for mb, must match the `storage-pallet::data_size_fee` value                                     |
| `expected_data_object_state_bloat_bond` | expected bloat bond for storage occupation. Must match the `storage-pallet::data_object_state_bloat_bond` value |
| `new_min_cashout_allowed`               | minimum amount that a channel is allowed to cash out (optional)                                                 |
| `new_max_cashout_allowed`               | maximum amount that a channel is allowed to cash out (optional)                                                 |
| `channel_cashouts_enabled`              | whether or not to enable the channel payouts functionality (optional)                                           |

#### Condition

* `min_cashout_allowed <= new_max_cashout_allowed` must be respected or `new_min_cashout_allowed <= new_max_cashout_allowed` if both are specified
* `new_min_cashout_allowed <= max_cashout_allowed` must be respected or `new_min_cashout_allowed <= new_max_cashout_allowed` if both are specified
* `new_min_cashout_allowed <= MINIMUM_CASHOUT_ALLOWED_LIMIT` if specified
* `new_max_cashout_allowed <= MAXIMUM_CASHOUT_ALLOWED_LIMIT` if specified
* `origin` must be root, i.e. the extrinsic must be dispatched via proposal
* `storage-pallet::upload_data_objects` preconditions must be verified
* `uploader_account` should be some account i.e. council #out-of-process or the proposer member controller account

#### Effect

* `max_cashout_allowed` set to `new_max_cashout_allowed` if this last value is specified
* `min_cashout_allowed` set to `new_min_cashout_allowed` if this last value is specified
* `channel_cashouts_enabled` updated to the the new value (if specified)
* `commitment` value updated to `new_commitment` if specified
* `storage-pallet::upload_parameters(params)` effects are taken in place where `params` is specified as follows:
  * `bag_id` is the Council Static Bag
  * `object_creation_list` is the `payload_params.object_creation_list`
  * `bloat_bond_source_account_id` is the `payload_params.uploader_account`
  * `expected_data_size_fee` is the `payload_params.expected_data_size_fee`
  * `expected_data_object_state_bloat_bond` is the `payload_params.expected_data_object_state_bloat_bon`

### Channel Reward Claim

Allow a channel to claim a `payout` and have the $JOYs deposited into its `reward_account`

**Parameters**

| Name                | Description                                                                                                                                                 |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actor`             | either a member, lead or curator claiming the `payout`                                                                                                      |
| `proof`             | merkle proof used for verifying whether the `payout` the channel is claiming is legit or not                                                                |
| `pull_payment_item` | the information containing the `payout` plus some other data used in the validation process and also the `channel_id` for which the `payout` is destined to |

#### Condition

* `channel_id`: must refer to an existing `channel`
* `channel`: must not have the `CreatorCashout` feature paused
* `actor`: must be endowed with a `RewardChannelReward` permission
* `channel_cashout_enabled`: must be `true`
* `channel_total_cashout + payout` amount of $JOY must be in the closed interval `[min_cashout_allowed,max_cashout_allowed]`
* `channel_total_cashout + payout` amount of $JOY must be transferrable from the Council Budget
* `pull_payout_element` must verify the [merkle proof](payout.md#merkle-proof) mechanism

#### Effect

* `payout` amount of $JOY is transferred from the Council Budget usable balance into the `reward_account` usable balance
* `cumulative_channel_reward` for channel `channel_id` is increased by `payout`

### Claim And Withdraw Channel Reward

Allow a channel to claim a `payout` and have the $JOYs deposited into the controller account if the channel is member-owned otherwise funds go into the Council Budget for non member-owned channels

**Parameters**

| Name                | Description                                                                                                                                                 |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `actor`             | either a member, lead or curator claiming the `payout`                                                                                                      |
| `proof`             | merkle proof used for verifying whether the `payout` the channel is claiming is legit or not                                                                |
| `pull_payment_item` | the information containing the `payout` plus some other data used in the validation process and also the `channel_id` for which the `payout` is destined to |

#### Condition

* `channel_id`: must refer to an existing `channel`
* `channel`: must not have the `[CreatorCashout, ChannelFundTransfer]` features paused
* `actor`: must be endowed with `[RewardChannelReward,WithDrawFromChannelBalance]` permissions
* `channel_cashout_enabled`: must be `true`
* `channel_total_cashout + payout` amount of $JOY must be in the closed interval `[min_cashout_allowed,max_cashout_allowed]`
* `channel_total_cashout + payout` amount of $JOY must be transferrable from the Council Budget
* `pull_payout_element` must verify the [merkle proof](payout.md#merkle-proof) mechanism

#### Effect

* `payout` amount of $JOY is transferred from the Council Budget usable balance into the `reward_account` usable balance first. After that they are transferred from the `reward_account` into the `destination_account` in the following fashion:
  * if channel is member-owned then the `payout` amount is transferred into the member controller account usable balance
  * if channel is curator/lead-owned the `payout` amount is burned from the `reward_account` and minted into the Council budget Account
* `cumulative_channel_reward` for channel `channel_id` is increased by `payout`
