---
description: Metrics used to compute score for the forum working group.
---

# Forum Score

## Overview

The forum working group activities relevant to scoring will, generally, fall into one of the following categories

* Maintain a reasonable set of categories, allowing users to easily navigate the forum
* Moderate the forum
  * ideally, this means moving threads that were placed inappropriately, but also
  * includes censoring anything that violates the [content policy](/system/content-directory/content-policy.md)
* Forum (tech) support,
  * Including maintaining guides for how the forum works from a user point of view

Jsgenesis staff may in some cases create posts or threads that the working group should deal with in one way or another.

## Knowledge Base

{% embed url="https://joystream.notion.site/Distribution-1f4cfbbb2e934c79bf20b8db7f019d32" %}
Distributor Working Group Knowledge Base
{% endembed %}

## Report

The working group report should include a special section with information about

* Changes made to category structure
* Forum statistics
* All actions taken by the group

## Score

The score is computed as follows

```
FORUM_SCORE = [0.1*GENERAL_WG_SCORE + 0.7*MODERATION_SCORE + 0.2*NOTIFICATION_SCORE]/(2^{N})
```

where

### `GENERAL_WG_SCORE`
Is computed with metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"), where the opportunity target is **`0%`**.

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

* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors


#### **Violation of Content Policy**

Although not strictly the same, the concepts in the [content policy](/system/content-directory/content-policy.md) applies to the forum as well. Any post or thread fitting the above, left unmoderated for 12h.
