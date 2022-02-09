---
description: Metrics used to compute score for storage providers working group.
---

# Storage Providers Score

## Overview

The storage providers, coordinated by the lead, have to provide a storage system which performs well in the following terms

* Low latency and reliable uploading.
* Very low probability of permanent data loss
* High upload speed.
* High upload volume capacity: many simultaneous parallel uploads.
* A high upload speed to distributors.
* A low replication latency for a new data objects to all providers for the given bag.
* A low synchronization time of new storage providers.
* Basic level of denial of service resistance at the public upload API.

Jsgenesis staff will be conducting experiments to put load on the system, including denial of service attacks, spamming, and also posing as malicious workers.

## Collaboration

It is critical that the lead and workers collaborate to compile and share information with the council and Jsgenesis infrastructure maintainers about changes that are needed in terms of resources or tech.

`wip`- add more here when builders WG has been fleshed out.

\-jsgenesis

* council&#x20;
*

## Knowledge Base

{% embed url="https://grizzled-corleggy-af8.notion.site/Storage-9dc5a16444934dc4bda08b596bc15375" %}
Storage Providers Working Group Knowledge Base
{% endembed %}

## Score

The score is computed as follows

`[GENERAL_WG_SCORE + UPLOAD_ROBUSTNESS + UPLOAD_CAPACITY + REPLICATION_LATENCY + DOS_ROBUSTNESS]/(5*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `UPLOAD_ROBUSTNESS`: is the share of uploads of data objects where the first picked liason for a storage bucket starts accepting the upload within **`300ms`**, as measured on the client side.
* `UPLOAD_CAPACITY`: is computed
* `REPLICATION_LATENCY`: is the share of uploads of data objects where the latency from upload completion to _all_ storage providers for corresponding first picked liason for a storage bucket starts accepting the upload within **`300ms`**, as measured on the client side.
* `DOS_ROBUSTNESS`:
*
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
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors&#x20;

#### **Permanent Data Object Loss**

An inadequate report addendum about the bounties was provided, for example by missing or incorrect information.

Failed .

xxx
