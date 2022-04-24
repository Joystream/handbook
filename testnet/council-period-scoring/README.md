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

_Valid through council scoring period number 4, for the council elected at block `#345,600.`_

| Name                  | Value                           |
| --------------------- | ------------------------------- |
| `JOY_BUDGET`          | 2,000,000 (0.2% \~USD 120,000)  |
| `REFERRER_JOY`        | 1000 (\~USD 60)                 |
| `REFERREE_JOY`        | 1000 (\~USD 60)                 |
| `tJOY_BUDGET`         | 90,000,000                      |
| `USD_SUBSIDY`         | USD 2000                        |
| `CAP`                 | JOY 15,000 (\~USD 9,000)        |
| `COUNCIL_tJOY_REWARD` | 2,016,000 (10,080,000 in total) |

_The Parameters for scoring period 5 will be made available on Monday 1800 CET, along with the updated metrics._&#x20;

Although changes must be expected, the council should assume they will stay the same until the update is made.

One change that can be accounted for already, is the fact that the Storage Providers and Distributors will receive an extra $tJOY subsidy, that will NOT count towards their $JOY earnings. This is done to account for the fact that workers (not Leads) in these roles have real operational costs, but their role doesn't require much time. The subsidy will be distributed at the time of grading, and will be shared equally across each worker in each group, adjusted by the number of blocks they were part of the group.

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
4.  No later than 24 hours after a new council is set:

    * the council delivers the council period plan
    * all working groups delivers working group period plan



For council period **Council Scoring Round 5 (#**446,400-#547,200) the following deadlines will apply

| Deliverable                                                                               | Responsible          | Deadline                             | Notes                            |
| ----------------------------------------------------------------------------------------- | -------------------- | ------------------------------------ | -------------------------------- |
| [#working-group-summary](general-working-group-score.md#working-group-summary "mention")  | Working Group Leads  | <p>#453,600<br>(24.04 ~1130 CET)</p> | Following the "old" ruleset      |
| [#council-period-summary](./#council-period-summary "mention")                            | Council #4           | <p>#453,600<br>(24.04 ~1130 CET)</p> | Following the "old" ruleset      |
| [#council-period-parameters](./#council-period-parameters "mention")                      | Jsgenesis            | <p>#471,600<br>(25.04 ~1800 CET)</p> | For Scoring Period #5            |
| Council Period Scoring Results                                                            | Jsgenesis            | <p>#472,800<br>(25.04 ~2000 CET)</p> | For Scoring Period #4            |
| [#council-period-plan](./#council-period-plan "mention")                                  | Council #5           | <p>#480,000<br>(26.04 ~0800 CET)</p> | Needs the two deliverables above |
| [#working-group-summary](general-working-group-score.md#working-group-summary "mention")  | Working Group Leads  | <p>#554,400<br>(01.05 ~0900 CET)</p> |                                  |
| [#council-period-summary](./#council-period-summary "mention")                            | Council #5           | <p>#558,000<br>(01.05 ~1200 CET)</p> |                                  |
| Council Period Scoring Results                                                            | Jsgenesis            | <p>#572,400<br>(02.05 ~1700 CET)</p> | For Scoring Period #5            |
| [#council-period-parameters](./#council-period-parameters "mention")                      | Jsgenesis            | <p>#572,400<br>(02.05 ~1700 CET)</p> | For Scoring Period #6            |



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

## Council Handover Meeting

Around the time a council election is over, a meeting between the council members that just finished their term, the newly elected council and Jsgenesis. Until further notice, the meeting will be closed off to only these participants, and mandatory in the sense that turnout impacts the score.

### Motivation

A handover meeting allows the new council to prepare for their [#council-period-plan](./#council-period-plan "mention") with assistance from both the previous council and Jsgenesis. The previous council will get immidiate feedback on their [#council-period-summary](./#council-period-summary "mention") and Jsgenesis will learn what the current pressure points are.

### Agenda

* Review the temporary summary, presented by the previous council, for the benefit of all parties, with an emphasis on lessons learned.
* A look at the next [#council-period-parameters](./#council-period-parameters "mention"), and the impacts that may have.
* A Q\&A session.
* A quick run through of how the scoring works.

A member of the new council takes notes, and quickly prepares a brief minutes of meeting to post on the forum or discord for feedback by the others. To avoid conflict and reduce the barrier to speak, the minutes must obey the "[Chatham House Rules](https://en.wikipedia.org/wiki/Chatham\_House\_Rule)".

### Submission

Once approved (informally, eg. no comments in discord unaddressed), the minutes are submitted in the forum category `Testnet>Council>Minutes`, as a thread which has the title which includes the two council period IDs.

## Council Daily Sync

As for any organization, internal communication is key for performance. Every day between the handovers, the Council shall have a daily sync call, held in public on Discord. They are free to coordinate internally when these are held, with the exception of the first one that must be held after Jsgenesis publishes the new [#council-period-parameters](./#council-period-parameters "mention") and the scoring metrics for the period, and well before the deadline to release the [#council-period-plan](./#council-period-plan "mention"). See [#summary-report-and-plan-deadlines](./#summary-report-and-plan-deadlines "mention") for more information.

During the [#council-handover-meeting](./#council-handover-meeting "mention") the Council shall agree on a specific times for these meetings. The minutes are submitted in the forum category `Testnet>Council>Minutes`, in a thread titled Council period ID.

## Lead Opportunities

There must be made space for people to try to participate as leads for working group, even to the extent that other more experienced - but proficient leads, have to pause their participation. It is up to the council to determine the cheapest way to accommodate newcomers without undermining the operations of the working group. Not only must the space be allocated and reserved for newcomers, but there must be effective collaboration with the [human-resources.md](../../system/human-resources.md "mention") working group to actually identify potential applicants and encourage them to apply to these opportunities.

## Score

### Overview

At the beginning of each council [#jsgenesis](../../glossary.md#jsgenesis "mention") staff will state a set of explicit metrics that will apply to the upcoming council period. At the end of each council period, [#jsgenesis](../../glossary.md#jsgenesis "mention") staff will determine a final _network performance score_ for the council which will be in the range \[0,1]. This score is used to determine the [usdtjoy.md](../usdtjoy.md "mention") reward and [#founding-member-points](../founding-member-program.md#founding-member-points "mention") for the council members, as described above.

Specifically, the score is a weighted linear combination of scores _working group scores_, which themselves are in the range \[0,1], which is normalized by the weights, and lastly discounted by exponentially by the number of _catastrophic errors_ detected, that is

```
NETWORK_PERFORMANCE_SCORE = [
BUILDER_SCORE*B_W +
CONTENT_SCORE*C_W +
DISTRIBUTOR_SCORE*D_W +
FORUM_SCORE*F_W +
HR_SCORE*HR_W +
MARKETER_SCORE*M_W +
STORAGE_SCORE*S_W +
SUMMARY_SCORE*SU_W +
PLAN_SCORE*P_W +
LO_W*LEAD_OPPORTUNITIES_SCORE
]/((B_W + C_W + D_W + F_W + HR_W + S_W + M_W + SU_W + P_W + LO_W)*2^N)
```

where

* `BUILDER_SCORE` (`B_W`): computed with metrics defined in [builders-score.md](builders-score.md "mention").
* `CONTENT_SCORE`(`C_W`): computed with metrics defined in [content-directory-score.md](content-directory-score.md "mention").
* `DISTRIBUTOR_SCORE` (`D_W`): computed with metrics defined in [forum-score.md](forum-score.md "mention") .
* `FORUM_SCORE` (`F_W`): computed with metrics defined in [distributors-score.md](distributors-score.md "mention").
* `HR_SCORE` (`HR_W`): computed with metrics defined in [human-resources-score.md](human-resources-score.md "mention").
* `MARKETER_SCORE` (`M_W`): computed with metrics defined in [marketers-score.md](marketers-score.md "mention").
* `STORAGE_SCORE` (`S_W`): computed with metrics defined in [storage-providers-score.md](storage-providers-score.md "mention").
* `SUMMARY_SCORE` (`SU_W`): is a score computed for the quality of the council summary, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
  * Quality of changes to the knowledge base.
* `PLAN_SCORE` (`P_W`): is a score computed by Jsgenesis staff for the quality of the council plan, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
* `HANDOVER_SCORE` (`P_W`): is a score in the range \[0, 1], computed based on three factors:
  * Turnout of council members (n/m), for both meetings a single council should participate on
  * The minutes of meeting, to be published for discussion within 30min of each call, and formalized within 2 days.
* `LEAD_OPPORTUNITIES_SCORE` (`LO_W`) is `1`
* `/min(x_1,..., x_k)` , which will be in the range \[0, 1], where `x_i` is the total number of council period in which the `i`th lead has worked in this group.
* `*_W` : are the weights from the table below.
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Weights

The current weights are:

<table><thead><tr><th>Weight</th><th data-type="number">Value</th></tr></thead><tbody><tr><td><code>B_W</code></td><td>4</td></tr><tr><td><code>C_W</code></td><td>2</td></tr><tr><td><code>D_W</code></td><td>5</td></tr><tr><td><code>F_W</code></td><td>1</td></tr><tr><td><code>HR_W</code></td><td>4</td></tr><tr><td><code>M_W</code></td><td>null</td></tr><tr><td><code>S_W</code></td><td>5</td></tr><tr><td><code>SUM_W</code></td><td>1</td></tr><tr><td><code>P_W</code></td><td>1</td></tr><tr><td><code>H_W</code></td><td>1</td></tr><tr><td><code>LO_W</code></td><td>1</td></tr></tbody></table>

Jsgenesis reserves the right to add 1 point to the `M_W` assuming a scope is agreed.

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
HANDOVER_SCORE*H_W +
LEAD_OPPORTUNITIES_SCORE*LO_W
]/((B_W + M_W + C_W + HR_W + S_W + D_W + SUM_W + P_W + LO_W)*2^N)

```

### Catastrophic Errors

#### **No valid plan**

A valid council period plan was not submitted by 24 hours after the last election was completed, as specified above.

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
