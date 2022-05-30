---
description: Metrics used to compute score for all working groups
---

# General Working Group Score

Introduction

The _general working group score_ is a type of score, computed in the same way, for all working groups. This general score is incorporated into a final specific score of each working group, which is what is directly used in the final network score, as described in [#network-performance-score](./#network-performance-score "mention")

To find the final scores for each group, consult the corresponding sub-article:

{% content-ref url="builders-score.md" %}
[builders-score.md](builders-score.md)
{% endcontent-ref %}

{% content-ref url="content-directory-score.md" %}
[content-directory-score.md](content-directory-score.md)
{% endcontent-ref %}

{% content-ref url="distributors-score.md" %}
[distributors-score.md](distributors-score.md)
{% endcontent-ref %}

{% content-ref url="human-resources-score.md" %}
[human-resources-score.md](human-resources-score.md)
{% endcontent-ref %}

{% content-ref url="forum-score.md" %}
[forum-score.md](forum-score.md)
{% endcontent-ref %}

{% content-ref url="marketers-score.md" %}
[marketers-score.md](marketers-score.md)
{% endcontent-ref %}

{% content-ref url="storage-providers-score.md" %}
[storage-providers-score.md](storage-providers-score.md)
{% endcontent-ref %}

## Worker Opportunities

There must be made space for newcomers to try to participate in the working group, even to the extent that other more experienced - but proficient participants, have to pause their participation in a given role to accommodate newcomers. It is up to the relevant authority, be it the working group lead or the council, in the case of hiring leads, to determine the cheapest way to accommodate newcomers without undermining the operations of the working group. Not only must the space be allocated and reserved for newcomers, but there must be effective collaboration with the [human-resources.md](../../system/human-resources.md "mention") working group to actually identify potential applicants and encourage them to apply to these opportunities.

## Bounty Score

The HR group is responsible for onboarding new people, by providing them a bounty or two where they can show what they can do to contribute. Assuming they are capable, it is important that they are given a chance to proceed further, and get a role where they belong.&#x20;

However, the Leads shouldn't have to hire anyone unless there is a reason they are qualified, meaning the HR group needs to be able to test them somehow.

For each new term, the group must present at least one bounty that a newcomer can address in order to prove themselves for the group in question.

### Scope

* Title
* High level summary and purpose
* Time estimate to complete, assuming some relevant skills, but little to no experience with Joystream or the working group
* Detailed scope of work, relevant for either a specific part of the working group score, or more general
  * if specific, this implies the group is looking for a worker in this sub-section
* Discord handle and `memberId` of a worker (or the Lead) WG to act as the oracle for the bounty

## Opening Score

In addition to actually be given opportunities when applying , there needs to be a way for them to have an opening to submit their application. Although the Lead may not be of the opinion they _need_ someone at any given moment, there should always be a space to apply to a well written and informative opening.

### Scope

* Maintain at least one opening for a role in the group at any point during a council period
* The opening must be relevant, created in the current or last council period, and
  * be well written and outlining any requirements, conditions, nice to haves, that is needed to get the job
  * include a set of question that allows the applicant to distinguish themselves
  * include a link to a forum thread, where any interested parties or applicants can ask questions, and the discord handle of the Lead
  * include the latest bounty created by the group, to act as a skill test
* Anyone applies or asks questions in the forum must be followed up within 48h

## Score

The general working groups score for a given group is computed as follows:

`GENERAL_SCORE = [SUMMARY_SCORE + PLAN_SCORE + WORKER_OPPORTUNITIES_SCORE + OPENING_SCORE + BOUNTY_SCORE]/(5*2^{N+M})`

where

* `SUMMARY_SCORE` is a score computed for the quality of the working group summary, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
  * Quality of changes to the knowledge base.
  * Quality and quantity of new bounties.
* `PLAN_SCORE` is a score computed by Jsgenesis staff for the quality of the working group plan, which will be in the range \[0, 1], and will emphasize things like
  * Clarity of communication and organization.
  * Appropriate scope.
  * Accuracy of facts and information.
  * Quality of recommendations
* `WORKER_OPPORTUNITIES_SCORE` is `1/percentile(X, [x_1, ..., x_n])` , which will be in the range \[0, 1], where
  * `X` is a group-specific percentage, called the _opportunity target_, and `percentile(X,S)` returns the `X`th percentile in non-empty sequence of observations _S._ Consult the scoring rules for each group to find values of `X`.
  * `x_i` is the total number of council period in which the `i`th worker in the group has worked in this group.
  * Consult the scoring rules for each group to find values of `X`.
* `OPENING_SCORE` is a score computed by Jsgenesis staff based on the quality (and existance) of the groups openings, which will be in the range \[0, 1], and will emphasize things like
  * No "downtime" without any openings, even just after filling or closing the old one
  * Quality of opening, in terms of information, requests and questions
  * Inquires and applications dealt with in a reasonable time and manner
* `BOUNTY_SCORE` is a score computed by Jsgenesis staff based on the quality of the groups openings, which will be in the range \[0, 1], and will emphasize things like
  * Appropriate and well defined scope, meaning it's related either to a general part of the working group, or specific task associated with a specific opening.
  * A time estimate for completion, which is between 30 minutes and 3 hours.
  * Proposes either the Lead, or another trusted worker in the group, as the oracle for the bounty.
* `N` : The number of catastrophic errors, as listed below.

### Catastrophic Errors

#### Late summary

The summary is late by >6 hours or more.

#### Late plan

The plan is late by >6 hours or more.

#### No openings

No openings existed during the term

#### HR sourced candidate not hired

Each scoring period, the HR group is allowed to force the group to hire a member that has gone through the onboarding, given that:

1. The member completed a Bounty made by the group and was awarded a winner.
   * If the group has not made any bounties for this purpose, or a member of the group was the Oracle, but didn't submit judgement in time, it counts as true
2. The member applied with more than two days (28,800 blocks) left of the term.
3. The group has not already hired someone recommended by the HR group said term.
