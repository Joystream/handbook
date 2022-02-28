---
description: Metrics used to compute score for marketers working group.
---

# Marketers Score

## Overview

The marketing working group activities relevant to scoring fall into the following three categories:

* **Content Creation:** Creating blog posts, videos, graphics and other content to promote the project, and remixing content which may already exist (e.g. community calls) to be used in marketing campaigns.
* **Research:** Collecting information on the current state of the project and its base of participants, as well as researching other projects in the space as directed by Jsgenesis, the Council, or to facilitate current or future marketing campaigns.
* **Campaign Management:** Running paid and non-paid campaigns to promote the project, informed by the research conducted by the working group

## Content Creation

Content curation is a broad area which might range from monitoring improving listings of the project on DAO aggregator sites or PolkaProject, to designing and writing landing pages for advertising campaigns or creating videos about any aspect of the project.

Another important element of content creation is remixing content which already exists. For example, creating tweets, blog posts and shorter video clips based on community calls.

## Research

A deep understanding of the project and where it fits into the wider crypto space is essential to being able to conduct effective marketing campaigns and produce impactful content.

For this reason, the marketing WG score will place some emphasis on the effectiveness of research activity conducted by the working group. Basically, we are looking for any useful information which will provide useful information for improving marketing activity (or any other aspect of the project).

Research might explore similar projects in the space and compare them to Joystream, or might involve creating surveys to understand our current base of participants. This research may be partially directed by Jsgenesis, but will also rely on the working group defining some of its own questions which research might help to answer.

## Campaign Management

Running marketing campaigns to increase participation in the project is the fundamental goal of establishing the marketing working group. These can take a variety of formats, but all will be scored based on a combination of factors, including the quality of planning, clarity and specificity of campaign objectives and the quality and presentation of data collected about ongoing campaigns.

## Knowledge Base

{% embed url="https://grizzled-corleggy-af8.notion.site/Marketers-e9c39c5089694ddd9a64087c831216f3" %}
Marketers Working Group Knowledge Base
{% endembed %}

## Score

The marketing working group score is computed as follows

`[GENERAL_WG_SCORE + CONTENT_SCORE + RESEARCH_SCORE + CAMPAIGN_SCORE]/(4*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `CONTENT_SCORE`:  is a score computed by Jsgenesis staff for the quality and volume of content produced, which will be in the range \[0, 1], and will emphasize
  * Quality of content produced and alignment with our branding guidelines
  * Quantity of content produced relative to the source material available
* `RESEARCH_SCORE`: is a score computed by Jsgenesis staff for the quality of research activity, which will be in the range \[0, 1], and will emphasize&#x20;
  * Robustness of data collection methods
  * Usefulness of data being collected
  * Amount of research being conducted given resources available
  * Clarity of conclusions reached based on campaign data
* `CAMPAIGN_SCORE`: is a score computed by Jsgenesis staff for the quality of campaign management activity, which will be in the range \[0, 1], and will emphasize
  * General quality of planning
  * Clarity and specificity of campaign objectives
  * Quality and presentation of data collected about ongoing campaigns
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors&#x20;

#### **Misinformation**

Any material published by the marketing working group contains gross inaccuracies or exaggerations.

#### Branding Failure

Any material published by the marketing working group which represents a significant departure from brand guidelines.
