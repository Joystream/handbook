---
description: Metrics used to compute score for the forum working group.
---

# Forum Score

## Overview

The forum working group activities relevant to scoring will, generally, fall into one of the following categories

* Maintain a reasonable set of categories, allowing users to easily navigate the forum
* Moderate the forum
  * ideally, this means moving threads that were placed inappropriately, but also
  * includes censoring anything that violates the content policy
* Forum (tech) support,
  * Including maintaining guides for how the forum works from a user point of view

Jsgenesis staff may in some cases create posts or threads that the working group should deal with in one way or another.

## Knowledge Base

{% embed url="https://joystream.notion.site/Distribution-1f4cfbbb2e934c79bf20b8db7f019d32" %}
Distributor Working Group Knowledge Base
{% endembed %}

## Score

The score is computed as follows

```
FORUM_SCORE = [GENERAL_WG_SCORE + REPORT_SCORE + MODERATION_SCORE + NOTIFICATION_SCORE]/(4^{N})
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with metrics defined in , where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-summary](general-working-group-score.md#working-group-summary "mention"), the working group report must include a section covering

* Changes made to category structure, and why
* Forum statistics over the course of the scoring period, meaning
  * How many threads were created
  * How many threads were deleted
  * How many posts were created of each type
  * How many posts were deleted
* A summary of all `forum` (except regular posting) transactions made by the group, who made it, and why

Whereas the same deadline as general report applies, there is no requirement to submit a temporary report for this.

### `MODERATION_SCORE`

#### Notes

As for any forum, some moderation is likely required.

Apply the moderation policy, and for each occurrence, make an entry of it in a spreadsheet/table on the groups notion space.

#### Scoring Calculations

The `MODERATION_SCORE` is set subjectively.

### `NOTIFICATION_SCORE`

#### Notes

A user that posts on the forum may have a question either towards a the council, a lead, a Worker, Jsgenesis or just a member of the platform. However, that person may not see it.

When a question is raised, that is either directly or indirectly best handled by someone else, help the user by tagging the appropriate person on Discord.

#### Scoring Calculations

The `NOTIFICATION_SCORE` is set subjectively.

### Catastrophic Errors

#### **Violation of Content Policy**

Although not strictly the same, the concepts in the content policy applies to the forum as well. Any post or thread fitting the above, left unmoderated for 12h.



### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
