---
description: Metrics used to compute score for marketers working group.
---

# Marketers Score

## Overview

The marketing working group activities relevant to scoring, will generally fall into one of the following categories:

* **Content Creation:** Creating blog posts, videos, graphics and other content to promote the project, and remixing content which may already exist (e.g. community calls) to be used in marketing campaigns.
* **Research:** Collecting information on the current state of the project and its base of participants, as well as researching other projects in the space as directed by Jsgenesis, the Council, or to facilitate current or future marketing campaigns.

## Content Creation

Content curation is a broad area which might range from monitoring improving listings of the project on DAO aggregator sites or PolkaProject, to designing and writing landing pages for advertising campaigns or creating videos about any aspect of the project.

Another important element of content creation is remixing content which already exists. For example, creating tweets, blog posts and shorter video clips based on community calls.

## Research

A deep understanding of the project and where it fits into the wider crypto space is essential to being able to conduct effective marketing campaigns and produce impactful content.

For this reason, the marketing WG score will place some emphasis on the effectiveness of research activity conducted by the working group. Basically, we are looking for any useful information which will provide useful information for improving marketing activity (or any other aspect of the project).

Research might explore similar projects in the space and compare them to Joystream, or might involve creating surveys to understand our current base of participants. This research may be partially directed by Jsgenesis, but will also rely on the working group defining some of its own questions which research might help to answer.

## Knowledge Base

{% embed url="https://joystream.notion.site/Marketers-e9c39c5089694ddd9a64087c831216f3" %}
Marketers Working Group Knowledge Base
{% endembed %}

## Score

The marketing working group score is computed as follows

```
MARKETING_SCORE = 0.1*GENERAL_WG_SCORE + 0.40*ISSUES_SCORE + 0.35*GITBOOK_SCORE + 0.15*GLOSSARY_SCORE
```

where

### `GENERAL_WG_SCORE`
Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`0%`**.

### `ISSUES_SCORE`
*Objective:* `Review Marketing issues`

#### Instructions
The marketing github repo has a lot of open [issues](https://github.com/Joystream/marketing/issues). Many of these are far outside the scope we want the WG to address, but some of them are not. Especially those that requires up front research of publicly available data.
Go through as many issues as possible, and produce a spreadsheet/table in the [notion space](https://joystream.notion.site/Marketers-e9c39c5089694ddd9a64087c831216f3) containing all (open issues) and comment:
- A one-liner on what the issue is about
- Assign it one of three categories:
  - `out-of-scope`
  - `maybe-in-scope`
  - `in-scope`
- If `in-scope` comment in the issue::
  - why you think this is something the group can do
  - what resources you'd need (if any)
  - what you imagine the deliverable is
  - link to the comment in the spreadsheet
- For all `maybe-in-scope` issues, create a _single new_ issue in said repo, and
  - list them all
  - add a quick comment on why you think it might be something the group can address
  -  what stops you from marking it `in-scope`
  - what you'd "need" to put it there
#### Scoring Calculations
Let:
- `issues_addressed` be the amount of issues added to the notion space, with comment
- `grading` be the subjective grading JSG assigns [0,1]
Then:
```
  ISSUES_SCORE = grading * (issues_addressed--40)/60
```

### `GITBOOK_SCORE`
*Objective:* `Propose Gitbook improvements`

#### Instructions
Our [gitbook](https://joystream.gitbook.io/testnet-workspace/) contains a lot of holes, broken links and hard to parse language. Although some parts of it will naturally have to be "difficult" to understand for non-technical users, the basic concepts should not be. Let's focus on what is there for now, as a lot of holes will be "filled" during the week.

Oftentimes, confusion will stem from either language barriers, or a concept being explained "too" succinctly with technical terms. Many of these can be overcome by adding a visual representation. In other cases, a complex concept requires examples, analogies, or just a longer/better explanation.
Produce a spreadsheet/table in the [notion space](https://joystream.notion.site/Marketers-e9c39c5089694ddd9a64087c831216f3), go through the gitbook as it stands and each time you struggle to understand something, or suspect lots of users will:
- Link to the section
- Add a short note what makes it difficult
- Suggest a (conceptional) solution, eg:
  1. "Add a [chart|graph|image] (visual) representation"
  2. "Use [an|this] analogy here"
  3. "Elaborate more on this"
  4. "Rewrite entirely"
  5. etc
- Feel free to make a complete suggestion as well. If it's really good, that will be add to your score, but if it's just a little better, no credit is given. The exception is 1. where a wireframe/MS paint rough sketch/draft is likely better than trying to make it perfect.

#### Scoring Calculations
Let:
- `identified_i` be a "problematic" part identified and added to the notion space, with comments
  - `identified_grading_i` be a binary [yes|no] whether the input was valuable
  - `suggestion_i` be a (potential) solution to a "problematic" part
  - `suggestion_grading_i` be the subjective grading JSG assigns [0,1] to a (potential) solution
Then:
```
  GITBOOK_SCORE = max[Zigma(identified_grading_i * identified_i)*0.8 * (i-10/30) + Zigma(suggestion_grading_i * suggestion_i) , 1]
```

#### Scoring Calculations
Let:
- `issues_addressed` be the amount of issues added to the notion space, with comment
- `grading` be the subjective grading JSG assigns [0,1]

Then:
```
  ISSUES_SCORE = grading * (issues_addressed-50)/100
```

### `GLOSSARY_SCORE`
*Objective:* `Propose a Gitbook glossary`

#### Instructions
Our [gitbook](https://joystream.gitbook.io/testnet-workspace/) also contains a far amount of technical terms.
While doing the above, create a list of terms that should go in the glossary, and add them to the [notion space](https://www.notion.so/joystream/Marketers-e9c39c5089694ddd9a64087c831216f3), along with:
- (a) link(s) to where the term is used
- why it needs to be there
- an attempt at the definition (if you understand it!)
  - IF a term only applies to a specific section - a category

#### Scoring Calculations
Let:
- `identified_i` be a difficult term identified and added to the notion space, with comments
  - `identified_grading_i` be a binary [yes|no] whether the input was valuable
Then:
```
  GLOSSARY_SCORE = Zigma(identified_grading_i * identified_i) * (i-10/10)
```
