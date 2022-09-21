---
description: Who is given what, for what reason at what time?
---

# 🤑 Testnet Rewards

## :flag\_us: US persons are not eligible for $JOY :flag\_us:

## Overview

{% embed url="https://www.youtube.com/watch?v=GKdtdgp9EWs" %}

## Introduction

There are two kinds of rewards associated with testnet participation.

1. The first is $tJOY, described here [usdtjoy.md](usdtjoy.md "mention") , which is the native token of our testnets. Although it was possible to exchange this for USD this is no longer possible. Although JSG may still choose to send users BCH directly as a reward for participation or running infrastructure.
2. The second is $JOY, described here [usdjoy.md](../usdjoy.md "mention"), which is the native token of our coming mainnet. This tokens are distributed as part of our Founding Member Program (FMP), described here [founding-member-program](founding-member-program/ "mention"), which is our program to reward high value community member with our mainnet token.

## Council Period Cadence

The cadence of the Joystream testnet revolves around council periods, read more about council periods here [council-period-scoring](council-period-scoring/ "mention").&#x20;

There is always a chance that an election cycle will not end in electing a Council. This can happen in any of three stages:

* If, during the _Announcing_ stage,  there are less than `CouncilSize+MinNumberOfExtraCandidates` candidates, the cycle will end and there will be a new _Announcing_ stage instead of _Voting_.
* If, during the Voting stage, there are less than `CouncilSize` votes made, the cycle will end and there will be a new _Announcing_ stage instead of _Revealing_.
* If, during the _Revealing_ stage, less then `CouncilSize` candidates receive (revealed) votes, the cycle will end and there will be a new _Announcing_ stage instead of a new Council.&#x20;

Currently, the `CouncilSize` is 5, and the `MinNumberOfExtraCandidates` is 1. The election stages are all 14400 blocks \~24 hours.

## Council Period Parameters

Each council period a set of key parameters are updated, and these are critical for determining how much each activity will be rewarded, and under what terms.

| Name                  | Description                                                                            |
| --------------------- | -------------------------------------------------------------------------------------- |
| `JOY_BUDGET`          | Total $JOY available to be rewarded for all activities, except referring a friend.     |
| `REFERRER_JOY`        | $JOY rewarded to someone who referred someone when that person was verified.           |
| `REFERREE_JOY`        | $JOY rewarded to someone who was referred when verified.                               |
| `tJOY_BUDGET`         | Total $tJOY which can be spent by DAO across all activities.                           |
| `CAP`                 | Limit for how much $JOY can be earned by unverified person.                            |
| `COUNCIL_tJOY_REWARD` | The council member reward in $tJOY how much each council member makes, as reward rate. |

## Activity Rewards

Here we cover how different kinds activities are rewarded

### Refer A Friend

Read more in section [#refer-a-friend](founding-member-program/#refer-a-friend "mention").

### Bounties

Each bounty has an associated $tJOY budget, which is the maximum amount one may earn by completing is successfully. One may also end up earning less if the delivery is deemed partially complete in terms of scope or quality. There is also a $JOY reward associated with completing bounties, specifically, it is a share of the `JOY_BUDGET` for the council period in which the bounty was funded (not the period where delivery was made!) which is equal to the share the $tJOY amount awarded makes up of the `tJOY_BUDGET` for the period the bounty started.

Only bounties created by the Human Resources working group will count towards the `JOY_BUDGET`. More information on this process can be found in the [#bounty-management](council-period-scoring/human-resources-score.md#bounty-management "mention") section of the [human-resources-score.md](council-period-scoring/human-resources-score.md "mention").

### Leads

They earn a $tJOY reward linearly over time at a rate decided by the council. Leads for different groups can, and likely will, have distinct reward rates, as seen in [this dashboard](http://joystream.org/dashboard).

Leads earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`.

### Workers

They earn a $tJOY reward linearly over time at a rate decided by the council. Leads for different groups can, and likely will, have distinct reward rates, as seen in [this dashboard](http://joystream.org/dashboard).

Leads earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`.

### Validators

Validators earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`.

Note that unless you use either your `membershipRoot` or `membershipController` key as your validator stash or controller key, we will not be able to link the two, and your earnings here will not be registered! If your keys are linked to two different memberships, **neither** will be eligible for $JOY rewards.

### Funding Requests

By default, the recipient of funding request will earn $JOY allocations in the same way as for bounty contributions: a share of the `JOY_BUDGET` equal to what share the earned $tJOY makes up of the `tJOY_BUDGET`. Note that, like with [#validators](testnet-rewards.md#validators "mention"), unless the recipient account is the `membershipRoot` or `membershipController` , we will not able to the recipient, and no $JOY will be allocated.

This can also be utilized if the council wishes to re-imburse someone, or for other reason pay someone $tJOY, but not $JOY.

### Council Member

All council members earn the same quantity of $tJOY per period, let `TOTAL_COUNCIL_tJOY_REWARD` denote the total $tJOY payout earned by the entire council. This value is controlled by Jsgenesis, and can change over time.

Council Members earn $JOY a bit differently, specifically, the total $JOY amount shared equally among all members are reduced by what is called the _network peformance score,_ squared, as shown below:

```
TOTAL_COUNCIL_JOY_REWARD = JOY_BUDGET * (TOTAL_COUNCIL_tJOY_REWARD/tJOY_BUDGET) * NETWORK_PERFORMANCE_SCORE^2
```

where `NETWORK_PERFORMANCE_SCORE`, and is in the interval \[0, 1]. This score, computed by Jsgenesis using public evaluation metrics, attempts to capture how well the network performed. The evaluation metrics will change from one council period to the next.



### Content Creator

`<Coming>`
