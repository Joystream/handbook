---
description: Reward what you want to see in the world.
---

# 📏 Council Period Scoring

## Introduction

There needs to be a way to measure how well the system is operating overall, as this is a key signal to the council about whether it is doing a good job or not. Given such a signal, the council would be able to change policies and reallocate resources to increase performance as measured by this signal. On mainnet, the market capitalization of $JOY is effectively this signal, but on testnet we have to find some substitute for this, and that is the role of the _network performance score_.

## Group Scores

{% content-ref url="general-working-group-score.md" %}
[general-working-group-score.md](general-working-group-score.md)
{% endcontent-ref %}

{% content-ref url="content-directory-score.md" %}
[content-directory-score.md](content-directory-score.md)
{% endcontent-ref %}

{% content-ref url="human-resources-score.md" %}
[human-resources-score.md](human-resources-score.md)
{% endcontent-ref %}

{% content-ref url="marketers-score.md" %}
[marketers-score.md](marketers-score.md)
{% endcontent-ref %}

{% content-ref url="storage-providers-score.md" %}
[storage-providers-score.md](storage-providers-score.md)
{% endcontent-ref %}

{% content-ref url="distributors-score.md" %}
[distributors-score.md](distributors-score.md)
{% endcontent-ref %}

{% content-ref url="builders-score.md" %}
[builders-score.md](builders-score.md)
{% endcontent-ref %}

## Previous Scoring Rounds

Here is a live [dashboard](https://joystream.retool.com/embedded/public/3ef6f2ee-7d4d-4437-b5f6-f59c8cb17ff6) where you can look up the results for individuals per scoring period, and overall status.

## Council Period Parameters

| Name                  | Value          |
| --------------------- | -------------- |
| `JOY_BUDGET`          | 1000000 (0.1%) |
| `REFERRER_JOY`        | TBD            |
| `REFERREE_JOY`        | TBD            |
| `tJOY_BUDGET`         | 80,000,000     |
| `USD_SUBSIDY`         | USD 2000       |
| `CAP`                 | TBD            |
| `COUNCIL_tJOY_REWARD` | TBD            |

## Summary Report and Plan Deadlines



For the system to work well, there is a need for a feedback-loop, between

* the councils [#council-period-summary](./#council-period-summary "mention") and the working groups [#working-group-summary](general-working-group-score.md#working-group-summary "mention") are important for Jsgenesis to;
* publish [#council-period-parameters](./#council-period-parameters "mention") (for the next term/scoring period), which are needed for;
* the new councils [#council-period-plan](./#council-period-plan "mention") and working groups [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"). ****&#x20;

For this to be the case, strict deadlines are required. See [#council-period-cadence](../testnet-rewards.md#council-period-cadence "mention") for definitions.

1. No later than 12 hours after the start of the _first_ Revealing stage following the election that set the current council:
   * the council delivers a **temporary** council period summary report
   * all working groups delivers a **temporary** working group summary report
     * based on information and data valid as of the start of the _first_ Revealing stage following the election that set the current council.
2. No later than 12 hours after the a new council is set:
   * the previous council delivers the **final** council period summary report
   * all working groups delivers a **final** working group summary report
     * based on information and data valid as of the block that set a new council
3. No later than 6 hours after a new council is elected, Jsgenesis announces the Council Period Parameters, and notifies this in the `#council` channel on [Discord](https://discord.gg/DE9UN3YpRP).
4. No later than 24 hours after a new council is set:
   * the council delivers the council period plan
   * all working groups delivers working group period plan

## Dashboard

TODO

## Knowledge Bases <a href="#group-knowledge-base" id="group-knowledge-base"></a>

The council and each working group must maintain its own Notion board where a body of knowledge related to the operations of the group are maintained. This base will be owned by Jsgenesis, while on testnet, and the current lead of each working group and all council members will be given write access to maintain it. The integrity of the boards is the responsibility of each person granted access, and sharing of credentials is not allowed. If this constraint causes problems in efficiently maintaining the boards, contact Jsgenesis.

## Council Knowledge Base

{% embed url="https://joystream.notion.site/Council-809dd7bcf6744844ba0dcccf98670dcc" %}
Council Knowledge Base
{% endembed %}

## Total tJOY Spending

The total tJOY spending over a given council period is something Jsgenesis attempts to directly constrain through its policy parameter `tJOY_BUDGET` , and it the sum of the following non-overlapping categories of flows during the blocks of a council period

* Any increase in tJOY that any validator can cashout, but currently has not.
* Any tJOY that has actually been cashed out by validators.
* Any tJOY actually awarded to any council member, lead or worker.
* Any tJOY "owed" to a council member, lead or worker, IF said tJOY is in fact paid out in the NEXT reward period (for the group).
* Any tJOY for spending proposals, except spending to finance on-demand bounties approval by [#human-resources](../../system/working-groups/#human-resources "mention") .
* Any tJOY approved for bounty work.

**Note** that it's not trivial for the Council to keep track of these payments flows themselves. We advise them to pay close attention to the status of missed payments at the start of each term, in addition to "general" budget overview.

## Council Period Summary

### Motivation

* Allow Jsgenesis to update the [#council-period-parameters](../testnet-rewards.md#council-period-parameters "mention") and [#network-performance-score](./#network-performance-score "mention") metrics for the next period based on up to date and accurate information.
* Allow the possible next council to have good information about the most urgent matters and status of the network.

### Scope

* Accounting of how much was spent on what.
* Actual hires made.
* Actual firings done.
* Spending proposals passed.
* Changes made to the notion board.
* A summary on how well the network as a whole performed, and what problems occurred.
* Recommendations for what should be focused on in next council period in order to make the network more effective.
* Feedback on the Council Period Parameters during their term.

### Submission

The report itself must be written as a markdown document in English, in the forum category `Testnet>Council>Summaries` , as a thread which has the title which includes the council period ID. The council must pass a text proposal (add link when proposal list is in) which references the report on the forum.

If there is a need to link to extra information, statistics, etc. these should be in the notion board.

## Council Period Plan

### Motivation

Give Jsgenesis visibility into the priorities of the council, and also serve as a canonical document to focus everyone in the council around a clearly defined plan.

### Scope

* Prioritization to each working group about what they should focus on solving.
* How total $tJOY budget will be allocated across groups and council.

### Submission

The plan itself must be written as a markdown document in English, in the forum category `Testnet>Council>Plans` , as a thread which has the title which includes the council period ID. The council must pass a text proposal (add link when proposal list is in) which references the plan on the forum.

If there is a need to link to extra information, statistics, etc. these should be in the notion board.

## Lead Opportunities

There must be made space for people to try to participate as leads for working group, even to the extent that other more experienced - but proficient leads, have to pause their participation. It is up to the council to determine the cheapest way to accommodate newcomers without undermining the operations of the working group. Not only must the space be allocated and reserved for newcomers, but there must be effective collaboration with the [human-resources.md](../../system/human-resources.md "mention") working group to actually identify potential applicants and encourage them to apply to these opportunities.

## Score

### Overview

At the beginning of each council [#jsgenesis](../../glossary.md#jsgenesis "mention") staff will state a set of explicit metrics that will apply to the upcoming council period. At the end of each council period, [#jsgenesis](../../glossary.md#jsgenesis "mention") staff will determine a final _network performance score_ for the council which will be in the range \[0,1]. This score is used to determine the [usdtjoy.md](../usdtjoy.md "mention") reward and [#founding-member-points](../founding-member-program.md#founding-member-points "mention") for the council members, as described above.

Specifically, the score is a weighted linear combination of scores _working group scores_, which themselves are in the range \[0,1], which is normalized by the weights, and lastly discounted by exponentially by the number of _catastrophic errors_ detected, that is

```
NETWORK_PERFORMANCE_SCORE = [
BUILDER_SCORE*B_W +
MARKETER_SCORE*M_W +
CONTENT_SCORE*C_W +
HR_SCORE*HR_W +
STORAGE_SCORE*S_W +
DISTRIBUTOR_SCORE*D_W +
SUMMARY_SCORE*SU_W +
PLAN_SCORE*P_W +
LO_W*LEAD_OPPORTUNITIES_SCORE
]/((B_W + M_W + C_W + HR_W + S_W + D_W + SU_W + P_W + LO_W)*2^N)
```

where

* `BUILDER_SCORE` (`B_W`): computed with metric defined in [builders-score.md](builders-score.md "mention").
* `MARKETER_SCORE` (`M_W`): computed with metric defined in [marketers-score.md](marketers-score.md "mention").
* `CONTENT_SCORE`(`C_W`): computed with metric defined in [content-directory-score.md](content-directory-score.md "mention").
* `HR_SCORE` (`HR_W`): computed with metric defined in [human-resources-score.md](human-resources-score.md "mention").
* `STORAGE_SCORE` (`S_W`): computed with metric defined in [storage-providers-score.md](storage-providers-score.md "mention").
* `DISTRIBUTOR_SCORE` (`D_W`): computed with metric defined in [distributors-score.md](distributors-score.md "mention").
* `SUMMARY_SCORE` (`SU_W`): is a score computed for the quality of the council summary, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
  * Quality of changes to the knowledge base.
* `PLAN_SCORE` (`P_W`): is a score computed by Jsgenesis staff for the quality of the council plan, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
* `LEAD_OPPORTUNITIES_SCORE` (`LO_W`) is `1/min(x_1,..., x_k)` , which will be in the range \[0, 1], where `x_i` is the total number of council period in which the `i`th lead has worked in this group.
* `B_W,M_W,C_W,HR_W,SP_W,D_W,SU_W,P_W,LO_W` : are the weights from the table below.
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Weights

The current weights are:

<table><thead><tr><th>Weight</th><th data-type="number">Value</th></tr></thead><tbody><tr><td><code>B_W</code></td><td>5</td></tr><tr><td><code>M_W</code></td><td>1</td></tr><tr><td><code>C_W</code></td><td>2</td></tr><tr><td><code>HR_W</code></td><td>3</td></tr><tr><td><code>S_W</code></td><td>5</td></tr><tr><td><code>D_W</code></td><td>6</td></tr><tr><td><code>SU_W</code></td><td>1</td></tr><tr><td><code>P_W</code></td><td>1</td></tr><tr><td><code>LO_W</code></td><td>0</td></tr></tbody></table>

Which Means:

```
NETWORK_PERFORMANCE_SCORE = [
BUILDER_SCORE*B_W +
MARKETER_SCORE*M_W +
CONTENT_SCORE*C_W +
HR_SCORE*HR_W +
STORAGE_SCORE*S_W +
DISTRIBUTOR_SCORE*D_W +
SUMMARY_SCORE*S2_W +
PLAN_SCORE*P_W +
LO_W*LEAD_OPPORTUNITIES_SCORE
STORAGE_DEPLOYMENT_SCORE*S_D_W +
CONTENT_DEPLOYMENT_SCORE*C_D_W +
DISTRIBUTOR_DEPLOYMENT_SCORE*D_D_W +
FORUM_DEPLOYMENT_SCORE*F_D_W +
]/((B_W + M_W + C_W + HR_W + S_W + D_W + SU_W + P_W + LO_W + S_D_W + C_D_W + D_D_W + F_D_W)*2^N)

```

### Catastrophic Errors

#### **No valid plan**

A valid council period plan was not submitted by 24 hours after the last election was completed, as specified above.

**NA** for the initial term

#### **No valid summary**

A valid council period summary was not submitted by 12 hours after the next election was completed, as specified above.

#### **Missed runtime upgrade**

A runtime upgrade was proposed by [#official-jsgenesis-membership](../../jsgenesis.md#official-jsgenesis-membership "mention"), but it was not approved.

#### **Upgrading non-Jsgenesis runtime**

A runtime upgrade, not proposed by [#official-jsgenesis-membership](../../jsgenesis.md#official-jsgenesis-membership "mention"), was approved.

#### **Total $tJOY exceeds tJOY\_BUDGET**

Total spending, as defined in [#total-usdtjoy-spending](./#total-usdtjoy-spending "mention"), exceeded `tJOY_BUDGET`

#### **Block time too low**

The average time between blocks was greater than `10s` for more than a 2 hour interval.

#### **Member faucet empty**

The membership faucet requires both that the Membership working group budget has sufficient tJOY to pay the `membershipPrice` and that the Lead has sufficient invitations. If at any point during the council term, the faucet capacity is less than 5 new members, that counts as effectively empty.

#### On chain Budget and Opening proposals without JOY equivalent

Any approved proposals that deals with a working group budget (denominated in `tJOY`), or the opening for a Lead role (reward denominated in `tJOY`), must also contain a reference to the `JOY` value. This is a key factor in increasing awareness of the value of incentives, and must be respected as such.

## FAQ

### How do I get on the council?

You have to win a seat as part of the [#elections](./#elections "mention"), and this requires persuading people to vote for you, in you yourself do not have sufficient $tJOY to back your own candidacy. However, Jsgenesis will be looking to help a few promising newcomers each council, as described in [#jsgenesis-endorsement](./#jsgenesis-endorsement "mention").
