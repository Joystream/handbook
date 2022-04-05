---
description: Who is given what, for what reason at what time?
---

# 🤑 Testnet Rewards

## :flag\_us: US persons are not eligible for $JOY :flag\_us:

## Introduction

There are two kinds of rewards associated with testnet participation.

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
| `REFERRER_JOY`        | $JOY rewarded to someone who referred someone when that person was verified.                       |
| `REFERREE_JOY`        | $JOY rewarded to someone who was referred when verified.                                           |
| `tJOY_BUDGET`         | Total $tJOY which can be spent by DAO across all activities.                                       |
| `USD_SUBSIDY`         | The USD value which is added to the backing value of $tJOY at the beginning of the council period. |
| `CAP`                 | Limit for how much $JOY can be earned by unverified person.                                        |
| `COUNCIL_tJOY_REWARD` | The council member reward in $tJOY how much each council member makes, as reward rate.             |

## Activity Rewards

Here we cover how different kinds activities are rewarded

### Refer A Friend

Read more in section [#refer-a-friend](founding-member-program.md#refer-a-friend "mention").

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

All council members earn the same quantity of $tJOY per period, let `TOTAL_COUNCIL_tJOY_REWARD` denote the total $tJOY payout earned by the entire council. This value is controlled by Jsgenesis, and can change over time.

Council Members earn $JOY a bit differently, specifically, the total $JOY amount shared equally among all members are reduced by what is called the _network peformance score,_ squared, as shown below:

```
TOTAL_COUNCIL_JOY_REWARD = JOY_BUDGET * (TOTAL_COUNCIL_tJOY_REWARD/tJOY_BUDGET) * NETWORK_PERFORMANCE_SCORE^2
```

where `NETWORK_PERFORMANCE_SCORE`, and is in the interval \[0, 1]. This score, computed by Jsgenesis using public evaluation metrics, attempts to capture how well the network performed. The evaluation metrics will change from one council period to the next.

### Content Creator

`<Coming>`


## Scoring and Reward Example
To clarify how the scoring and rewards works, here is straightforward example.
Note that the inputs are somewhat random, so don't set your expectations based on them.

### Council Period Parameters and weights
| Name                  | Value                     |
| --------------------- |:-------------------------:|
| `JOY_BUDGET`          | 2,000,000/0.2%/USD120,000 |
| `USD_SUBSIDY`         | 2,000                     |
| `tJOY_BUDGET`         | 80,000,000                |
| `COUNCIL_tJOY_REWARD` | 10,000,00                 |

| Group                 | Weight                    |
| --------------------- |:-------------------------:|
| `B_W`                 | 5                         |
| `C_W`                 | 3                         |
| `D_W`                 | 6                         |
| `F_W`                 | 1                         |
| `HR_W`                | 5                         |
| `M_W`                 | 2                         |
| `P_W`                 | 2                         |
| `SU_W`                | 2                         |
| `LO_W`                | 1                         |
| `SUM`                 | **27**                    |

### Budget Allocation

Of the tJOY 80M in the budget, we assume tJOY 78M was spent, as shown below:
| Purpose         | Spending [tJOY] | Workers (ex Lead) | Lead [tJOY] | Workers [tJOY] |
|-----------------|:---------------:|:-----------------:|:-----------:|:--------------:|
| Builders        | 15              | 5                 | 3           | 2.4            |
| Content         | 10.5            | 6                 | 1.8         | 1.45           |
| Distributor     | 17              | 8                 | 3           | 1.75           |
| Forum           | 3               | 2                 | 1.5         | 0.75           |
| Human Resources | 16              | 20                | 2           | 0.7            |
| Marketing       | 7               | 3                 | 1           | 2              |
| Council         | 6               | 5                 | NA          | 1.2            |
| `SUM`           | **74.5**        | **49**            | **12.3**    | **62.2**       |

### WG Rewards
As the WG rewards are not (directly\*) impacted by their performance, we get the following rewards for the Workers and Leads:

| Purpose         | Spending [MtJOY] | Workers (ex Lead) | Workers [MtJOY] | Workers [JOY] | Workers [USD]   | Lead [MtJOY] | Lead [JOY] | Lead [USD]      |
|-----------------|:----------------:|:-----------------:|:---------------:|:-------------:|:---------------:|:------------:|:----------:|:---------------:|
| Builders        | 15               | 5                 | 2.4             | 60000         | 60 - 3600       | 3            | 75000      | 75 - 4500       |
| Content         | 10.5             | 6                 | 1.45            | 36250         | 36.25 - 2175    | 1.8          | 45000      | 45 - 2700       |
| Distributor     | 17               | 8                 | 1.75            | 43750         | 43.75 - 2625    | 3            | 75000      | 75 - 4500       |
| Forum           | 3                | 2                 | 0.75            | 18750         | 18.75 - 1125    | 1.5          | 37500      | 37.5 - 2250     |
| Human Resources | 16               | 20                | 0.7             | 17500         | 17.5 - 1050     | 2            | 50000      | 50 - 3000       |
| Marketing       | 7                | 3                 | 1.5             | 50000         | 37.5 - 2250     | 2.5          | 62500      | 62.5 - 3750     |
| **SUM**         | **68.5**         | **44**            | **54.7**        | **1367500**   |**1368 - 82050** | **13.8**     | **345000** |**345 - 20700**  |  


### CM Rewards
For the CMs, the tJOY reward is independent of the `NETWORK_PERFORMANCE_SCORE`, whereas the JOY reward is not.

To calculate the `NETWORK_PERFORMANCE_SCORE`, we need the individual groups scores:
**Scores**
| Group              | Weight | Score | Contribution |
|--------------------|:------:|:-----:|:------------:|
| Builders           | 5      | 0.64  | 3.2          |
| Content            | 3      | 0.45  | 1.35         |
| Distributor        | 6      | 0.8   | 4.8          |
| Forum              | 1      | 0.5   | 0.5          |
| Human Resources    | 5      | 0.6   | 3            |
| Marketing          | 2      | 0.44  | 0.88         |
| Plan               | 2      | 0.8   | 1.6          |
| Summary            | 2      | 0.6   | 1.2          |
| Lead Opportunities | 1      | 0     | 0            |
| SUM / AVG / SUM    | **27** | 0.537 | 16.53        |

That means:
```
NETWORK_PERFORMANCE_SCORE = 16.53/27 = 0.612
```
This allows us to calculate the total and individual rewards for the Council Members:

```
COUNCIL_JOY_REWARD = JOY_BUDGET * (TOTAL_COUNCIL_tJOY_REWARD/tJOY_BUDGET) * NETWORK_PERFORMANCE_SCORE^2

# denominated in JOY
COUNCIL_JOY_REWARD = JOY 2000000 * (10/80) * 0.612^2 = JOY 93636

# denominated in USD
COUNCIL_JOY_REWARD = USD 120000 * (10/80) * 0.612^2 = USD 5618
```

For the sake of comparison:
| Purpose         | Spending [MtJOY] | Workers (ex Lead) | Workers [MtJOY] | Workers [JOY] | Workers [USD]   | Lead [MtJOY] | Lead [JOY] | Lead [USD]      |
|-----------------|:----------------:|:-----------------:|:---------------:|:-------------:|:---------------:|:------------:|:----------:|:---------------:|
| Builders        | 15               | 5                 | 2.4             | 60000         | 60 - 3600       | 3            | 75000      | 75 - 4500       |
| Content         | 10.5             | 6                 | 1.45            | 36250         | 36.25 - 2175    | 1.8          | 45000      | 45 - 2700       |
| Distributor     | 17               | 8                 | 1.75            | 43750         | 43.75 - 2625    | 3            | 75000      | 75 - 4500       |
| Forum           | 3                | 2                 | 0.75            | 18750         | 18.75 - 1125    | 1.5          | 37500      | 37.5 - 2250     |
| Human Resources | 16               | 20                | 0.7             | 17500         | 17.5 - 1050     | 2            | 50000      | 50 - 3000       |
| Marketing       | 7                | 3                 | 1.5             | 50000         | 37.5 - 2250     | 2.5          | 62500      | 62.5 - 3750     |
| Council         | 10               | 5                 | 2               | 50000         | 50 - 1123.6     | NA           | NA         | NA              |
| **SUM**         | **78.5**         | **49**            | **64.7**        | **1617500**   |**1618 - 87668** | **13.8**     | **345000** |**345 - 20700**  |


If the NETWORK_PERFORMANCE_SCORE was 1:
```
COUNCIL_JOY_REWARD = JOY 2000000 * (10/80) * 1^2 = JOY 250000
COUNCIL_JOY_REWARD = USD 120000 * (10/80) * 1^2 = USD 15000
```

We see the `NETWORK_PERFORMANCE_SCORE` is of major importance to the Council, but not for Workers or Leads \*.
\* Which should make the Council pay close attention to the performance of the groups!
