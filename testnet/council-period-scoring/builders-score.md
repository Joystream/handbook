---
description: Metrics used to compute score for builders working group.
---

# Builders Score

## Overview

The operations working group is unlike other working groups, in that they are only really being measured based on the quality of their output, as judged by Jsgenesis.&#x20;

The working group is exclusively focussed on developing tools and enhancing existing applications (Pioneer, Atlas, CLI etc.) and the runtime which come together to make the Joystream platform as a whole.\
\
Their contributions to these tools and the creation of new ones are represented as a development score, which attempts to measure the volume and quality of development based on the resources available to the working group.\
\
It should be kept in mind that this development activity is not purely restricted to Jsgenesis tools and projects, but can also apply to community projects such as [JoystreamStats](https://joystreamstats.live).

## Knowledge Base

{% embed url="https://grizzled-corleggy-af8.notion.site/Builders-ffb1c9d1d1094fc4a6f04eb47677673d" %}
Builders Notion knowledge base
{% endembed %}

## Score

The builders working group score is computed as follows

`[GENERAL_WG_SCORE + DEVELOPMENT_SCORE]/(2*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `DEVELOPMENT_SCORE`: is a score computed by Jsgenesis staff for the quality and volume of development activity, which will be in the range \[0, 1], and will emphasize
  * Quality of development activity and alignment with project objectives, as defined by the Council and Jsgenesis
  * Quantity of development taking place relative to the resources available (e.g. measured in lines of code)
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors

#### **Inadequate Report**

An inadequate report about the working group was provided, for example by missing or incorrect information.
