# 💰 Channel Payouts
## Introduction
The council may find it appropriate to reward some channels based on various merits, such as most viewed content, etc... The payout functionality allows the channel owner (or a content actor with sufficient permission) to cash out a particular sum of JOY rewarded by the council to the channel
## Concepts
### Payout & Payouts Commitment
The amount of $JOY the council has decided to award to a particular channel at a particular point in time. 
New payouts will be added as time passes via council proposal. By cumulative payout earned, we will refer to the cumulative amount of payout awarded by the council to a particular channel since the genesis block.
Herein we will refer to as payment element the triple consisting of:
- channel id
- cumulative payout earned
- human-readable reason for the latest payout added
At any given time the set of payment elements (representing the channel awarded by the council with the respective payout amounts) is stored in the content pallet chain state as Merkle proof root hash. This value is called payouts commitment
#### Claim
The action of the channel owner (or a delegate) to claim and cash out the payout. The delegate can be whoever has sufficient permission to perform this action. From here on we'll say that a claim is made by the channel to avoid distinguishing between owner & non-owner.
The channel can claim the amount via Merkle proof verification. In particular, the claiming at a particular block height is allowed if:
1. The payment element provided by the channel must be verified via Merkle proof verification against the commitment stored on the chain state 
2. The claiming channel must not have `CreatorCashout` among its paused features
3. The payout amount must be in the range `[MinCashoutAllowed, MaxCashoutAllowed]` (see param section)
4. The channel is not being transferred to another owner
5. The actor doing the claiming has sufficient permissions, as explained previously
## Parameters
The following are mutable parameters updated via council proposal
| Name | Type | Description |
|---------|---------|----------------|
|`PayoutsCommitment` | `Hash` |Payouts commitment hash value at any given time |
| `MinCashoutAllowed` | `Balance` | Minimum amount of JOY a channel is allowed to cash out at any given time|
| `MaxCashoutAllowed` | `Balance` | Maximum amount of JOY a channel is allowed to cash out at any given time|
| `CashoutEnabled` | `boolean` | Whether payout claiming is enabled or not | 
## Constants
The following constants are hard coded into the system, and they can only be changed via runtime upgrade
| Name | Description | Value |
|----------|----------------|----------|
| `MIN_CASHOUT_ALLOWED` | minimum payout amount that a channel is allowed to cash out | `fill-in` | 
| `MAX_CASHOUT_ALLOWED` | maximum payout amount that a channel is allowed to cash out | `fill-in` | 
| `CHANNEL_CASHOUTS_ENABLED` |  Whether payout claiming is enabled or not | `TRUE` | 
## Extrinsics