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
FORUM_SCORE = [3*CATEGORY_SCORE + USAGE_SCORE]/(5*2^{N})
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `CATEGORY_SCORE`

1. Create a set of initial categories for the Forum, and ensure it works
2. Request feedback from the Community
3. With the below in mind, create a proposal to the Council outlining the categories and hierarchy within
4. If approved, implement the changes. If not, revise and repeat 4

The score for of the above accounts for 25% of the final score, which will be in the range \[0, 1].

The score will decrease by 10% for each hour of delay, given the following deadlines:

1. 24h from `#216,000`
2. 24h from `#216,000`
3. Allow 24h of feedback, then 12h to create proposal
4. Implement changes, without breaking anything, within 12h of approval; OR\
   Create a new proposal within 12h of rejection

### `USAGE_SCORE`

Not (just) the Forum Lead to decide, but there a plethora of ways the community CAN communicate. Discord is probably the fastest, the proposal system is probably best for "big" things, and DMs are probably better for non-public communication or smalltalk.

However, the forum has it's benefit given that it's easy for all to know who you're talking with, and the messages are (somewhat) permanent.

Draft a proposal outlining this.

### Catastrophic Errors

#### **Violation of Content Policy**

Although not strictly the same, the concepts in the content policy applies to the forum as well. Any post or thread fitting the above, left unmoderated for 12h.

#### **Unwarrented deletion of a post or thread**

Any thread or post that gets deleted, for any reason, must be justified in the report. If the grounds are found unwarranted (ie. not in line with any policy), or simply not mentioned in any report, it counts as a catastrophic error.

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
