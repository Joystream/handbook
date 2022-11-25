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

_Valid for council scoring period number 31, for the first council elected on Carthage (at block `#216,000.`)_ _The term will last from `#216,000` to `#288,000` -> `72,000` blocks -> 5 days_

| Name                  | Value               |
| --------------------- | ------------------- |
| `JOY_BUDGET`          | USD 150,000 (0.25%) |
| `REFERRER_JOY`        | USD 3,000 (0.005%)  |
| `REFERREE_JOY`        | USD 3,000 (0.005%)  |
| `tJOY_BUDGET`         | 300,000             |
| `COUNCIL_tJOY_REWARD` | 83,333              |

Notes:

* `tJOY_BUDGET` Does NOT include validator rewards, as the Council can not influence in time for the network.
* `COUNCIL_tJOY_REWARD` is the total reward for the CMs earned over the duration of the Scoring Period

##

## Reporting

#### Daily Status Update

For Carthage, the Council is expected to publish daily reports on the Forum, and link to it on Discord. The report should cover:

* Working Group status, meaning for each group:
  * The composition (and changes) of Workers and Leads
  * Any changes in openings
  * Budgets and spending
  * What the group is working on, with emphasis on Scoring Metrics
  * Communication between the Council and the Group
* Council Status, meaning:
  * Overall budget and spending
  * What they have been doing
  * Which meetings have taken place, with links to MoM if applicable
  * Announce planned meetings
* Proposal status changes

The document should be concise but complete and preferably published at roughly the same time each day.

#### Scoring Period Summary

Unless a Scoring Period ends on a new election, the documents should be posted within a window of 12 hours before the period ends, and a day after. The summary should cover:

* Working Group status, meaning for each group over the period:
  * The composition (and changes) of Workers and Leads
  * Any changes in openings
  * Budgets and spending
  * What the group worked on and achieved
  * Communication between the Council and the Group
* Council Status, meaning:
  * Overall budget and spending
  * What they have been doing
  * Which meetings have taken place, with links to MoM if applicable
  * Announce planned meetings
* Proposal summary
* Lessons learned

More or a less a summary of the status updates, but with some extra context.

#### Scoring Period Plan

Unless a Scoring Period ends on a new election, the documents should be posted within a window of 12 hours before the period ends, and a day after. The plan should cover:

* Working Group plans, meaning for each group over the period:
  * What they expect to work on and achieve
  * Budgets for the Group
  * Planned communication with the Group
  * Changes planned from the previous Scoring Period
* Council plans, meaning activities outside of the Working Groups:
  * Other spending plans
  * Workflow plans
  * Changes planned from the previous Scoring Period

## Knowledge Bases <a href="#group-knowledge-base" id="group-knowledge-base"></a>

The council and each working group must maintain its own Notion board where a body of knowledge related to the operations of the group are maintained. This base will be owned by Jsgenesis, while on testnet, and the current lead of each working group and all council members will be given write access to maintain it. The integrity of the boards is the responsibility of each person granted access, and sharing of credentials is not allowed. If this constraint causes problems in efficiently maintaining the boards, contact Jsgenesis.

## Council Knowledge Base

{% embed url="https://joystream.notion.site/Council-809dd7bcf6744844ba0dcccf98670dcc" %}
Council Knowledge Base
{% endembed %}

### Total tJOY Spending

The total tJOY spending over a given council period is something Jsgenesis attempts to directly constrain through its policy parameter `tJOY_BUDGET` , and it the sum of the following non-overlapping categories of flows during the blocks of a council period

* Any tJOY actually awarded to any council member, lead or worker.
* Any tJOY paid through a Funding Request.

Note that the although the `$tJOY_BUDGET`, may be confused with the concept of on chain Council and \[Working Group] Budgets, these are not equivalent.

### Opportunities Score

At the end of the Period, the amount of Workers and Leads OR their rewards, whatever is worst (excluding Council Members) will be added up between members that have reached the FM threshold or not.

Starting at 1, for each percentage point over 40% that is held by members over the threshold, the score will decrease by by 0.025.

### Score

#### Overview

At the beginning of each council #jsgenesis staff will state a set of explicit metrics that will apply to the upcoming council period. At the end of each council period, #jsgenesis staff will determine a final _network performance score_ for the council which will be in the range \[0,1]. This score is used to determine the usdtjoy.md reward and #founding-member-points for the council members, as described above.

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

* `BUILDER_SCORE` (`B_W`): computed with metrics defined in builders-score.md.
* `CONTENT_SCORE`(`C_W`): computed with metrics defined in content-directory-score.md.
* `DISTRIBUTOR_SCORE` (`D_W`): computed with metrics defined in forum-score.md .
* `FORUM_SCORE` (`F_W`): computed with metrics defined in distributors-score.md.
* `HR_SCORE` (`HR_W`): computed with metrics defined in human-resources-score.md.
* `MARKETER_SCORE` (`M_W`): computed with metrics defined in marketers-score.md.
* `STORAGE_SCORE` (`S_W`): computed with metrics defined in storage-providers-score.md.
* `SUMMARY_SCORE` (`SU_W`): is a score computed for the quality of the council summary, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
  * Quality of changes to the knowledge base.
* `PLAN_SCORE` (`P_W`): is a score computed by Jsgenesis staff for the quality of the council plan, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
* `DAILY_STATUS_SCORE` (`CM_W`): is a score in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
* `OPPORTUNITIES_SCORE` is `1/min(x_1,..., x_k)` , which will be in the range \[0, 1] as defined above
* `*_W` : are the weights from the table below.
* `N` : The number of catastrophic error instances which occurred, as defined below.

#### Weights

The current weights are:

| Weight | Value |
| ------ | ----- |
| B\_W   | 3     |
| C\_W   | 1     |
| D\_W   | 5     |
| F\_W   | 1     |
| HR\_W  | 3     |
| M\_W   | 1     |
| S\_W   | 5     |
| SUM\_W | 2     |
| P\_W   | 2     |
| CM\_W  | 2     |
| LO\_W  | 2     |

Which Means:

```
NETWORK_PERFORMANCE_SCORE = [
BUILDER_SCORE*B_W +
CONTENT_SCORE*C_W +
DISTRIBUTOR_SCORE*D_W +
FORUM_SCORE*D_W +
HR_SCORE*HR_W +
MARKETER_SCORE*M_W +
STORAGE_SCORE*S_W +
SUMMARY_SCORE*SUM_W +
PLAN_SCORE*P_W +
DAILY_STATUS_SCORE*CM_W +
OPPORTUNITIES_SCORE*LO_W
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
