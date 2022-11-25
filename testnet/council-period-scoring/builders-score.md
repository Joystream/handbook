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
BUILDER_SCORE = [STAGING_NETWORK_SCORE + TESTING_SCORE + PIONEER_DEVELOPMENT_SCORE + GENERAL_DEVELOPMENT_SCORE]/4
```

where

```
STAGING_NETWORK_SCORE
```

#### Instructions

Create one or more staging networks with the values requsted, for the Storage and Distribution groups.

### `TESTING_SCORE`

_Objective:_ `Test pioneer bugfixes`

#### Instructions

A github [project](https://github.com/orgs/Joystream/projects/55) has been created for the Builder group.

#### Scoring Calculations

Let:

* `ISSUES_TESTED` be the number of issues tested, regardless of the outcome of the test
* If the feedback provided is lacking, or the workflow is not adhered to, the issue will not count.

```
TESTING_SCORE:
  If ISSUES_TESTED >= 15:     1
  If 5 < ISSUES_TESTED < 15:  ISSUES_TESTED/15
  If ISSUES_TESTED =< 5:      0
```

### `PIONEER_DEVELOPMENT_SCORE`

#### Instructions

Two github projects has been created for the Builder group, this metric applies to the pioneer project found [here](https://github.com/orgs/Joystream/projects/55).

How well the story points translates into score is not fully calibrated, and may be revised after the period is over. If so, it will only be upward. Not that only when a PR is _approved_ by Jsgenesis, will story points translate into points.

#### Rules

The workflow cards that was added by jsgenesis must be added back to the board.

#### Scoring Calculations

For each issue that gets merged during a scoring period, the amount of story points are summed up, and added below.

```
DEVELOPMENT_SCORE:
  If STORY_POINTS >= 12:  1
  If STORY_POINTS < 12:   STORY_POINTS/12
```

If the score surpasses 12 `STORY_POINTS` the points can be transferred over to the `TESTING_SCORE` or the `GENERAL_DEVELOPMENT_SCORE` this term.

### `GENERAL_DEVELOPMENT_SCORE`

#### Instructions

Two github projects has been created for the Builder group, this metric applies to the general builders project found [here](https://github.com/orgs/Joystream/projects/56).

How well the story points translates into score is not fully calibrated, and may be revised after the period is over. If so, it will only be upward. Not that only when a PR is _approved_ by Jsgenesis, will story points translate into points.

#### Rules

Only Jsgenesis may add tasks to this board, but the Council may ask Jsgenesis to add tasks in the Builders working group plan.&#x20;

#### Scoring Calculations

For each issue that gets merged during a scoring period, the amount of story points are summed up, and added below.

```
GENERAL_DEVELOPMENT_SCORE:
  If 0 < STORY_POINTS < 15:  STORY_POINTS/15
  If STORY_POINTS >= 15:     1
```

If the score surpasses 15 `STORY_POINTS` the points can be transferred over to the `TESTING_SCORE` or the `PIONEER_DEVELOPMENT_SCORE` this term.

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
