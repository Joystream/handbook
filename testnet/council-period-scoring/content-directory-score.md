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
CONTENT_SCORE = [MODERATION_SCORE + DOCUMENTATION_SCORE]/(2*2^{N})
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

``

### `MODERATION_SCORE`

Content moderation is applied swiftly and appropriately in accordance with the [Content Policy](../content-policy.md).

#### Scoring Calculations

Let:

* `response_time_i` be the time (in hours) from a video `i` is published until an action has been taken.
* `justification_j` be a score in the range \[0,1], set by Jsgenesis staff for a few selected actions, based on:
  * the justification provided for the action, such as pointing to the rule or guideline that is violated, proof related to license, etc.
  * the `rationale` included in the `content.updateVideoCensorshipStatus` extrinsic
  * further logging, such as the blockheight/event/[link to explorer](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.joystream.org%3A9944#/explorer) and who made the decision
  * whether or not the justification/`rationale` is true

Then:

```
response_time_score_i:
  response_time_i >= 4:          1
  response_time_i < 24:          0
  4 < response_time_i < 24:      -0.05*response_time_i + 1.2
  
MODERATION_SCORE = [ sum(response_time_score_i) / i + sum(justification_j) / j] / 2
```

### `DOCUMENTATION_SCORE`

Play around with the new system, and document how the content directory works. Emphasis on permissions for updating, changing and moderating, as a:

* Channel owner
* Collaberator
* Curator (not in a group)
* Curator (in a group)
* Lead

### Catastrophic Errors

#### Failure to apply moderation rules

Any item which violates the content guidelines is unmoderated more than 36 hours after being uploaded

**Video censored unjustly**

Any video that shouldn't have been censored, gets censored without being reverted by the end of the period. Same applies if a video is censored without justification in the report (from `REPORT_SCORE`).

**Logging does not occur**

No logs are kept.

#### Featured Content Unplayable

If the hero video, or the hero of any category, is not playable and is not dealt within within 1 hour after the change

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
