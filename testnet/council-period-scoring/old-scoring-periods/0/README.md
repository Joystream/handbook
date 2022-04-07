---
Scoring Period 0 Summary
---

# 📏 Council Period 0 Scoring

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
All metrics and results for previous scoring rounds can be found [here](/testnet/council-period-scoring/old-scoring-periods/scoring-period-0).

## Dashboard

Here is a live [dashboard](http://joystream.org) which holds key information from the current council period.

For the first Council:
- `tJOY_BUDGET`: 48,000,000
-  `JOY_BUDGET`: 0.06%

(Both numbers revised upwards, with the addition of a `MARTETING_SCORE` & `GENERAL_WG_SCORE` )


## Knowledge Bases <a href="#group-knowledge-base" id="group-knowledge-base"></a>

The council and each working group must maintain its own Notion board where a body of knowledge related to the operations of the group are maintained. This base will be owned by Jsgenesis, while on testnet, and the current lead of each working group and all council members will be given write access to maintain it. The integrity of the boards is the responsibility of each person granted access, and sharing of credentials is not allowed. If this constraint causes problems in efficiently maintaining the boards, contact Jsgenesis.

## Council Knowledge Base

{% embed url="https://joystream.notion.site/Council-809dd7bcf6744844ba0dcccf98670dcc" %}
Council Knowledge Base
{% endembed %}

## Total $tJOY Spending

The total $tJOY spending over a given council period is something Jsgenesis attempts to directly constrain through its policy parameter `tJOY_BUDGET` , and it the sum of the following non-overlapping categories of flows during the blocks of a council period

* Any increase in $tJOY that any validator can cashout, but currently has not.
* Any $tJOY that has actually been cashed out by validators.
* Any $tJOY actually cashed out by any council member, lead or worker, so not counting missed payments.
* Any $tJOY for spending proposals, except spending to finance on-demand bounties approval by [#human-resources](../../system/working-groups/#human-resources "mention") .
* Any $tJOY approved for bounty work.

**Note:** The last two will be updated once the bounty module is included in Pioneer.

**Question:** how easy is it for the council to actually (a) constrain and (b) monitor these flows for a given council period? At least before Pioneer 2 financial section.

## Council Period Summary

### Motivation

* Allow Jsgenesis to update the [#council-period-parameters](../testnet-rewards.md#council-period-parameters "mention") and [#network-performance-score](./#network-performance-score "mention") metrics for the next period based on up to date and accurate information.
* Allow the possible next council to have good information about the most urgent matters and status of the network.

### Scope

* Accounting of how much was spent on what.
* Actual hirings done.
* Actual firings done.
* Spending proposals passed.
* Changes made to the corresponding [Broken link](broken-reference "mention") .
* A summary on how well the network as a whole performed, and what problems occurred.
* Recommendations for what should be focused on in next council period in order to make the network more effective.

### Submission

The report itself must be written as a markdown document in English, in the forum category `Testnet>Council>Summaries` , as a thread which has the title which includes the council period ID. The council must pass a text proposal (add link when proposal list is in) which references the report on the forum.

## Council Period Plan

### Motivation

Give Jsgenesis visibility into the priorities of the council, and also serve as a canonical document to focus everyone in the council around a clearly defined plan.

### Scope

* Prioritization to each working group about what they should focus on solving.
* How total $tJOY budget will be allocated across groups and council.

### Submission

The plan itself must be written as a markdown document in English, in the forum category `Testnet>Council>Plans` , as a thread which has the title which includes the council period ID. The council must pass a text proposal (add link when proposal list is in) which references the plan on the forum.

## Lead Opportunities

There must be made space for people to try to participate as leads for working group, even to the extent that other more experienced - but proficient leads, have to pause their participation. It is up to the council to determine the cheapest way to accommodate newcomers without undermining the operations of the working group. Not only must the space be allocated and reserved for newcomers, but there must be effective collaboration with the [human-resources.md](../../system/human-resources.md "mention") working group to actually identify potential applicants and encourage them to apply to these opportunities.

## Score

### Overview
**Note:**
See [Deployment Score](#deployment-score) for how the deployment incentives plays in this first term.


At the beginning of each council  [#jsgenesis](../../glossary.md#jsgenesis "mention") staff will state a set of explicit metrics that will apply to the upcoming council period. At the end of each council period,  [#jsgenesis](../../glossary.md#jsgenesis "mention") staff will determine a final _network performance score_ for the council which will be in the range \[0,1]. This score is used to determine the [usdtjoy.md](../usdtjoy.md "mention") reward and [#founding-member-points](../founding-member-program.md#founding-member-points "mention") for the council members, as described above.

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
````

where

* `BUILDER_SCORE` (`B_W`): computed with metric defined in [builders-score.md](builders-score.md "mention").
* `MARKETER_SCORE` (`M_W`): computed with metric defined in [marketers-score.md](marketers-score.md "mention").
* `CONTENT_SCORE`(`C_W`): computed with metric defined in [content-directory-score.md](content-directory-score.md "mention").
* `HR_SCORE` (`HR_W`): computed with metric defined in [human-resources-score.md](human-resources-score.md "mention").
* `STORAGE_SCORE` (`S_W`): computed with metric defined in [storage-providers-score.md](storage-providers-score.md "mention").&#x20;
* `DISTRIBUTOR_SCORE` (`D_W`): computed with metric defined in [distributors-score.md](distributors-score.md "mention").&#x20;
* `SUMMARY_SCORE` (`SU_W`):  is a score computed for the quality of the council summary, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
  * Quality of changes to the knowledge base.
* `PLAN_SCORE` (`P_W`): is a score computed by Jsgenesis staff for the quality of the council plan, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
* `LEAD_OPPORTUNITIES_SCORE` (`LO_W`) is `1/min(x_1,..., x_k)` , which will be in the range \[0, 1], where `x_i` is the total number of council period in which the `i`th lead has worked in this group.&#x20;
* `B_W,M_W,C_W,HR_W,SP_W,D_W,SU_W,P_W,LO_W` : are the weights from the table below.
* `N` : The number of catastrophic error instances which occurred, as defined below.



### Weights

The current weights are:

<table><thead><tr><th>Weight</th><th data-type="number">Value</th></tr></thead><tbody><tr><td><code>B_W</code></td><td>3</td></tr><tr><td><code>M_W</code></td><td>1</td></tr><tr><td><code>C_W</code></td><td>2</td></tr><tr><td><code>HR_W</code></td><td>3</td></tr><tr><td><code>S_W</code></td><td>5</td></tr><tr><td><code>D_W</code></td><td>6</td></tr><tr><td><code>SU_W</code></td><td>1</td></tr><tr><td><code>P_W</code></td><td>0</td></tr><tr><td><code>LO_W</code></td><td>0</td></tr></tbody></table>

### Deployment Score
For this first council term, the rewards from the initial set of [incentives](https://gist.github.com/bwhm/0df4242854c41a77a397b0e52e2f8a3b), focused on deploying the network, must also be included:

 * `STORAGE_DEPLOYMENT_SCORE` (`S_D_W`): 9
 * `CONTENT_DEPLOYMENT_SCORE` (`C_D_W`): 3
 * `DISTRIBUTOR_DEPLOYMENT_SCORE` (`D_D_W`): 3
 * `FORUM_DEPLOYMENT_SCORE` (`F_D_W`): 2

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
Which means:
```
TOTAL_COUNCIL_tJOY_REWARD = 0.4 * (tJOY_BUDGET + UNSPENT_tJOY_BUDGET) * NETWORK_PERFORMANCE_SCORE^2
```

### Catastrophic Errors&#x20;

#### **No valid plan**

A valid council period plan was not submitted by 24 hours after the last election was completed, as specified above.&#x20;

**NA** for the initial term

#### **No valid summary**

A valid council period summary was not submitted by 12 hours after the next election was completed, as specified above.

#### **Missed runtime upgrade**

A runtime upgrade was proposed by [#official-jsgenesis-membership](../../jsgenesis.md#official-jsgenesis-membership "mention"), but it was not approved.

#### **Upgrading non-Jsgenesis runtime**

A runtime upgrade, not proposed by [#official-jsgenesis-membership](../../jsgenesis.md#official-jsgenesis-membership "mention"), was approved.

#### **Total $tJOY exceeds tJOY\_BUDGET**

Total spending, as defined in [#total-usdtjoy-spending](./#total-usdtjoy-spending "mention"), exceeded `tJOY_BUDGET`&#x20;

#### **Block time too low**

The average time between blocks was greater than `10s` for more than a 2 hour interval.


## Results
general-working-group-score.md

### Content

```
CONTENT_SCORE = 0.1*GENERAL_WG_SCORE +0.25*POLICY_SCORE + 0.35*WORKFLOW_SCORE + 0.3*GUIDE_SCORE

CONTENT_SCORE = 0.1*1 + 0.25*0 + 0.35*0 + 0.3*0 = 0.1
```

### HR
```
HR_SCORE = 0.1*GENERAL_WG_SCORE + 0.2*PROTOCOL_SCORE + 0.25*CRM_SCORE + 0.2*TIMELINESS_SCORE + 0.25*WELCOMING_SCORE


HR_SCORE = 0.1*1 + 0.2*1 + 0.25*1 + 0.2*1 + 0.25*1 = 1
```

### Marketers
```
MARKETING_SCORE = 0.1*GENERAL_WG_SCORE + 0.40*ISSUES_SCORE + 0.35*GITBOOK_SCORE + 0.15*GLOSSARY_SCORE

MARKETING_SCORE = 0.1
```



### Storage
```
STORAGE_SCORE = 0.1*GENERAL_WG_SCORE + 0.25*REPLICATION_SCORE + 0.3*MAINTENANCE_SCORE + 0.20*UPLOAD_SCORE + 0.15*GUIDE_SCORE


REPLICATION_SCORE = 0.5*[max(min_replication_rate-2,1)+max(avg_replication_rate-2.5,1)] + max(min_replication_rate-3,1)
= 0.5*[(2-2 + 2.02-2.5) + (4.991736838-3)] = 0.5*(0+1)
REPLICATION_SCORE = 0.25

MAINTENANCE_SCORE = 0.25*(dynamic_configuration_score + existing_bag_configuration_score + excess_capacity_objects_score + excess_capacity_size_score)
= 0.25*(0 + 0 + 1 + 1)
MAINTENANCE_SCORE = 0.5

UPLOAD_SCORE = (successful_uploads/total_uploads - 0.96)/0.04
= (109/(109+9) - 0.96)/0.04 + (133/(133+17) - 0.96)/0.04
UPLOAD_SCORE = 0

STORAGE_SCORE = 0.1*1 + 0.25*0.25 + 0.3*0.5 + 0.20*0 + 0.15*0 = 0.3125
```

### Distributors
```
DISTRIBUTOR_SCORE = 0.1*1 + 0.35*THUMBNAIL_SCORE + 0.1*PLAYABLITIY_SCORE + 0.3*SERVICE_SCORE + 0.15*GUIDE_SCORE

THUMBNAIL_SCORE = 0.6*avg_rendering + 0.4*max_rendering_score
THUMBNAIL_SCORE = 0.6*(1500-1647) + 0.4*(2500-2590) = 0

SERVICE_SCORE = 0.25*(1 + 0.32 + 0.26 + 0.24)
SERVICE_SCORE = 0.455

DISTRIBUTOR_SCORE = 0.1*1 + 0.35*0 + 0.1*1 + 0.3*0.455 + 0.15*1 = 0.4865
```

### Builders
```
BUILDER_SCORE = 0.1*1 + 0.4*HOWTO_SCORE + 0.10*BOUNTY_SCORE + 0.35*ISSUES_SCORE + 0.05*WORK_LIST_SCORE

BUILDER_SCORE = 0.1*1 + 0.4*0 + 0.10*0 + 0.35*0 + 0.05*0 = 0.1
```


## Initial
### Storage Providers
```
# 1
create_opening_score = (44000 - opening_approved_block)/1000 + 0.2*quality_of_opening
= (44000 - 43404 )/1000 + 0.2*0.1 = 0.616

# 2
hire_lead_score = (45000 - lead_hired_block)/3600 + 0.5*preparation_score
= (45000 - 43465)/3600 + 0.5*0.1 = 0.476

# 3
migration_readiness_score = 0.5*(lead_readiness_block - lead_hired_block)/600 + 0.5*preparation_score + 0.5*approved_lead_transactions/required_lead_transactions
= 0

# 4
lead_availability_score = 1

STORAGE_DEPLOYMENT_SCORE = 0.616*0.2 + 0.476*0.3 + 0*0.3 + 1*0.2 = 0.466
```
### Content
```
create_opening_score = (45000 - 44498)/1800 = 0.279

CONTENT_DEPLOYMENT_SCORE = 0.279
```

### Distributor
```
# 1
create_opening_score = (44000 - opening_approved_block)/1000 + 0.2*quality_of_opening
= (44000 - 43455)/1000 + 0.2*1 = 0.745

# 2
fill_opening_score = (45000 - lead_hired_block)/3600 + 0.5*preparation_score
= (45000 - 44885)/3600 + 0.5*0.3 = 0.182

# 3
deployment_score = 0.3*bag_coverage_score + 0.3*asset_coverage_score + 0.4*bag_duplication/2
= 0.3*1 + 0.3*1 + 0.4*1 = 1

DISTRIBUTOR_DEPLOYMENT_SCORE = 0.745*0.3 + 0.182*0.3 + 1*0.4 = 0.6781
```

### Forum
```
# 1
fill_opening_score` = (44000 - lead_hired_block)/800
= (44000 - 43710)/800 = 0.3625

# 2
deploy_categories_score = 0.5*(44400 - bounty_category_block)/1200 + 0.5*(45000 - initial_categories)/1800
= deploy_categories_score = 0.5*(44400 - 44850)/1200 + 0.5*(45000 - 45421)/1800 = 0

FORUM_DEPLOYMENT_SCORE = 0.3625*0.2 + 0*0.8 = 0.0725
```

### Membership
```
create_opening_score = (45000 - lead_hired_block)/1800
= (45000 - 43483)/1800 = 0.843
```

### Final
```
NETWORK_PERFORMANCE_SCORE =
[0.1*3 + 0.1*1 + 0.1*2 + 1.0*3 + 0.3125*5 + 0.3125*6 + 0.8*1 + 0.466*9 + 0.279*3 + 0.6781*3 + 0.0725*2] 3+1+2+3+5+6+1+0+9+3+3+2 = 15.0478 / 38 = 0.396
```

## Earnings
Due to poor information, and possibly errors finding the rewards, the Council "underspent" significantly during this cycle. Following the formulaes for rewards, that strictly speaking, would mean the JOY budget wouldn't be distributed in full. We are making an exception this once.

The overall, and individual rewards can be found using the dashboards [here]()
