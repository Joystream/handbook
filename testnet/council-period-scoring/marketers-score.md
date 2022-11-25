---
description: Metrics used to compute score for marketers working group.
---

# Marketers Score

## Overview

The marketing working group activities relevant to scoring, will generally fall into one of the following categories:

* **Recruiting Testnet Participants:** Work hand-in-hand with Jsgenesis marketing team on recruiting more testnet participants to join Joystream.
* **Research:** Collecting information on the current state of the project and its base of participants, as well as researching other projects in the space as directed by Jsgenesis, the Council, or to facilitate current or future marketing campaigns.
* **Content Creation:** Creating blog posts, videos, graphics and other content to promote the project, and remixing content which may already exist (e.g. community calls) to be used in marketing campaigns.

## **Recruiting Testnet Participants**

This is the perfect job for that person who is “always online” and loves to chat with people. You will follow a simple framework for sourcing, posting, and converting testnet participants. During the process you will be coached directly by the CMO at Jsgenesis. You just need a basic understanding of Joystream, and live in Discord. We’ll help you with the rest.

## Research

A deep understanding of the project and where it fits into the wider crypto space is essential to being able to conduct effective marketing campaigns and produce impactful content.

For this reason, the marketing WG score will place some emphasis on the effectiveness of research activity conducted by the working group. Basically, we are looking for any useful information which will provide useful information for improving marketing activity (or any other aspect of the project).

Research might explore similar projects in the space and compare them to Joystream, or might involve creating surveys to understand our current base of participants. This research may be partially directed by Jsgenesis, but will also rely on the working group defining some of its own questions which research might help to answer.

## Content Creation

Content curation is a broad area which might range from monitoring improving listings of the project on DAO aggregator sites or PolkaProject, to designing and writing landing pages for advertising campaigns or creating videos about any aspect of the project.

Another important element of content creation is remixing content which already exists. For example, creating tweets, blog posts and shorter video clips based on community calls.

## Knowledge Base

{% embed url="https://joystream.notion.site/Marketers-e9c39c5089694ddd9a64087c831216f3" %}
Marketers Working Group Knowledge Base
{% endembed %}

## Score

The Marketing working group score is computed as follows

```
HOLD
```

**No metrics for period 31.**

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention") where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-summary](./#working-group-summary "mention") the working group report must publish a separate report covering working group specific stats

* A summary of the recruiting process for the period, including
  * Discord groups visited and for each
    * a TL;DR about the discord group/project visited
    * the opening message that was posted
    * amount of users engaging over DMs
    * how many users
      * joined our discord
      * was added to the CRM (get `personId)`
      * registered a membership (get `memberId`)
      * got assigned a bounty (get `bountyId`)
  * Perform a status update for all users recruited, by an entry in the `CRM` in previous periods.
    * How many were assigned a bounty, and how many how many completed it?
    * How many has had a role?
    * What are the biggest success stories, and what can we learn from that?

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `RECRUITING_SCORE`

For the inaugural version of this, the metrics will be published after the group has scheduled a call with `cmo#1656` for an introduction and workflow discussion. Then a brief training.

Note that we will start small here, and only two marketers will be "allowed" to be measured.

### `DOCUMENTATION_SCORE`

The handbook can be divided in to two parts, namely `system` and `testnet`.

The system part contains lots of technical details, not critical for all users to understand, but also lots of guides that should be simple enough to follow. It rarely gets updated and a high standard is required to contribute.

The testnet part is perhaps more relevant for the current community members, as it's the key to earning $JOY. Unlike the system parts, it has to get updated frequently, and as a consequence, many flaws have been introduced.

**Resources**

* the [handbook repo](https://github.com/Joystream/handbook)
* a "fork" of the old (and deleted) [helpdesk repo](https://github.com/bwhm/helpdesk/tree/giza)
* all Joystream [notion boards](https://joystream.notion.site/Joystream-Workspace-1175fcb1cc644fdb874558181fd2dbee)
* our discord

`System`: Go through two sections, Memberships and Working Groups

`Testnet`: Review the entire part and ask workers in each group

* Locate all issues, and describe them in detail
* Propose how to fix the issues to the sections
* Perform an internal review
* Create an issue in the handbook repo with all of the above, and assign `@bwhm` to review.

&#x20;Let:

* `system_score` be a score in the range \[0,1] set by Jsgenesis staff
* `testnet_score` be a score in the range \[0,1] set by Jsgenesis staff

```
DOCUMENTATION_SCORE = (system_score + testnet_score)/2
```

### Catastrophic Errors <a href="#catastrophic-errors" id="catastrophic-errors"></a>

#### **Inadequate Report** <a href="#inadequate-report" id="inadequate-report"></a>

The report doesn't address the statistics requested, even if there is nothing new.

#### **Workflow Violation** <a href="#inadequate-report" id="inadequate-report"></a>

Any deviance from the workflows is not accepted.
