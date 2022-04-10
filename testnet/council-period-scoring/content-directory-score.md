---
description: Metrics used to compute score for content directory working group.
---

# Content Directory Score

Overview

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
CONTENT_SCORE = [GENERAL_WG_SCORE + REPORT_SCORE + FEATURING_SCORE + MODERATION_SCORE]/(4*2^{N})
```

where

### `GENERAL_WG_SCORE`

Is computed with metrics defined in [general-working-group-score.md](general-working-group-score.md "mention") where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must include a section covering

* All channels and videos created.
* All channels and videos deleted.
* Amount of duplicate assets on chain, and what type they are (eg. video, channel cover, etc.)
* All moderation actions taken by the group, for which channels/video and why.
* All requests made to storage working group lead, related to moderation.
* Any changes made to the moderation policy, and why.
* Amount of videos hidden and censored.
* All changes made to the featured content.
* Categories created.
* A chart (with raw data available for future use) that plots the changes in the values below over the council period, through snapshots at every 600 block:
  * total playtime of videos available
  * total videos and channels
  * amount of members that own a channel

Whereas the same deadline as general report applies, there is no requirement to submit a temporary report for this.

### `FEATURING_SCORE`

_Objective:_ `The "Featured Content" must be changed frequently to keep fresh`

### Notes

`FEATURING_SCORE` is a score computed by Jsgenesis staff for the quality of featuring activity, which will be in the range \[0, 1], and will emphasize;

* Frequency of updating featured content
* Quality of content featured given the content available and quality of text, thumbnails etc. and other assets used in promoting content

#### Instructions

There are three different "types" of featured content:

1. [Featured Categories](https://play.joystream.org/discover)
2. [Hero](https://play.joystream.org)

* More information about 1. and 2. can be found [here](https://github.com/Joystream/atlas/blob/master/docs/community/featured-content.md).
* The access keys, or help, needed to make the changes will be granted to the Lead upon mentioning `@klaudiusz.eth#6880` and `@bwhm#6514` on discord.

#### Scoring Calculations

Let:

* `CATEGORIES_SCORE` be the score for updating the main featured categories on the platform, as a function of:
  * `HERO_CATEGORIES_CHANGE` be the score for how frequently the categories at the top row are changed, counted on a 24h basis
  * `VIDEO_CATEGORIES_CHANGE` be the score for how frequently the top video(s) in each categories are changed, counted on a 24h basis
  * `CATEGORIES_CHANGE_QUALITY` be the subjective score of how well this is done, based on how frequently the same videos are rotated back to the top, whether the "teaser" and metadata is correct, and whether the video is appropriate to feature (eg. actually representative of the category, good/bad video, not NSFW, etc.)
* `HERO_SCORE` be the score for updating the main featured video on the platform, as a function of:
  * `HERO_CHANGE_FREQUENCY` be the frequency of which the hero video is changed, where only changes once per day counts (as close as possible to a set time, eg. \~noon GMT)
  * `HERO_CHANGE_QUALITY` be the subjective score of how well this is done, based on how frequently the same video is rotated back to the top, whether the "teaser" and metadata is correct, and whether the video is appropriate to feature (eg. good/bad video, not NSFW, etc.)
    * Note that Jsgenesis reserves the right to veto videos suggested for this position, as it's the first thing a new user sees, and should thus be of really high quality
* `LOGGING_SCORE` be the quality of the change logs in the notion board, so that grading can be done without having to check manually every day. This means creating a spreadsheet/table/db/json that every time a change is made, shows:
  * `HERO`:
    * `entryId` the index of change (eg 0,1,2,...,n)
    * `blockheight+timestamp` denoting when changed
    * `videoId` of new video,
    * `metadata` used
    * (perma)`link` to teaser
    * `Delta_blockheight` showing how many blocks/days since the last time that vide was used as hero
    * `lastEntryIds` an array of `entryIds` with all the previous times the video was used
  * `CATEGORY`:
    * `entryId` the index of change (eg 0,1,2,...,n)
    * `blockheight+timestamp` denoting when changed
    * `changelog` showing the exact changes made, eg.
      * Top row: `Comedy/9,Gaming/7,Sports/5 -> Gaming/7,Film&Animation/1,Education/13`
      * Autoplay: `Pets&Animals/4: 22770->22769`
      * Top 6: ...

```
  CATEGORIES_SCORE = (0.5*HERO_CATEGORIES_CHANGE + 0.5*VIDEO_CATEGORIES_CHANGE) * CATEGORIES_CHANGE_QUALITY =
  0.5*[max(HERO_CHANGES_MADE/3,1) + max(VIDEO_CHANGES_MADE/3,1)] * CATEGORIES_CHANGE_QUALITY

  HERO_SCORE = HERO_CHANGE_FREQUENCY*HERO_CHANGE_QUALITY =
  max(CHANGES_MADE/3,1) * HERO_CHANGE_QUALITY

  # finally
  FEATURING_SCORE = (CATEGORIES_SCORE + HERO_SCORE + LOGGING_SCORE)/3
```

### `MODERATION_SCORE`

Content moderation is applied swiftly and appropriately.

#### Scoring Calculations

Let:

* `BLOCK_upload_i` be the blockheight of which a channel or video _i_, which should be moderated, is created.
* `BLOCK_moderated_i` be the blockheight of which a channel or video _i_, is moderated.
* `RULING_score_i` be the subjective score, set by Jsgenesis, whether the ruling _i_ made by the group was appropriate or not.

Then:

```
MODERATION_SCORE = 
Sum[RULING_score_i + (14400 -(BLOCK_moderated_i - BLOCK_upload_i)/14400)]/i
```



### Catastrophic Errors;

#### Failure to apply moderation rules

Any item which violates the content guidelines is unmoderated more than 24 hours after being uploaded

#### Featured Content Unplayable

If the hero video, or the hero of any category, is not playable and is not dealt within within 1 hour after the change
