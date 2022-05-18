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

_Valid through council scoring period number 8, for the council elected at block `#748,800.`_

Note: Increased by 5% to account for Forum weighting and score.

| Name                  | Value                           |
| --------------------- | ------------------------------- |
| `JOY_BUDGET`          | 2,500,000 (0.25% \~USD 150,000) |
| `REFERRER_JOY`        | 1000 (\~USD 60)                 |
| `REFERREE_JOY`        | 1000 (\~USD 60)                 |
| `tJOY_BUDGET`         | 100,000,000                     |
| `USD_SUBSIDY`         | USD 2400 `*`                    |
| `CAP`                 | JOY 15,000 (\~USD 9,000)        |
| `COUNCIL_tJOY_REWARD` | 3,024,000 (15,120,000 in total) |

\`\*\` includes $100 subsidy for SPs, and $150 subsidy for distributors This means that JSG will mint $250 worth of tJOY and distribute across the workers, but these tJOY will not earn the recipients JOY.

_The Parameters for each new scoring period should be made available the following Monday 1800 CET, along with the updated metrics._

Until published, the council should assume they will stay the same until the update is made.

One change that can be accounted for already, is the fact that the Storage Providers and Distributors will receive an extra $tJOY subsidy, that will NOT count towards their $JOY earnings. This is done to account for the fact that workers (not Leads) in these roles have real operational costs, but their role doesn't require much time. The subsidy will be distributed at the time of grading, and will be shared equally across each worker in each group, adjusted by the number of blocks they were part of the group.

## Summary Report and Plan Deadlines

For the system to work well, there is a need for a feedback-loop, between

* the councils [#council-period-summary](./#council-period-summary "mention") and the working groups [#working-group-summary](general-working-group-score.md#working-group-summary "mention") are important for Jsgenesis to;
* publish [#council-period-parameters](./#council-period-parameters "mention") (for the next term/scoring period), which are needed for;
* the new councils [#council-period-plan](./#council-period-plan "mention") and working groups [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"). ****&#x20;

For this to be the case, strict deadlines are required.&#x20;

The following deadlines will apply for a **Council Scoring Round**`n` with definitions below.

| Deliverable                                                                                                | Responsible | Deadline                                                 |
| ---------------------------------------------------------------------------------------------------------- | ----------- | -------------------------------------------------------- |
| Note: Council `n` elected                                                                                  | NA          | NA (`B_ce)`                                              |
| [#working-group-summary](general-working-group-score.md#working-group-summary "mention") (for `n-1`)       | WG Leads    | <p>Max(<code>B_ce+3600</code>,<br><code>N_cs</code>)</p> |
| [#council-period-summary](./#council-period-summary "mention") (for `n-1`)                                 | Council     | <p>Max(<code>B_ce+3600</code>,<br><code>N_cs</code>)</p> |
| Period Scoring Results (for `n-1`)                                                                         | Jsgenesis   | <p>Min[<code>B_ce+21600</code>,</p><p>09.05-1400CET]</p> |
| [#council-period-parameters](./#council-period-parameters "mention") and Metrics  (for `n`)                | Jsgenesis   | <p>Min[<code>B_ce+24000</code>,</p><p>09.05-1800CET]</p> |
| [#council-period-plan](./#council-period-plan "mention") (for `n`)                                         | Council     | <p>Max[<code>B_ce+24000</code>,<br>PPM+3000]</p>         |
| [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention") (for `n`) | WG Leads    | <p>Max[<code>B_ce+24000</code>,<br>PPM+3000]</p>         |

* `B_cs` means the block height the council term started (`B_cs+600`thus means 600 blocks later)
* `N_cs` means the first time the clock strikes noon CET after the council term started
* `B_ce` means the block height the council term ended
* `N_ce` means the first time the clock strikes noon CET after the council term ended
* `PPM` means when the new council period parameters and metrics are posted.

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
* Any tJOY paid through a Funding Request.
* Any $tJOY approved for bounty work.

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

The report itself must be written as a markdown document in English, in the forum category `Governance>Council Reports`, as a thread which has the title which includes the council period ID. The council must pass a text proposal (add link when proposal list is in) which references the report on the forum.

If there is a need to link to extra information, statistics, etc. these should be in the notion board.

## Council Period Plan

### Motivation

Give Jsgenesis visibility into the priorities of the council, and also serve as a canonical document to focus everyone in the council around a clearly defined plan.

### Scope

* Prioritization to each working group about what they should focus on solving.
* How total $tJOY budget will be allocated across groups and council.
* Set the schedule for all the [#council-meetings](./#council-meetings "mention") until the council period is over.
* List all known tasks to be assigned to individual council members, and add them to the council period task tracker on the Notion board.
* The council are further _encouraged_ to include specific workflows for items such as:
  * How to follow up each working group, and by whom
  * How budgets are managed, and by whom
  * Who is responsible for taking and publishing minutes
  * etc.

### Submission

The plan itself must be written as a markdown document in English, in the forum category `Governance>Council Reports`, as a thread which has the title which includes the council period ID. The council must pass a text proposal (add link when proposal list is in) which references the plan on the forum.

If there is a need to link to extra information, statistics, etc. these should be in the notion board.

## Council Meetings

As a minimum, all council members are expected to be available for

* two handover calls, after getting elected and after their term has ended
  * organized and always attended by Jsgenesis
* daily standups for coordinating between them
  * organized by the council themselves

### Motivation

#### Handover

A handover meeting allows the new council to prepare for their [#council-period-plan](./#council-period-plan "mention") with assistance from both the previous council and Jsgenesis. The previous council will get immidiate feedback on their [#council-period-summary](./#council-period-summary "mention") and Jsgenesis will learn what the current pressure points are.

#### **Daily Standup**

As for any organization, internal communication is key for performance. Every day between the handovers, the Council shall have a daily sync call, held in public on Discord. The scheduling will be set in the [#council-period-plan](./#council-period-plan "mention"), where the inaugural shall be **after** Jsgenesis publishes the new [#council-period-parameters](./#council-period-parameters "mention") and the scoring metrics for the period, but **before** the deadline to release the [#council-period-plan](./#council-period-plan "mention").&#x20;

See [#summary-report-and-plan-deadlines](./#summary-report-and-plan-deadlines "mention") for more information.

### Scope

#### Handover

* Discuss the performance of the previous council
* Review the temporary summary, presented by the previous council, for the benefit of all parties, with an emphasis on lessons learned
* Questions and comments

A member of the new council takes notes, and quickly prepares a brief minutes of meeting to post on the forum or discord for feedback by the others. To avoid conflict and reduce the barrier to speak, the minutes must obey the "[Chatham House Rules](https://en.wikipedia.org/wiki/Chatham\_House\_Rule)".

#### **Daily Standup**

* Follow up the tasks in the councils own task tracker

### Submission

#### Handover

Once approved (informally, eg. no comments in discord unaddressed), the minutes are submitted in the forum category `Governance>Council Reports` as a thread which has the title which includes the two council period IDs.

#### **Daily Standup**

Minutes are added to the `Governance>Council Reports` in a thread that contains all standups for the week.

## Council Daily Sync



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
MEETING_SCORE*ME_W +
LEAD_OPPORTUNITIES_SCORE + LO_W
]/((B_W + C_W + D_W + F_W + HR_W + S_W + M_W + SU_W + ME_W + P_W + LO_W)*2^N)
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
* `MEETING_SCORE` (`ME_W`): is a score in the range \[0, 1], computed based on two factors:
  * Turnout of council members (n/m), for all handover and standups, where 80% is required to achieve a full score
  * The quality and promptness of publishing the minutes of meeting, where the score falls linearly from 1 to 0 if minutes are published between 2 hour and 8 hours after the meeting started
* `LEAD_OPPORTUNITIES_SCORE` is `1/min(x_1,..., x_k)` , which will be in the range \[0, 1], where `x_i` is the total number of council period in which the `i`th lead has worked in this group.
* `*_W` : are the weights from the table below.
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Weights

The current weights are:

<table><thead><tr><th>Weight</th><th data-type="number">Value</th></tr></thead><tbody><tr><td><code>B_W</code></td><td>8</td></tr><tr><td><code>C_W</code></td><td>4</td></tr><tr><td><code>D_W</code></td><td>6</td></tr><tr><td><code>F_W</code></td><td>1</td></tr><tr><td><code>HR_W</code></td><td>8</td></tr><tr><td><code>M_W</code></td><td>null</td></tr><tr><td><code>S_W</code></td><td>6</td></tr><tr><td><code>SUM_W</code></td><td>2</td></tr><tr><td><code>P_W</code></td><td>2</td></tr><tr><td><code>CM_W</code></td><td>2</td></tr><tr><td><code>LO_W</code></td><td>2</td></tr></tbody></table>

Jsgenesis reserves the right to add 1 point to the `M_W` assuming a scope is agreed.

Which Means:

```
NETWORK_PERFORMANCE_SCORE = [
BUILDER_SCORE*B_W +
DISTRIBUTOR_SCORE*D_W +
CONTENT_SCORE*C_W +
HR_SCORE*HR_W +
MARKETER_SCORE*M_W +
STORAGE_SCORE*S_W +
SUMMARY_SCORE*SUM_W +
PLAN_SCORE*P_W +
COUNCIL_MEETING_SCORE*CM_W +
LEAD_OPPORTUNITIES_SCORE*LO_W
]/((B_W + C_W + D_W + HR_W + M_W + S_W + SUM_W + P_W + CM_W + LO_W)*2^N)
```

### General Working Group Grading Notes

For Jsgenesis to be able to complete the grading in "due time", all plans summaries needs to be

* easy to find (eg. in the applicable forum category)
* punctual
* formatted the same, easy to digest, way

To address this problem, the council will be tasked to create a template for the general working group summary and plan. Any report that is not made from this template, and posted on the forum in time, will score 0.



### Resources

It has become clear that some extra resources are needed for all parties to:

* See grading in flight
* Learn how Jsgenesis is grading each metric
* Further tips and ideas, not formally part of the overall scoring

{% embed url="https://www.notion.so/joystream/Tools-and-Resources-8969641b5b284d1c85c658106a79792d" %}
Tools and resources for grading
{% endembed %}

### Catastrophic Errors

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
