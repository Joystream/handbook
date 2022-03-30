---
description: Metrics used to compute score for the forum working group.
---

# Forum Score

## Overview

The forum working group activities relevant to scoring will, generally, fall into one of the following categories

* Maintain a reasonable set of categories, allowing users to easily navigate the forum
* Moderate the forum
  * ideally, this means moving threads that were placed inappropriately, but also
  * includes censoring anything that violates the [ToS](todo)
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
Is computed with metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"), where the opportunity target is **`0%`**.


### `CATEGORY_SCORE`
*Objective:* `Finalize current forum category setup, under the current limitations`

#### Notes
Unfortunately, some runtime parameter/limits and interpretation of them, was not deployed correctly. The current ones are:
```
pub const MaxCategoryDepth: u64 = 6;
pub const MaxSubcategories: u64 = 20;
pub const MaxThreadsInCategory: u64 = 20;
pub const MaxPostsInThread: u64 = 20;
pub const MaxModeratorsForCategory: u64 = 20;
pub const MaxCategories: u64 = 20;
pub const MaxPollAlternativesNumber: u64 = 20;
pub const ThreadDeposit: u64 = 30;
pub const PostDeposit: u64 = 10;
pub const ForumModuleId: ModuleId = ModuleId(*b"mo:forum"); // module : forum
pub const PostLifeTime: BlockNumber = 3600;
```
#### Instructions
- With the limits above in mind, the plan for the forum structure had to be partially discarded.
- The ones that could be deployed were so, but it's not clear if the current structure is optimized in any way, or simply the result of creating 20 categories in "random" order, until it stopped
- Review the current one, and revise if necessary with two priorities in mind:
  1. Ease of use/quality of structure right now
  2. Ease of migrating to a new structure, where more categories are available, eg:
    - requires moving as few threads as possible (don't delete BEFORE the current ones are moved)
    - doesn't require moving any threads to a new "main/root" category, but simply to a new sub-category within the same ("main/root") category

#### Scoring Calculations
Let:
- `proposal_block` be the block number when a new structure is Proposed for Council approval.
- `changed_block`be the number of blocks, after approval from the Council, when the new, approved structure is implemented
- `category_quality_score` be the subjective grading of the implemented structure, taking into account the "quality of the structure", the presentation/readability of the proposal, the amount of threads deleted/moved to get there, etc.
- `category_score` be the final score [0,1]

Then:
```
  proposal_time_score = max[(90000 - proposal_block)/7200 , 1]
  changed_time_score = max[(proposal_approved_block + 2400 - changed_block)/1800 , 1]

  # finally
  CATEGORY_SCORE = 0.25*(proposal_time_score + changed_time_score) + 0.5*category_score
```

### `PARAMETER_SCORE`
*Objective:* `Propose new forum runtime values`

#### Notes
As stated above, there are some limits that probably needs to be configured for the forum to work well.

#### Instructions
Review the current ones, and propose new ones, given the following input:
- [current values link](https://github.com/Joystream/joystream/blob/9097670a51d4410d701d2a93f98c4eada1255ce0/runtime/src/lib.rs#L734)
- [module, with comments to some of these values](https://github.com/Joystream/joystream/blob/master/runtime-modules/forum/src/lib.rs)
  - You are not required to read or understand the code itself, but lots of considerations are commented (`/// all comments are written after three slashes`)
    - Further comments from dev shared [here](https://github.com/Joystream/community-repo/issues/737)
- [staging network for testing](https://pioneer-2.vercel.app/#/settings?network-config=https://18.207.235.254.nip.io/network/config.json)
  - DM Martin on discord for the Lead key, as testing is likely required
  - Hard deadline:
    - block `#144,000`

#### Scoring Calculations
The `PARAMETER_SCORE` is set subjectively.

### `MODERATION_SCORE`
*Objective:* `Create a set of moderation rules`

#### Notes
As for any forum, some moderation is likely required.
- Propose a moderation policy, if approved by the Council, add a (sticky) thread about it, and add it to the [notion space](https://www.notion.so/Forum-9d4eae77ce7544e0a860fbce4386805d).
- Separate between removing posts for censorship purposes, and moving a thread to the "correct" category.

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
