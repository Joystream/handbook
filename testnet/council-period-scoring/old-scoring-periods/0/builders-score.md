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
BUILDER_SCORE = 0.1*GENERAL_WG_SCORE + 0.4*HOWTO_SCORE + 0.10*BOUNTY_SCORE + 0.35*ISSUES_SCORE + 0.05*WORK_LIST_SCORE
```

where

### `GENERAL_WG_SCORE`
Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`0%`**.


### `HOWTO_SCORE`
*Objective:* `Create various guides for users`

#### Instructions
In this [notion space](https://joystream.notion.site/Technical-Guides-aa4d5973d8de4db0b31a6f5fca31d8ae), write guides on:
- How to become a
  - validator
  - nominator
- How to install and use
  - `joystream-node`
  - `joystream-cli` (basic use, nothing that requires Worker/Lead privileges)
  - `query-node`

#### Scoring Calculations

```
  HOWTO_SCORE = 0.3*joystream-node_score + 0.15*validator_score + 0.05*nominator_score + 0.2*joystream-cli_score + 0.3*query-node_score
```


### `BOUNTY_SCORE`
*Objective:* `Create various guides for users`

#### Instructions
As part of the onboarding for new users specifically, but also for more "advanced" users in some cases, bounties will be created on-chain for them. Technical bounties will have someone from the Builder WG as the "oracle", set by the HR group when opening said Bounty.

Create a document outlining the Bounty workflow (with emphasis on the oracle side), and add it to the [notion space](https://joystream.notion.site/Builders-ffb1c9d1d1094fc4a6f04eb47677673d).
- Use the staging network for testing, with [pioneer](https://pioneer-2.vercel.app/#/settings?network-config=https://18.207.235.254.nip.io/network/config.json)

#### Scoring Calculations

The `BOUNTY_SCORE` is set subjectively.

### `ISSUES_SCORE`
*Objective:* `Review Pioneer issues`

#### Instructions
Pioneer 2.0, and it's [github repo](https://github.com/Joystream/pioneer) has a lot of open issues. In the near future, the devs and product manager will go through each, and assign them a specific label (likely `community`), meaning the issue will be assigned to the Builders, or Bounties will be created for them.

More info [here](https://github.com/Joystream/joystream/issues/3473)

In the meantime, go through as many issues as possible (filtered by what you think are appropriate labels, based on the "more info" issue above, also - ignore issues assigned to `dmtrjsg`), and produce a spreadsheet/table in the [notion space](https://joystream.notion.site/Builders-ffb1c9d1d1094fc4a6f04eb47677673d) and comment:
- `if` the issue doesn't seem likely to be assigned as a Bounty or Builder task:
  - why (one-liner)
- `else if` the issue seems very easy, and no "joystream" context is needed (Bounty?)
  - why (one-liner)
  - assign a **rough** difficulty level and hour(s) needed
- `else` the issue seems like a good task for the Builders, eg. not that easy, and/or some "joystream" context needed:
  - why (one-liner)
  - assign a **rough** difficulty level and hour(s) needed

#### Scoring Calculations
Let:
- `issues_addressed` be the amount of issues added to the notion space, with comment
- `grading` be the subjective grading JSG assigns [0,1]

Then:
```
  ISSUES_SCORE = grading * (issues_addressed-50)/100
```

### `WORK_LIST_SCORE`
*Objective:* `Gather list of "wanted" work`

#### Instructions
Some members in the Builders group will have "pet projects" they want to work on. There are also a ton of useful tools the project as a whole, and especially other WGs need to do their job.

Compile a list of these, and set a rough estimate of hours needed for each.

#### Scoring Calculations

The `WORK_LIST_SCORE` is set subjectively.
