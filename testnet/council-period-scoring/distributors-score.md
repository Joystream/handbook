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

{% embed url="https://joystream.notion.site/Distribution-1f4cfbbb2e934c79bf20b8db7f019d32" %}
Distributor Working Group Knowledge Base
{% endembed %}



## Score

The score is computed as follows

```
DISTRIBUTOR_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + 2*SYSTEM_SCORE + COST_SCORE]/(6*2^{N})

```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with the metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must publish a separate report covering

* What was the setup of distribution family buckets, and buckets at the beginning and end of the term.
* What was the dynamic policy at the beginning and end of the term.
* How are bags distributed among the buckets in each bucket family.
* What was the rationale behind the family bucket and bucket configuration, meaning
  * What geographical regions are the families meant to serve
  * Why was the specific dynamic bag policy chosen
* How much bandwidth did the individual nodes consume during the period.
* How is the bandwidth usage distributed, meaning
  * How did bandwidth usage look over a day (peak hours and slow hours)
  * How did bandwidth usage look over a week (peak days and slow days)
  * How did bandwidth usage look across regions (which regions consumes the most, if accessible)
  * How did bandwidth usage look across nodes, operators, buckets and families
* How are distributors supposed to set their `config.yaml` file and why.
* What is the current running costs for the system, and a breakdown of said costs.
* What, if anything, is the group doing the monitor the health of the system.
* A list of all `storage` transactions (not `distributorWorkingGroup`) made by the lead, and the purpose behind them.
* An overview of which nodes that running with `--elasticSearchEndpoint`, what log level they are using, and how this information is used.

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `SYSTEM_SCORE`

Although well intended and partially correct given the purpose of `bucket_families` , the current system causes issues for many reasons, two of which are easy to fix:

* Buckets are assigned more bags than they should, and needs to fetch objects from a storage provider themselves, before they can serve them
* High latency between user, the player/orion and the distributor nodes, given most users residing Europe and the CIS

Redesign the distributor system, to reduce these errors.

#### Parameters

* **All** families/buckets are well distributed across Europe and the CIS (`coverage_score`)
  * No **active** distributor operates from any other geographical location
* All objects must be available from at least 2 operators in each family (`redundancy_score`)
* All distributor nodes are on the latest version of `argus` (`version_score`)
* All distributors that has been operating for more than 1 week (100,800 blocks), must maintain their own query node, and share the public url in the metadata (`autonomy_score`)
  * Will not be measured before scoring period 16
* All distributor nodes displays their location coordinates, node storage capacity and caching in the metadata,   (`transparancy_score`)
  * These should be the same numbers as `limits.storage` `limits.maxCachedItemSize` in the `config.yml` file
* No distributor node stores more than 80% of their capacity (`excess_capacity_score`)
  * This may severely reduce performance
* The maximum response time is 2h (`response_score)`

The first five subscores are measured at some point during the last 14400 blocks of the scoring period.

The latter will be measured by creating an opening for `@bwhm` without any rewards, that should be invited to a bucket and set as serving, but not accept any bags. If the node goes down, it must be set to not serving.

```
All subscores are graded binary

  SYSTEM_SCORE = (1/7)*(coverage_score + redundancy_score + version_score + autonomy_score + transparancy_score + excess_capacity_score + response_score)
```

### `COST_SCORE`

The cost score will try to measure how the group allocates their resources. Although being cost efficient is not a top priority for a testnet in general, it doesn't make much sense to:

* Employ a lot of operators that are not serving content
* Have operators store significantly less content than their capacity (especially cached capacity)
* Have operators run with costly hardware, and/or in expensive datacenters unless the benefit outweighs the extra costs

The score is the sum of two subscores:

1. A report documenting
   * Current costs
   * What can be done to reduce them (without impacting other scores)
   * What could be done to reduce them (may impact other scores), and why this may, or may not, be worth it
2. A subjective analysis by Jsgenesis, based on the report above and chain data. Any "excessive" costs not covered in the report will reduce the score, whereas costs that are documented will not.  An exeption to this rule is if a "cut" is not enacted in subsequent council periods.&#x20;

Jsgenesis will assign a score in the range \[0,1] based on this.

### Catastrophic Errors

#### **No available sources to fetch a data object from**

A data object is not available from any distributor, despite being held be an available storage node

#### Old version

A node is operating (set as serving content) while being on an older version 4h after an upgrade has been published.

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
