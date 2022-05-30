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
DISTRIBUTOR_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + SYSTEM_SCORE + RESEARCH_SCORE]/(5*2^{N})

```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with the metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`25%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must publish a separate report covering

* What was the setup of distribution family buckets, and buckets at the beginning and end of the term.
* What was the dynamic policy at the beginning and end of the term.
* How are bags distributed among the buckets in each bucket family.
* What was the rationale behind the family bucket and bucket configuration, meaning
  * What geographical regions are the families meant to serve
  * Why was the specific dynamic bag policy chosen
  * How do you want to scale the system assuming a growth of 2x, 10x and 100x in terms of data objects and size
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

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `SYSTEM_SCORE`

Although well intended and partially correct given the purpose of `bucket_families` , the current system causes issues for many reasons, two of which are easy to fix:

* Buckets are assigned more bags than they should, and needs to fetch objects from a storage provider themselves, before they can serve them
* High latency between user, the player/orion and the distributor nodes, given most users residing in eurasia

Redesign the distributor system, to reduce these errors.

#### Parameters

* All families/buckets well distributed across Europe and the CIS (`coverage_score`)
* All objects must be available from at least 2 buckets in each family
  * The top 10 most videos must be available from at least 3 buckets in each family (`redundancy_score`)
* All distributor nodes are on the latest version of `argus` (`version_score`)
* All distributor nodes displays their location coordinates and node capacity in the metadata,   (`transparancy_score`)
* No distributor node stores more than 60% of their capacity (`excess_capacity_score`)
* The maximum response time is 2h (`response_score)`

The first five subscores are measured at some point during the last 14400 blocks.

The latter will be measured by creating an opening for `@bwhm` without any rewards, that should be invited to a bucket and set as serving, but not accept any bags. If the node goes down, it must be set to not serving.

```
All subscores are graded binary

  SYSTEM_SCORE = (1/6)*(coverage_score + redundancy_score + version_score + transparancy_score + excess_capacity_score + response_score)
```

### `RESEARCH_SCORE`

**Notes**

In order to drive improvements, we need the group to also consider how we can improve the functionality of their core focus.

**Research Logging**

To evaluate a system like this, we need to make sure the individual node logs are available, and useful.

**`DEFAULT_LOGGING`** Review what is currently being logged by a distributor node, for each configurable `log-level`. Describe what information it provides, and in what way it can be used to improve the data in the current report, or what new statistics can be derived from it.

**`ELASTIC_LOGGING`** In the `config.yml` file `elastic` is commented out. Look into the codebase/documentation, and:

* deploy a server to act as the endpoint
* have a distributor node or two report to it, and compare the resource consumption before/after (a couple of times)
* make it public, so it can be used to debug and collect data
* create a guide that explains how to set it up, and use it to look at the logs

Note that the storage providers will have a similar task - consider collaborating.

#### Scoring Calculations

Jsgenesis will assign a score in the range \[0,1] based on:

* The quality of the report
* The quality of the guide
* The amount of nodes that connected to the server

### Catastrophic Errors

#### **No available sources to fetch a data object from**

A data object is not available from any distributor, despite being held be an available storage node

#### Old version

A node is operating (set as serving content) while being on an older version 4h after an upgrade has been published.

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
