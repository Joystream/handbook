---
description: Metrics used to compute score for storage providers working group.
---

# Storage Providers Score

## Overview

`wip`

## Knowledge Base

{% embed url="https://grizzled-corleggy-af8.notion.site/Storage-9dc5a16444934dc4bda08b596bc15375" %}
Storage Providers Working Group Knowledge Base
{% endembed %}

## Score

The HR working group score is computed as follows

`[GENERAL_WG_SCORE + GREETING_SCORE + ONBOARDING_SCORE + CATALYZING_SCORE + BOUNTY_MANAGEMENT]/(5*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `GREETING_SCORE`:  is a score computed by Jsgenesis staff for the quality and speed of the greeting activity, which will be in the range \[0, 1], and will emphasize
  * Latency: the time it takes from a new person joining until someone gets in touch. Between **`8am` ** to **`23pm`** (CET), greeting time must be less than **`2 minutes`**.
  * Capture: The% of interactions that lead to a membership getting created and data entered into CRM, and the quality of this data.
* `ONBOARDING_SCORE`: is a score computed by Jsgenesis staff for the quality of onboarding activity, which will be in the range \[0, 1], and will emphasize the % of captured persons who are&#x20;
  * assigned a bounty
  * apply for a working group role with a credible application
  * stand for the council with a credible candidacy
  * have a bounty created for them
* `CATALYZING_SCORE`: is `1/percentile(75%, [x_1, ..., x_l])` , which will be in the range \[0, 1], where&#x20;
  * `percentile(X,S)` returns the `X`th percentile in non-empty sequence of observations _S._&#x20;
  * `x_i` is the number of days since the last registered interaction in the CRM with the ith non-founding member in the CRM as of the end of the period.&#x20;
* `BOUNTY_MANAGEMENT` : is a score computed by Jsgenesis staff for the quality of bounty management, which will be in the range \[0, 1].
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors&#x20;

#### **Inadequate Report**

An inadequate report addendum about the bounties was provided, for example by missing or incorrect information.

**Budget Template Violation**

A bounty was created with an amount of $tJOY exceeding the current template budget.

**Missing Judgement**

A bounty did not receive oracle judgement.
