---
description: Metrics used to compute score for distributors working group.
---

# Distributors Score

## Overview

The distributors, coordinated by the lead, have to provide a distribution system which performs well in the following terms

* Low latency and reliable downloading.
* High download speed.
* High download volume capacity: many simultaneous parallel downloads.
* A high download speed from storage providers.
* A low replication latency for a new data objects to all distributors for the given bag.
* A low synchronization time of new distributors.

Jsgenesis staff will be conducting experiments to put load on the system, including denial of service attacks, spamming, and also posing as malicious workers. **Expect Jsgenesis to rent botnet services or other denial of service infrastructure to simulate at scale attacks.**

## Knowledge Base

{% embed url="https://grizzled-corleggy-af8.notion.site/Distribution-1f4cfbbb2e934c79bf20b8db7f019d32" %}
Distributor Working Group Knowledge Base
{% endembed %}

## Report

The working group report should include a special section with information about

* What data objects were permanently lost.
* How many bags were created.
* How many bags were deleted.
* How many data objects were downloaded, and
  * what was their total size,
  * what was the size distribution.
* Distribution of bag sizes in terms of data object counts.
* Distribution of bag sizes in terms of total data object size.
* Total capacity of all distribution bucket limits.
* Total used capacity of all distribution buckets.

## Score

The score is computed as follows

`[GENERAL_WG_SCORE + UPLOAD_ROBUSTNESS + UPLOAD_CAPACITY + REPLICATION_LATENCY + DOS_ROBUSTNESS]/(5*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `DOWNLOAD_ROBUSTNESS`: is the share of uploads of data objects where the first picked liason for a storage bucket starts accepting the upload within **`300ms`**, as measured on the client side.
* `DOWNLOAD_CAPACITY`: is 1, will be defined later.
* `REPLICATION_LATENCY`: is the share of uploads of data objects where the latency from upload completion to _all_ storage providers for corresponding first picked liason for a storage bucket starts accepting the upload within **`300ms`**, as measured on the client side.
* `DOS_ROBUSTNESS`: is a score computed by Jsgenesis staff for the ability to withstand DoS and DDoS attacks, which will be in the range \[0, 1], and will emphasize handling of attacks of the following kinds
  * ICMP Flooding/ Smurf Attack
  * SYN Flooding
  * Ping of Death
  * HTTP (GET/POST) Flooding
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors

#### **Permanent Data Object Loss**

A confirmed data object can no longer be recovered from storage nodes, despite not being deleted on chain.
