---
description: Metrics used to compute score for content directory working group.
---

# Content Directory Score

## Overview

The Content Directory working group activities relevant to scoring can be understood exclusively in terms of the following three categories:

* **Moderation:** Ensuring that the content available through the platform's public applications is legal, properly licensed and appropriate for the testnet environment and its participants.
* **Featuring:** Ensuring that the most impressive content available on the platform is promoted to the maximum extent possible given the tools available, and as regularly as is feasible considering the volume of new high-quality content coming in. This must be done in a manner which is clean and in accordance with the design and branding of our consumption application, Atlas.
* **Metadata Integrity:** On the testnet environment, partially as a training exercise which will develop participants familiarity with the structure of the content directory, there will be a focus on maintaining a "clean" directory of content, with effective titles, descriptions, thumbnails and other metadata, as well as correct license information and the deployment of attribution best practices, and also the avoidance of spam.

## Moderation

Perhaps the most important element of the content curator role is helping to tackle the tiny minority of participants who are intent on using the platform in an unproductive or negative manner.

The content curators are responsible for building on the basic moderation principles established by Jsgenesis and developed by the Council. Based on these principles, they have the power to hide videos, unlist them, or remove them from the content directory entirely. The chain gives curators similar privileges to manage entire channels where problems may have arisen.

While we are an open source platform with a philosophical opposition to censorship, it is important that the testnet platform is accessible to as many people as possible. As a result, content curators should be proactive in monitoring the content directory for potential violations of the established content guidelines.

## Featuring

While removing damaging content is important, showing off the best content that Joystream has to offer is also very important for the platform's long-term growth.

This is possible through a variety of different featuring capabilities already built into Atlas and the runtime. For example, curators are currently able to set featured videos for categories, and for the main landing page.

There should be an emphasis on choosing recent, high-quality videos with broad appeal when selecting featured videos, as these provide new participants with an important initial impression of the current state of the platform.

## Metadata Integrity

Joystream represents a library of content, and as is the case in any library, it's important that the articles within it are properly organised and looked after.

Videos in the wrong category, tagged in the wrong language, having empty titles or with blurry or misleading thumbnails lead to bad experiences for users, so instances of these sorts of errors should be tackled efficiently and in accordance with some established policy.

It's particularly important that the main "surfaces" for content consumers, such as the landing page, are free of spam, in order to provide the best possible experience for those exploring the platform.

Curators, who should be very familiar with content licensing and attribution rules, also have some responsibility for training content uploaders in the appropriate ways of handling this.

## Knowledge Base

{% embed url="https://joystream.notion.site/Content-Directory-6e4b6d211b174526889464d263475cab" %}
Content Directory Working Group Knowledge Base
{% endembed %}

## Score

The Content Directory working group score is computed as follows

```
CONTENT_SCORE = 0.1*GENERAL_WG_SCORE +0.25*POLICY_SCORE + 0.35*WORKFLOW_SCORE + 0.3*GUIDE_SCORE
```

where

### `GENERAL_WG_SCORE`
Is computed with metricS defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`0%`**.


### `POLICY_SCORE`
*Objective:* `Create a curation policy`

#### Instructions
Jsgenesis has published a new (limited) [curation policy](/system/content-directory/content-policy.md) to use as the base, but that only covers the bare minimum.
The Council and/or Content group should create two documents:
1. one that targets users, so that a channel owner can know what to expect, how to rectify the situation, etc.
2. one that targets curators, so that they know what to do in case `x` happens
- create a flow chart diagram that displays the above visually
Propose a moderation policy, if approved by the Council, add a (sticky) Forum thread about it, and add it to the [notion space](https://joystream.notion.site/Content-Directory-6e4b6d211b174526889464d263475cab).

#### Scoring Calculations
The `POLICY_SCORE` is graded subjectively.


### `WORKFLOW_SCORE`
*Objective:* `Create a Content Curation workflow`

#### Instructions
Closely related to the above, but not exactly the same. Curators can't just randomly look at videos popping up on the [player](play.joystream.org), and watch/review them independently of each other. Propose a workflow, if approved by the Council, add it to the [notion space](https://www.notion.so/joystream/Content-Directory-6e4b6d211b174526889464d263475cab).
A good workflow could be built around a spreadsheet, or db, that keeps track of all channels, videos and dataObjects in the directory, and:
- when they were last updated
- who reviewed "it", and when (in case of new updates)
- any remarks
- any actions made
- etc.
Part of this should address who reviews what and how?

#### Scoring Calculations
The `WORKFLOW_SCORE` is graded subjectively.

### `GUIDE_SCORE`
*Objective:* `Create a howto guide for Content Workers`

#### Instructions
Until now, the Joystream "howto" guides in general, and Curators are no exception, has been available in the helpdesk. We are moving away from this, and want them to hosted in the groups [notion space](https://joystream.notion.site/Content-Directory-6e4b6d211b174526889464d263475cab).

In order to test how curation works, use staging network, with:
- [pioneer](https://pioneer-2.vercel.app/#/settings?network-config=https://18.207.235.254.nip.io/network/config.json)
- [atlas](https://atlas-olympia-staging.vercel.app/)
DM Martin on discord for the Lead key, as testing of access is likely needed.

Create new guides for doing all the actions required by the Curators (and the Lead). This includes (at least):
- How to use the [query-node playground](query.joystream.org)
  - To find new or updated channels/videos
- How to use the cli
  - What you can do (as a `Curator`) in the cli
  - What are groups, and how do they work
- How to delete assets, if the owner refuses (this requires checking other modules!)

#### Scoring Calculations
The `GUIDE_SCORE` is graded subjectively.
