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
FORUM_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + MODERATION_SCORE + CATEGORY_SCORE]/(5*2^{N})
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with metrics defined in , where the opportunity target is **`25%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-summary](general-working-group-score.md#working-group-summary "mention"), the working group report must include a section covering

* Forum statistics over the course of the scoring period, meaning
  * How many threads were created
  * How many threads were deleted
  * How many posts were created of each type
  * How many posts were deleted
* For each category
  * How many threads exists, and how many was created during the last scoring period
  * How many posts exists, and how many was created during the last scoring period
* Charts showing the forum history over time
  * Threads made since genesis
  * Posts made since genesis
* A summary of all `forum` (except regular posting) transactions made by the group, who made it, and why, eg.
  * Moderation of threads
  * Moderation of posts
  * Threads moved
  * Categories changed, deleted or created

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `MODERATION_SCORE`

#### Notes

As for any forum, some moderation is likely required.

Apply the moderation policy, and for each occurrence, make an entry of it in a spreadsheet/table on the groups notion space.

#### Scoring Calculations

The `MODERATION_SCORE` is set subjectively.

### `CATEGORY_SCORE`

#### Notes

With the runtime upgrade at block `#697,500`, we know have gone from 20 to 40 max categories. This means we can implement the previously designed system, or a new better one.

There are multiple tasks associated with this metric:

1. OPTIONAL: If the old, previously approved, system is found lacking, design a new system of categories and sub-categories.
2. Get an proposal for a/the new category system approved by the Council. If a "brand" new system is designed, the proposal must include a design brief to explain the reasoning behind it. Regardless, it must include a an overview of:
   * Which, if any, categories or subcategories should be deleted or moved
   * Which, if any, threads should be moved
3. Implement the new category system, without deleting any threads or posts.

#### Scoring Calculations

If the changes made

* are not approved by the council
* are not implemented exactly as approved (without technical reasons) before the end of the term
* ends up permanently deleting any post or thread

the score is automatically zero.

### Catastrophic Errors

#### **Violation of Content Policy**

Although not strictly the same, the concepts in the content policy applies to the forum as well. Any post or thread fitting the above, left unmoderated for 12h.

#### **Unwarrented deletion of a post or thread**

Any thread or post that gets deleted, for any reason, must be justified in the report. If the grounds are found unwarranted (ie. not in line with any policy), or simply not mentioned in any report, it counts as a catastrophic error.

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
