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
FORUM_SCORE = 0.1*GENERAL_WG_SCORE + 0.35*CATEGORY_SCORE + 0.3*PARAMETER_SCORE + 0.05*MODERATION_SCORE + 0.2*GUIDE_SCORE
```

where

### `GENERAL_WG_SCORE`
Is computed with metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"), where the opportunity target is **`20%`**.

### `MODERATION_SCORE`

#### Notes
As for any forum, some moderation is likely required.

Apply the moderation policy, and for each occurrence, make an entry of it in a spreadsheet/table on the groups notion space.

#### Scoring Calculations
The `MODERATION_SCORE` is set subjectively.

### `GUIDE_SCORE`
*Objective:* `Create a howto guide for Forum Workers`

#### Notes
Until now, the Joystream "howto" guides in general has been available in the helpdesk. The Forum WG is brand new, so not really applicable, but we are moving away from this, and want guides hosted in the groups [notion space](https://joystream.notion.site/Forum-9d4eae77ce7544e0a860fbce4386805d).
- Create a user friendly "landing page", that explains:
  - the purpose of the role
  - the tools required
  - how to apply for the role
  - other relevant information and links
  - a visual of the current category structure, and the philosophy behind it
  - a visual of the (imagined future) category structure, and the philosophy behind it
- Add the technical instructions required for working as a Forum Lead/Worker, basically explain/example for all cli commands
  - how to create/delete/update categories
  - how to "sticky" threads
  - how to moderate

#### Scoring Calculations
The `GUIDE_SCORE` is set subjectively.

* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors
NA
