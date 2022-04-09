---
description: Metrics used to compute score for builders working group.
---

# Builders Score

## Overview

The operations working group is unlike other working groups, in that they are only really being measured based on the quality of their output, as judged by Jsgenesis.

The working group will generally focus on developing tools and enhancing existing applications (Pioneer, Atlas, CLI etc.) and the runtime which come together to make the Joystream platform as a whole. Once the network has stabilized, a specific label will be assigned to issues in the various repos under the Joystream organization, each of which will include points to serve as a way to assign weight to each issue. These points will then be used in terms of calculating the groups score.

Their contributions to these tools and the creation of new ones are represented as a development score, which attempts to measure the volume and quality of development based on the resources available to the working group.

It should be kept in mind that this development activity is not purely restricted to Jsgenesis tools and projects, but can also apply to community projects such as [JoystreamStats](https://joystreamstats.live).

## Knowledge Base

{% embed url="https://joystream.notion.site/Builders-ffb1c9d1d1094fc4a6f04eb47677673d" %}
Builders Notion knowledge base
{% endembed %}

## Score

The builders working group score is computed as follows

```
BUILDER_SCORE = [GENERAL_WG_SCORE + REPORT_SCORE + TESTING_SCORE + DEVELOPMENT_SCORE]/4
```

where

### `GENERAL_WG_SCORE`

Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must include a section covering

#### Dev builder issues

* How many dev issues, when and which (link) for each, in each project board was
  * Assigned to a worker (which)
  * Started by a worker
  * Sent for internal review (to whom)
  * Internal review approved
  * Sent to Jsgenesis review
    * what is the status/result of said review
  * What was the approximate hours spend per issue (work, review, addressing review feedback)
* What is the current status on all issues started, but not completed

#### Testing builder issues

* How many testing issues, when and which (link) for each, in each project board was
  * Tested and approved
  * Tested, but issues were found

#### Bounty issues

* How many bounty issues, when and which (link) for each, in each project board was
  * A builder was assigned as oracle (which)
  * What is the current status of the bounty

#### Other

* How well is the Joystream stack covered by the current group
* How well are the current dev issues suitable to the current group, meaning
  * Are there any "kinds" of issues the group wants more of, relative to the their stack
  * Are there any "kinds" of issues the group wants fewer of, relative to the their stack
* What part of the workflow is unclear, or could be improved (how, why)

Whereas the same deadline as general report applies, there is no requirement to submit a temporary report for this.

### `TESTING_SCORE`

_Objective:_ `Test pioneer bugfixes`

#### Instructions

A github [project](https://github.com/orgs/Joystream/projects/55) has been created for the Builder group.

#### Scoring Calculations

Let:

* `ISSUES_TESTED_SCORE_i` be an issue that was tested, moved to one of the two "done" in the github project, and commented on in line with the workflow.
* `GRADING_i` be the grading of each of the issues, based on whether the information provided was sufficient or not (binary)
* `WORKFLOW_SCORE` be the overall grading of the workflow, representing whether or not it was followed

```
  TESTING_SCORE = PIONEER_TEST_SCORE*WORKFLOW_SCORE = [(15 - ISSUES_TESTED_SCORE_i*GRADING_i)/15]*WORKFLOW_SCORE
```

### `DEVELOPMENT_SCORE`

_Objective:_ `Help building the platform`

#### Instructions

Two github projects has been created for the Builder group:

1. [https://github.com/orgs/Joystream/projects/55](https://github.com/orgs/Joystream/projects/55)
2. [https://github.com/orgs/Joystream/projects/56](https://github.com/orgs/Joystream/projects/56)

Whereas the first one is well populated, and with a fully fleshed out workflow, the latter is not.

How well the story points translates into score is not fully calibrated, and may be revised after the period is over. If so, it will only be upward. Not that only when a PR is _approved_ by Jsgenesis, will story points translate into points.

#### Scoring Calculations

```
  ISSUE_POINTS = Sigma(STORY_POINTS_i)
  DEVELOPMENT_SCORE = (10-ISSUE_POINTS)/5
```
