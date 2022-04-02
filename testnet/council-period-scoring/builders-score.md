---
description: Metrics used to compute score for builders working group.
---

# Builders Score

## Overview

The operations working group is unlike other working groups, in that they are only really being measured based on the quality of their output, as judged by Jsgenesis.

The working group will generally focus on developing tools and enhancing existing applications (Pioneer, Atlas, CLI etc.) and the runtime which come together to make the Joystream platform as a whole.  Once the network has stabilized, a specific label will be assigned to issues in the various repos under the Joystream organization, each of which will include points to serve as a way to assign weight to each issue. These points will then be used in terms of calculating the groups score.

Their contributions to these tools and the creation of new ones are represented as a development score, which attempts to measure the volume and quality of development based on the resources available to the working group.

It should be kept in mind that this development activity is not purely restricted to Jsgenesis tools and projects, but can also apply to community projects such as [JoystreamStats](https://joystreamstats.live).

## Knowledge Base

{% embed url="https://joystream.notion.site/Builders-ffb1c9d1d1094fc4a6f04eb47677673d" %}
Builders Notion knowledge base
{% endembed %}

## Score
The builders working group score is computed as follows

```
BUILDER_SCORE = 0.1*GENERAL_WG_SCORE + 0.15*WG_WORKFLOW_SCORE + 0.4*TESTING_SCORE + 0.35*ISSUES_SCORE
```

where

### `GENERAL_WG_SCORE`
Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`20%`**.


### `WG_WORKFLOW_SCORE`
*Objective:* `Test pioneer bugfixes`

#### Instructions
A github [project](https://github.com/orgs/Joystream/projects/55) has been created for the Builder group. At the time of writing, the workflow it's not fully finalized, it only contains issues from the [pioneer](https://github.com/Joystream/pioneer/), and it only contains testing issues. By Tuesday, some development issues will be added as well.

A critical part of the Builders WG is to maintain a good workflow. We will hold the Builders to a different (and higher) standard than we would for "other" community members or just your random contributor. This is both because we are preparing the community for the future, but also because we want you to be an asset for us. If Jsgenesis continuously needs to spend more time reviewing/triaging/assisting the Builders than we would just fixing the issue, that wouldn't be true.

#### Scoring Calculations
Unlike other Builder scores, the metrics below are graded subjectively.
Let:
`ACCESS_RIGHTS`:
- The Lead will research what (organizational) permissions are needed to:
  - assign, and be assigned, issues
  - move issues around in the project kanban boards
- The Lead decides on a subset of Workers that will be given these privileges, based on:
  - trust and experience
  - organizational skills (rather than dev/testing skills)
  - github familiarity
- The Lead pings Jsgenesis every time a change in the permissions are required, including the Lead themselves.
`WORKFLOW_FEEDBACK`
- Review the workflow in the Project, and provide feedback to JSG regarding:
  - clarity
  - viability
  - reasonability
`ENVIRONMENT_SCORE`
- Devs need a good environment to test in, whether it's their own work or not. We have a staging network deployed for which the Builders can be given access. Ask Jsgenesis for access, and review further needs.
- Create a guide for in the groups notion board, for how to set up their own testing environment, whether it be:
  - Pioneer only, where they connect to a specific chain and query-node, whether it's the staging network, "Olympia" proper, or a dev-chain
  - A complete dev-chain, with local instances of the joystream-node query-node, Pioneer, atlas, orion, argus and colossus.

Then:
```
WG_WORKFLOW_SCORE = (ACCESS_RIGHTS + WORKFLOW_FEEDBACK + ENVIRONMENT_SCORE)/3
```

### `TESTING_SCORE`
*Objective:* `Test pioneer bugfixes`

#### Instructions
A github [project](https://github.com/orgs/Joystream/projects/55) has been created for the Builder group.

There are two "todo" columns in the project. One of them is "To Test on Staging", that contains issues that should have been fixed by the corresponding PR linked to in the issue itself. The workflow is defined at the top of the column.

See [`WG_WORKFLOW_SCORE`](#wg_workflow_score) for more information.

#### Scoring Calculations
Let:
  - `ISSUES_TESTED_SCORE_i` be an issue that was tested, moved to one of the two "done" in the github project, and commented on in line with the workflow.
  - `GRADING_i` be the grading of each of the issues, based on whether the information provided was sufficient or not (binary)
  - `WORKFLOW_SCORE` be the overall grading of the workflow, representing whether or not it was followed
```
  TESTING_SCORE = PIONEER_TEST_SCORE*WORKFLOW_SCORE = [(13 - ISSUES_TESTED_SCORE_i*GRADING_i)/13]*WORKFLOW_SCORE
```

### `DEVELOPMENT_SCORE`
*Objective:* `Help building the platform`

#### Instructions
A github [project](https://github.com/orgs/Joystream/projects/55) has been created for the Builder group.

There are two "todo" columns in the project. One of them is "Community Backlog", and will be populated with issues by Tuesday. The workflow (will be updated) is defined at the top of the column.

See [`WG_WORKFLOW_SCORE`](#wg_workflow_score) for more information.

These will be assigned an `ISSUE_VALUE`, represented by a number, meant to roughly equate to 1h of work for (and by) an experienced developer. Whenever a PR, made by someone in the Builders WG, is merged, points are earned for that scoring period.

The relationship between the `ISSUE_VALUE` and `ISSUE_POINTS` will be added.

#### Scoring Calculations
```
  ISSUE_POINTS = Sigma(ISSUE_POINTS_i)
  DEVELOPMENT_SCORE = (X-ISSUE_POINTS)/Y
```
