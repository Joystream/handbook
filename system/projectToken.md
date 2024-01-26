---
description: Financial and marketing super powers for content creators
---

# 🪙 Creator Tokens

## Introduction

Gives token-like functionality for a content creator to capitalize on his channel and popularity.\
A token works similarly to shares of a company, meaning that holders can claim the channel's profit (via revenue split), but also it can be transferred between accounts and exchanged for $JOYs. From now on we'll denote by the word CRT the token ecosystem for a particular channel that possesses the functionalities described in this document. A Joystream member who owns (or has owned in the past) some non-zero amount of tokens for a particular project or channel is referred to as a CRT account (or a CRT holder).

## Concepts

### Token Supply

Tokens are minted and burned due to issuance and burning events, made possible by the CRT ecosystem. The number of tokens outstanding for a particular channel/project will be called _Total Supply_ throughout the document and it will denote the number of tokens that have been minted minus the tokens that have been burned since the particular CRT instance has been issued by the Content Creator.

### Permissioned and Permissionless Mode

A particular Token can be labeled at any time as either _Permissioned_ or _Permissionless_. Permissioned mode allows for transfers only between selected accounts. Only the Token issuer can change a mode from Permissioned to Permissionless. When Permissionless mode is activated it stays active forever. As mentioned in the account section, an account can be dusted by anyone in permissionless mode and only by its Joystream controller member in permissoned mode. If a CRT is issued in permissioned mode then the Issuer can also specify a particular whitelist of members that are allowed to create a CRT account for themselves and thus interact with the pallet functionalities via `join_whitelist` extrinsic.

### Account

Denotes the information about the number of tokens that a particular Joystream member holds. There are different types of balances in a CRT account according to their usage:

* _Transferrable balance_: denotes the amount that can be transferred at any time (i.e. liquidity)
* _Vested balance_: the amount that is due but not yet credited and is subjected to a vesting schedule
* _Staked balance_: the amount that is not accessible due to staking (locking funds for a certain period) The total amount for an account is the following quantity: $$\text{totalBalance}= \text{transferrableBalance} + \max(\text{stakedBalance}, \text{vestedAmount})$$ (This is because we allow vested tokens to be used for staking as it will be explained later).\
  When an account is created a _Bloat Bond_ for on-chain storage protection must be deposited into the CRT treasury account. Dusting refers to the process of removing the information for an account from the on-chain storage state. An account can be dusted when its Total Balance is equal to zero and one of the following is satisfied:
* Token mode is Permissionless
* Token mode is Permissioned and the user doing the dusting is the Joystream member controller for that account. Whoever does the dusting gets accredited with the associated bloat bond for the account removed.

### Vesting schedule

An account can be credited with tokens directly and the transferrable balance is increased as a consequence, or through vesting. An account upon whom a vesting schedule is pending is said to be vested. A vesting schedule is specified by the following parameters:

* `cliff_amount`: the amount that is assigned immediately to the transferrable balance of an account
* `start`: start of the schedule vesting period
* `end`: end of the schedule vesting period Crediting a given `amount` through vesting works in the following way:
* first, a certain `cliff_amount` is assigned to the transferrable balance
* the remaining `amount - cliff_amount` is uniformly distributed over the period specified by the `start, end` parameters

### Issuing a token

The content creator (herein called _Token Issuer_) can issue a CRT. The act of issuing a token is called token issuance and it requires the issuer to specify the following parameters:

* `patronage_rate`: rate for the patronage functionality, which allows the token Issuer to mint tokens into his account according to such rate.
* `initial_allocation`: a mapping between Joystream members and their transferrable balance, specifying who receives what at issuance.
* `revenue_split_rate`: percentage of channel profit that a CC can retain for himself in a revenue split distribution.
* `symbol`: ticker for the Token.
* `transfer_policy`: whether to allow a transfer only between a selected group of accounts (_Permissioned_ mode) or not (_Permissionless_). In case a CRT is issued as _Permissioned_ an initial whitelist containing the selected accounts must be specified.

### Transferring Tokens

Transfer denotes the act of moving a given token amount (which can be zero) from one sender to one or more receiver CRT accounts. The are two possible ways for transferring tokens: `issuer_transfer`: when the sender is the Token Issuer, in which case the receiver can be any Joystream member `transfer`: when the sender is not the token Issuer and in which case the receiver must be a valid CRT account. In case the receiver doesn't have an account a new one will be automatically created and it is up to the issuer to pay the bloat bond for each created account.\
During a issuer, transfer tokens can be both credited to the receiver transferrable balance and vested, meanwhile during a simple transfer amounts are credited to the recipients' transferrable balance. The maximum amount of recipients regardless of the type of transfer is specified by the `MAX_OUTPUTS` constant.

### Patronage

The patronage functionality allows the token issuer to claim a certain percentage of the current supply. The claim can be exercised at any time and the patronage amount will be minted into the token issuer account. The amount of tokens minted through patronage is computed according to:

$$
\text{patronageAmount} = \text{totalSupply} ( \times (1 + \text{patronageRate})^{c} - 1 )
$$

with

$$
c = \frac{blocksSinceLastPatronageClaim}{blocksInAYear}
$$

The `patronage_rate` can range from $0$ to a certain upper bound set by the governance. It can be also reduced at any given time by the Token Issuer, in this case, the patronage rate used for computing the patronage amount will be the latest value set.

### Revenue split

Allows the Token issuer to dispense a certain amount of $JOY between himself (called _Issuer Amount_) and CRT accounts (called _Revenue Allocation_) in a predefined time window. Is up to the token issuer to start a revenue split at any given time (provided that there's no other ongoing) in which case he will receive his Issuer Amount immediately, the remaining Revenue Allocation amount is thus destined for CRT accounts. At any time since the start of the revenue split any CRT holder willing to participate can stake some of his token (both from his transferrable and vesting balance) to participate in the revenue split and claim some JOYs (referred to as _JOY Dividend_). The tokens will remain staked until the split is ended and it is up to the CRT holders to unstake their tokens via the appropriate extrinsic. In particular, the JOY Dividend amount is transferred to the CRT holders' JOY balance upon staking and according to the following formula:

$$
\text{JOYDividend} = \frac{\text{TokensStaked}}{\text{TotalSupply}} \times \text{RevenueAllocation}
$$

### Token Sale

Allows the Token issuer to sell part of his allocation to any Joystream Member. A sale can be started at any given time (provided that there are no other ongoing sales) by the Issuer who has to specify the following:

* a particular amount of Tokens to sell
* and a start, end block number pair to identify a time window over which the sale is going to be held (herein referred to as _Sale Timeline_).
* a unit sale price
* (optional) parameters for vesting the token purchased during the sale The sale timeline can be updated by the issuer at any time prior to the starting block. Once a sale has started any Joystream member can purchase tokens at the given sale price, the purchased amount can be credited to the transferrable balance or it can be vested. A CRT account is created in case the purchaser doesn't have one yet, and in that case, the purchaser is required to deposit the bloat bond for the account. A sale can be auto-finalized, meaning that once the tokens allocated for the sale have been fully sold the sale is automatically closed and finalized, alternatively, the Issuer can close an ended sale and get any amount of token left over.

### AMM

This type of sale is best thought of as an automated market maker (AMM) which users can buy from and sell tokens at a variable unit price. The sale has an indefinite duration and it can be started immediately at any time by the Token Issuer. Two possible operations are possible in this AMM scenario:

* a `buy` operation, through which any Joystream member can have new Tokens minted into his transferrable balance effectively and immediately in exchange for JOYs (in case of a member not having a CRT account yet the mechanics are the same as in the standard Token Sale). The JOY proceedings from the minting operation are deposited into an internally managed AMM account.
* a `sell` operation, through which any CRT account can sell some of its transferrable balance to the AMM and get some AMM treasury JOYs in exchange. A sell operation is no longer possible if the AMM treasury account is empty. Tokens sold to the AMM are burned. The amount of tokens outstanding from all AMM buy/sell sale operations is referred to as the _AMM-Provided Supply_, which is a subset of the Total supply denoting the number of tokens that have been minted minus the tokens that have been burned by the AMM since its activation. The unit price for each token bought/sold on the AMM is computed using the following formula:

$$
\text{AMMprice} = a \times \text{AMMProvidedSupply} + \text{initialPrice}
$$

Where _Initial Price_ and $a$ are respectively the first price and sensitivity parameter the Issuer sets upon AMM activation.

The AMM Sale can be finally closed at any given time by the Issuer provided that the following condition holds: $$\text{AMMProvidedSupply} \le \text{TotalSupply} \times \text{Threshold}$$ Where `THRESHOLD` is a governance-set percentage. Notice that if `THRESHOLD = 0` then every token minted through the AMM must be also burned for the AMM sale to be closed.

## Parameters

| Name                       | Type          | Description                                                           |
| -------------------------- | ------------- | --------------------------------------------------------------------- |
| `BloatBond`                | `Balance`     | Bloat bond value used during account creation                         |
| `MinSaleDuration`          | `BlockNUmber` | Minimum duration of a token sale                                      |
| `MinRevenueSplitDuration`  | `BlockNumber` | Minimum duration for a revenue split                                  |
| `SalePlatformFee`          | `Permill`     | Platform fee percentage charged on top of each sale and burned        |
| `AMMDeactivationThreshold` | `Permill`     | maximum AMMSupply/TotalSupply ration allowed for deactivating the AMM |
| `AMMBuyTxFees`             | `Permill`     | Percentage of fees charged on top of each token purchase from the AMM |
| `AMMSellTxFees`            | `Permill`     | Percentage of fees charged on top of each token sold to the AMM       |
| `MaxYearlyPatronageRate`   | `Permill`     | Maximum patronage rate allowed                                        |

## Constants

| Name                    | Description                                    | Value     |
| ----------------------- | ---------------------------------------------- | --------- |
| `PalletId`              | Identifier for the pallet                      | `fill-in` |
| `JoyExistentialDeposit` | Existential deposit for the JOY account        | `fill-in` |
| `BlocksPerYear`         | (Average) number of blocks finalized in a year | `fill-in` |
| `MaxOutputs`            | Max number of receivers for a single transfer  | `fill-in` |

## Metadata

Add data later.

## Extrinsics

### Issue Creator Token

* Name: `issue_creator_token`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Init Creator Token Sale

* Name: `init_creator_token_sale`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Update Upcoming Creator Token Sale

* Name: `update_upcoming_creator_token_sale`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Creator Token Issuer Transfer

* Name: `creator_token_issuer_transfer`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Make Creator Token Permissionless

* Name: `make_creator_token_permissionless`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Reduce Creator Token Patronage Rate

* Name: `reduce_creator_token_patronage_rate_to`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Claim Creator Token Patronage Credit

* Name: `claim_creator_token_patronage_credit`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Issue Revenue Split

* Name: `issue_revenue_split`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Finalize Revenue Split

* Name: `finalize_revenue_split`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Finalize Creator Token Sale

* Name: `finalize_creator_token_sale`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Deissue Creator Token

* Name: `deissue_creator_token`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Activate AMM

* Name: `activate_amm`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Deactive AMM

* Name: `deactivate_amm`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**

### Creator Token Issuer Remark

* Name: `creator_token_issuer_remark`
* Pallet: `content`

#### Parameters

**WIP**

#### Conditions

**WIP**

#### Effect

**WIP**





