---
description: Metrics used to compute score for all working groups
---

# General Working Group Score

## Introduction

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
* Propose set of bounties that newcomers can tackle.
* Changes made to the corresponding notion board.
* A summary on how well the working group served it's intended purpose.
* Recommendations for what should be focused on in next council period in order to make group more effective.
* Suggested changes to the purpose or practices built in to this working group, other working groups, the council or Jsgenesis' role, in order to increase overall effectiveness of the group or the project.

### Submission

The lead for each for a working group must submit the report, with the following specifics:

* written as a markdown document in English
* in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the title which includes the council period ID.
* must use the template created by the council for the term, which should be posted on their notion boards

If there is a need to link to extra information, statistics, etc. these should be in the working groups own notion board, but the general report itself **must** be posted on the forum.

## Working Group Period Plan

### Motivation

Give Jsgenesis and the council visibility into the priorities of the group, and also serve as a canonical document to focus everyone in the group around a clearly defined plan.

### Scope

All working group period plans have the same scope:

* Current group composition.
* Plan for hirings (emphasizing newcomers).
* Planned firings.
* Onboarding plans for newcomers.
* Ranked list of suggestions for problems groups should attempt to tackle, and how, with corresponding budgeting, marketing or other resources needed from council or Jsgenesis.

**Note:** The plan for hiring and firings don't have to be specific members/workers, just the number of.

### Submission

The lead for each for a working group must submit the report, with the following specifics:

* written as a markdown document in English
* in the forum category `Working Groups >[Working Group Name]>Plans` where `[Working Group Name]` is the name of the working group, as a thread which has the title which includes the council period ID
* must use the template created by the council for the term, which should be posted on their notion boards

If there is a need to link to extra information, statistics, etc. these should be in the working groups own notion board, but the general report itself **must** be posted on the forum.

## Worker Opportunities

There must be made space for newcomers to try to participate in the working group, even to the extent that other more experienced - but proficient participants, have to pause their participation in a given role to accommodate newcomers. It is up to the relevant authority, be it the working group lead or the council, in the case of hiring leads, to determine the cheapest way to accommodate newcomers without undermining the operations of the working group. Not only must the space be allocated and reserved for newcomers, but there must be effective collaboration with the [human-resources.md](../../system/human-resources.md "mention") working group to actually identify potential applicants and encourage them to apply to these opportunities.

## Score

The general working groups score for a given group is computed as follows:

`GENERAL_SCORE = [SUMMARY_SCORE + PLAN_SCORE + WORKER_OPPORTUNITIES_SCORE]/(3*2^{N+M})`

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
* `N` : The number of full 6 hour increments that elapse from the [deadline](./#summary-report-and-plan-deadlines) until a summary report is submitted as described.&#x20;
* `M` : The number of full 12 hour increments that elapse from  [deadline](./#summary-report-and-plan-deadlines) until the summary a period plan is submitted as described.
