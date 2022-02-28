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

{% embed url="https://grizzled-corleggy-af8.notion.site/Content-Directory-35573c46f5b54d899fa2069621a6f1e4" %}
Content Directory Working Group Knowledge Base
{% endembed %}

## Score

The Content Directory working group score is computed as follows

`[GENERAL_WG_SCORE + MODERATION_SCORE + FEATURING_SCORE + METADATA_SCORE]/(4*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `MODERATION_SCORE`:  is a score computed by Jsgenesis staff for the quality and speed of the moderation activity, which will be in the range \[0, 1], and will emphasize
  * Speed of response to any content which violates our guidelines
  * Appropriate level of sanction applied for infractions
* `FEATURING_SCORE`: is a score computed by Jsgenesis staff for the quality of featuring activity, which will be in the range \[0, 1], and will emphasize&#x20;
  * Frequency of updating featured content
  * Quality of content featured given the content available and quality of text, thumbnails etc. and other assets used in promoting content
* `METADATA_SCORE`: is a score computed by Jsgenesis staff for the quality of metadata monitoring activity, which will be in the range \[0, 1], and will emphasize&#x20;
  * The proportion of Jsgenesis test videos uploaded correctly screened
  * Instances where other video metadata errors have been ignored (apart from Jsgenesis spotchecks)
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors&#x20;

#### Failure to apply moderation rules

Any item which violates the content guidelines is unmoderated more than 24 hours after being uploaded
