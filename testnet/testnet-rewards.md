---
description: Who is given what, for what reason at what time?
---

# 🤑 Testnet Rewards

## &#x20;:flag\_us: US persons are not eligible for $JOY :flag\_us:

## Introduction

There are two kinds of rewards associated with testnet participation.&#x20;

1. The first is $tJOY, described here [usdtjoy.md](usdtjoy.md "mention") , which is the native token of our testnets, and which can be used to redeem for $USD at any time.
2. The second is $JOY, described here [usdjoy.md](../usdjoy.md "mention"), which is the native token of our coming mainnet. This tokens are distributed as part of our Founding Member Program (FMP), described here [founding-member-program.md](founding-member-program.md "mention"), which is our program to reward high value community member with our mainnet token.

## Council Period Cadence

The cadence of the Joystream testnet revolves around council periods, read more about council periods here [council-period-scoring](council-period-scoring/ "mention").

1. No later than 12 hours after a the first election of a council period is over is is a council supposed to deliver the [#council-period-summary](council-period-scoring/#council-period-summary "mention")and all working group leads to deliver their [#working-group-summary](council-period-scoring/general-working-group-score.md#working-group-summary "mention") to Jsgenesis.
2. Jsgenesis announced the [#council-period-parameters](testnet-rewards.md#council-period-parameters "mention")no later than 12 hours after the last election is completed.\*
3. No later than 24 hours after the last election is completed is the council supposed to deliver the [#council-period-plan](council-period-scoring/#council-period-plan "mention") and all working group leads to deliver their [#working-group-period-plan](council-period-scoring/general-working-group-score.md#working-group-period-plan "mention") to Jsgenesis.

\* Notice that in principle there could be more than one election in a row if there is failure, this is why there is a distinction with first and last in the steps above.

## Council Period Parameters

Each council period a set of key parameters are updated, and these are critical for determining how much each activity will be rewarded, and under what terms.

| Name                  | Description                                                                                        |
| --------------------- | -------------------------------------------------------------------------------------------------- |
| `JOY_BUDGET`          | Total $JOY available to be rewarded for all activities, except referring a friend.                 |
| `REFERRAL_JOY_AMOUNT` | $JOY rewarded for referring a friend, per friend.                                                  |
| `tJOY_BUDGET`         | Total $tJOY which can be spent by DAO across all activities.                                       |
| `USD_SUBSIDY`         | The USD value which is added to the backing value of $tJOY at the beginning of the council period. |
| `REFERRALS_LIMIT`     | Max number of referrals that can be rewarded with $JOY during a council period.                    |
| `CAP`                 | Limit for how much $JOY can be earned by unverified person.                                        |
| `COUNCIL_tJOY_REWARD` | The council member reward in $tJOY how much each council member makes, as reward rate.             |

## Activity Rewards

Here we cover how different kinds activities are rewarded

### Refer A Friend

For a given council period, the first `REFERRALS_LIMIT` number of members who get verified and who were invited, then result in `REFERRAL_JOY_AMOUNT`  amount of $JOY for the invitor. The reward occurs on a first-come-first-serve basis, so if the limit has already been reached in a given period, then opportunity to receive $JOY for this invitation is permanently lost. Read more in section [#refer-a-friend](founding-member-program.md#refer-a-friend "mention").

### Bounties

Each bounty has an associated $tJOY budget, which is the maximum amount one may earn by completing is successfully. One may also end up earning less if the delivery is deemed partially complete in terms of scope or quality. There is also a $JOY reward associated with completing bounties, specifically, it is a share of the `JOY_BUDGET` for the council period in which work on the bounty sd (not the period where delivery was made!) which is equal to the share the $tJOY amount awarded makes up of the `tJOY_BUDGET` for the period the bounty started.

### Leads

They earn a $tJOY reward linearly over time at a rate decided by the council. Leads for different groups can, and likely will, have distinct reward rates, as seen in [this dashboard](http://joystream.org/dashboard).

Leads earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`.

### Workers

They earn a $tJOY reward linearly over time at a rate decided by the council. Leads for different groups can, and likely will, have distinct reward rates, as seen in [this dashboard](http://joystream.org/dashboard).

Leads earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`.

### Validators

Validators earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`.

### Council Member

All council members earn the same quantity of $tJOY per period, let `TOTAL_COUNCIL_tJOY_REWARD` denote the total $tJOY payout earned by the entire council.  This value is controlled by Jsgenesis, and can change over time.&#x20;

Council Members earn $JOY a bit differently, specifically, the total $JOY amount shared equally among all members is given by\
\
`(TOTAL_COUNCIL_tJOY_REWARD/tJOY_BUDGET)*(NETWORK_PERFORMANCE_SCORE)^2`\
\
where `NETWORK_PERFORMANCE_SCORE` is called the _network performance score_, and is in the interval \[0, 1]. This score, computed by Jsgenesis using public evaluation metrics, attempts to capture how well the network performed. The evaluation metrics will change from one council period to the next.

### Content Creator

`<Coming>`

