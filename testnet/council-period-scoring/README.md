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

_Valid through council scoring period number 10, for the council elected at block `#950,400.`_

| Name                      | Value                           |
| ------------------------- | ------------------------------- |
| `JOY_BUDGET`              | USD 150,000 (0.25%)             |
| `REFERRER_JOY`            | USD 3,000 (0.005%)              |
| `REFERREE_JOY`            | USD 3,000 (0.005%)              |
| `tJOY_BUDGET`             | 100,000,000                     |
| `USD_SUBSIDY`             | USD 2,400 `*`                   |
| `JOY_VERIFICATION_CAP`    | USD 5,000 (0.00833%)            |
| `JOY_INDUCTION_THRESHOLD` | USD 15,000 (0.025%)             |
| `COUNCIL_tJOY_REWARD`     | 4,032,000 (20,160,000 in total) |

\`\*\` includes $100 subsidy for SPs, and $150 subsidy for distributors This means that JSG will mint $250 worth of tJOY and distribute across the workers, but these tJOY will not earn the recipients JOY.

_The Parameters for each new scoring period should be made available the following Monday 2000 CET, along with the updated metrics._

Until published, the council should assume they will stay the same until the update is made.

## Summary Report and Plan Deadlines

For the system to work well, there is a need for a feedback-loop, between

* the councils [#council-period-summary](./#council-period-summary "mention") and the working groups [#working-group-summary](general-working-group-score.md#working-group-summary "mention") are important for Jsgenesis in order to;
* publish [#council-period-parameters](./#council-period-parameters "mention") (for the next scoring period), which are needed for;
* the new councils [#council-period-plan](./#council-period-plan "mention") and working groups [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"). ****&#x20;

For this to be the case, strict deadlines are required. Based on feedback, we are going to make some changes in order to allow for information transfer from working groups to the council, and for the latter to review and request changes.&#x20;

Suppose Council `n` is elected at block B\_n\_el.

[#working-group-summary](./#working-group-summary "mention")&#x20;

Deadline: `B_n_el+10800 (`election + 18h) for scoring period `n-1`



[#council-period-summary](./#council-period-summary "mention")

Deadline: `B_n_el+14400 (`election + 24h) for scoring period `n-1`



**Working Group Reports**

Deadline: `B_n_el+14400 (`election + 24h) for scoring period `n-1`



**Initial Grading Results Published**

Target Deadline: `B_n_el+23400`(election+39h) for scoring period `n-1`

A post made in the `#council` room on discord will be made to notify the "old" Council of this.



[#council-period-parameters](./#council-period-parameters "mention")

Target Deadline: `B_n_el+28800`  (election+48h) for scoring period `n-1`



****[#council-period-plan](./#council-period-plan "mention")****

Deadline: `B_n_el+36000 (`election + 60h) for scoring period `n`

``

[#working-group-period-plan](./#working-group-period-plan "mention")****

Deadline: `B_n_el+43200 (`election + 72h) for scoring period `n`

### Deadline Notes

* This means the council can not "formally" approve a final version of their own, nor the working groups summaries through a proposal, as there will be a "new" Council by the time it's completed. Instead, the "old" Council will be allowed to make corrections, by simply having one of the "old" Council members posting a new version of the report as a reply to the one made by the Lead, within the Council Period Summary Deadline (meaning an extra 6 hours).
* For 6h after the **Initial Grading Results** are published, complaints may be issued. For any complaint to be considered, it must come from the "old" Council or the Lead of the Working Group in question, with specific errors or corrections, backed by numbers, facts or links.
* Once the new **Council Period Parameters** are out, Jsgenesis will create a signal proposal with:
  * A summary of which paramters was changed and why
  * A summary of changes to made to the scoring metrics
* For every 6h the **Initial Grading Results** are delayed, the plans may be submitted 6h later with no negative impact on the scoring.

##

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
* Any $tJOY approved for bounty work (as defined in the [human-resources-score.md](human-resources-score.md "mention")).

Note that the although the `$tJOY_BUDGET`, may be confused with the concept of on chain Council and \[Working Group] Budgets, these are not equivalent. Whereas the tJOY\_BUDGET above includes the spending on validators and nominators, the council do not in fact control this. The same can be said for the bounties referred to above, although they have some influence and recourse here.

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

## Working Group Summary

### Motivation

1. Allow Jsgenesis to update the [#council-period-parameters](../testnet-rewards.md#council-period-parameters "mention") and [#network-performance-score](./#network-performance-score "mention") metrics for the next period based on up to date and accurate information.
2. Allow the possible next council and working group lead to have good information about the most urgent matters and status of the group.
3. Provide some group-specific data, to ease the grading process.

### Scope

All working group summaries have the same "core" scope

* Accounting of how much was spent on what.
* Actual hires made.
* Actual slashes imposed.
* Actual firings done.
* Changes made to the corresponding notion board.
* A summary on how well the working group served it's intended purpose.
* Recommendations for what should be focused on in next council period in order to make group more effective.
* Suggested changes to the purpose or practices built in to this working group, other working groups, the council or Jsgenesis' role, in order to increase overall effectiveness of the group or the project.

### Submission

For each working group, a plan must be submitted with the following specifics:

* written as a markdown document in English
* using a template, so that each report is structured and formatted uniformly
* posted to the forum under category `Governance > Working Groups Plans and Summaries`  in a thread titled:  `[Working Group Name] Summary: [Council Period ID]` where `[Working Group Name]`is the name of the working group

In order for the Council to review and approve any summary, we have to either:

1. Accept that the latest datapoints can not be part of the scoring
2. Allow the council or leads to update the final numbers after the council can no longer approve a plan or summary.

As the numbers are such a key component, we are going with alternative 2. However, this means the Council need another way of approving them.

If there is a need to link to extra information, statistics, etc. these should be in the working groups own notion board, but the general report itself **must** be posted on the forum.

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

## Working Group Period Plan

#### Motivation

Give Jsgenesis and the council visibility into the priorities of the group, and also serve as a canonical document to focus everyone in the group around a clearly defined plan.

#### Scope

All working group period plans have the same scope:

* Current group composition.
* Plan for hirings (emphasizing newcomers).
* Planned firings.
* Onboarding plans for newcomers.
* Ranked list of suggestions for problems groups should attempt to tackle, and how, with corresponding budgeting, marketing or other resources needed from council or Jsgenesis.

**Note:** The plan for hiring and firings don't have to be specific members/workers, just the number of.

#### Submission

For each working group, a plan must be submitted with the following specifics:

* written as a markdown document in English
* using a template, so that each report is structured and formatted uniformly
* posted to the forum under category `Governance > Working Groups Plans and Summaries` in a thread titled: `[Working Group Name] Plan: [Council Period ID]` where `[Working Group Name]`is the name of the working group
* include a link to a signal proposal, where the Council explicitly approves the plan
  * a single proposal can approve all/multiple plans

Links to external resources, such as notion boards, can only include extra information, statistics, and the likes, not the core scope.

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

<table><thead><tr><th>Weight</th><th data-type="number">Value</th></tr></thead><tbody><tr><td><code>B_W</code></td><td>8</td></tr><tr><td><code>C_W</code></td><td>5</td></tr><tr><td><code>D_W</code></td><td>6</td></tr><tr><td><code>F_W</code></td><td>1</td></tr><tr><td><code>HR_W</code></td><td>8</td></tr><tr><td><code>M_W</code></td><td>2</td></tr><tr><td><code>S_W</code></td><td>6</td></tr><tr><td><code>SUM_W</code></td><td>2</td></tr><tr><td><code>P_W</code></td><td>2</td></tr><tr><td><code>CM_W</code></td><td>2</td></tr><tr><td><code>LO_W</code></td><td>2</td></tr></tbody></table>

Jsgenesis reserves the right to add 1 point to the `M_W` assuming a scope is agreed.

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
