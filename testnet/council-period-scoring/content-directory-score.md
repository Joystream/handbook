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
CONTENT_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + FEATURING_SCORE + MODERATION_SCORE  + MIGRATION_SCORE]/(6)
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with metrics defined in [general-working-group-score.md](general-working-group-score.md "mention") where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must publish a separate report covering

**During the period**

* All channels and videos by `*Id` created. For each, include&#x20;
  * metadata, meaning (at least) `title`, `category`, `license`, `objectId`(s)
  * content directory status, meaning (at least) `isCensored`, `isPublic`, whether each object `isAccepted`
  * curator specific information, such as in which block it was created, the `createdAt` and `updatedAt`timestamps, for the purpose of being able to review a video that gets updated should be dealt with (eg. censored or no longer censored)
* All channels and videos by `*Id` updated. For each, include what the change was and when it was made.
* Channel or video categories created or deleted, when and why.
* All `NFT`s created, and their `Id`
* All `NFT`s sold, and the auction type and `Id`
* All moderation actions taken by the group, for which channels/video and why. This must include&#x20;
  * `*Id`
  * action taken
  * &#x20;justification (longer and "off-chain" - see `MODERATION_SCORE`)&#x20;
  * `rationale` (if applicable)
  * block height/event/[link to explorer](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.joystream.org%3A9944#/explorer) if a transaction was made
  * the `curatorId` which made the transaction
* All requests made to storage working group lead, related to moderation.
* All changes made to the featured content, with precise logs (see `FEATURING_SCORE`)

**For the content directory as a whole**

* Total amount of videos
* Total amount of channels
* Total amount of `NFT`s
* Amount of videos hidden and censored.

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `FEATURING_SCORE`

_Objective:_ `The "Featured Content" must be changed frequently to keep fresh`

### Notes

`FEATURING_SCORE` is a score computed by Jsgenesis staff for the quality of featuring activity, which will be in the range \[0, 1], and will emphasize;

* Frequency of updating featured content
* Quality of content featured given the content available and quality of text, thumbnails etc. and other assets used in promoting content

#### Instructions

There are three different "types" of featured content:

1. [Featured Categories](https://play.joystream.org/discover)
2. [Hero](https://play.joystream.org/)

* More information about 1. and 2. can be found [here](https://github.com/Joystream/atlas/blob/master/docs/community/featured-content.md).
* The access keys, or help, needed to make the changes will be granted to the Lead upon mentioning `@klaudiusz.eth#6880` and `@bwhm#6514` on discord.

#### Scoring Calculations

Let:

* `CATEGORIES_SCORE` be the score for updating the main featured categories on the platform, as a function of:
  * `HERO_CATEGORIES_CHANGE` be the amount of times all heros were changed during the council period
  * `VIDEO_CATEGORIES_CHANGE` be the amount of times the top video(s) in each categories were changed during the council period
* `HERO_SCORE` be the score for updating the main featured video on the platform, as a function of:
  * `HERO_CHANGE` be the amount of times the hero was changed during the council period
  * `HERO_CHANGE_QUALITY` be the subjective score of how well this is done, based on how frequently the same video is rotated back to the top, whether the "teaser" and metadata is correct, and whether the video is appropriate to feature (eg. good/bad video, not NSFW, etc.)
    * Note that Jsgenesis reserves the right to veto videos suggested for this position, as it's the first thing a new user sees, and should thus be of really high quality
* `LOGGING_SCORE` be the quality of the change logs in the notion board, so that grading can be done without having to check manually every day. This means creating a spreadsheet/table/db/json that every time a change is made

```
  CATEGORIES_SCORE = max[(HERO_CATEGORIES_CHANGE + VIDEO_CATEGORIES_CHANGE)/4 , 1]

  HERO_SCORE = max[(HERO_CHANGE + HERO_CHANGE_QUALITY)/4 , 1]

  # finally
  FEATURING_SCORE = (CATEGORIES_SCORE + HERO_SCORE + LOGGING_SCORE)/3
```

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

### `MIGRATION_SCORE`

We are approaching `carthage`, where no channel or videos will be migrated over. This means all channels needs to be evaluated for migration.

Over the course of the next 4 council periods, go through all channels and videos. For each period, process the a third of channels, create a table with (at least) 6 columns, namely:

* Channel ID
* Owner Member ID
* Video IDs:  a comma separated list of all videos in the channel
* Grade: a score between 0 and 3, where:
  * 3 means **all** videos in the channel are both of "good" quality, **and** does not violate any license, copyright or other parts of the content policy
  * 0 means **no** videos in the channel are both of "good" quality, **and** does not violate any license, copyright or other parts of the content policy
  * 2 and 1 means most, but not all, of the matches the requirements in 3 and 0 respectively
* Comments: for channels that are graded:
  * 2 - which videos should be excluded from migration and why.
  * 1 - which videos should be included in the migration and why.
* Checked: meaning who performed the check (member and discord handle), and when the check was made. This is to ensure we can check all channels that have been updated at the end, and in case of complaints, the community knows who to ask if there is an issue.

Share the table publicly with the community, so they can appeal.

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
