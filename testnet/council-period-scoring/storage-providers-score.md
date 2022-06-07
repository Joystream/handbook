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

Jsgenesis staff will be conducting experiments to put load on the system, including denial of service attacks, spamming, and also posing as malicious workers. **Expect Jsgenesis to rent botnet services or other denial of service infrastructure to simulate at scale attacks.**

## Knowledge Base

{% embed url="https://joystream.notion.site/Storage-9dc5a16444934dc4bda08b596bc15375" %}
Storage Providers Working Group Knowledge Base
{% endembed %}



## Score

The score is computed as follows

```
STORAGE_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + SYSTEM_SCORE + UPLOAD_SCORE + RESEARCh_SCORE]/(6*2^{N})

```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `GENERAL_WG_SCORE`

Is computed with the metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must include a section covering

* How many storage buckets were created.
* How many storage buckets were deleted.
* What was the capacity and utilization of each storage bucket at the beginning and end of the term (number and size of data objects).
* How many bags were created.
* How many bags were deleted.
* What data objects were permanently lost, and if any, why.
* How many data objects were (attempted) uploaded, and
  * what was their total size,
  * what was the size distribution.
* List of failed data upload upload attempts on chain, and if possible to find out - why.
  * If this is not done, the `UPLOAD_SCORE` will assume all uploads failed independently, and that the group is at fault.
* A chart (with raw data available for future use) that plots the changes in the values below over the council period, through snapshots at every 600 block:
  * data objects, number and size;
  * amount of bags;
  * (average) number and size of data objects in a bag
* What is the current running costs for the system, and a breakdown of said costs.
* How much bandwidth did the individual nodes consume during the period.
* What, if anything, is the storage group doing the monitor the health of the system.
* A list of all `storage` transactions (not `storageProviderWorkingGroup`) made by the lead, and the purpose behind them.
* The values used as inputs for the subscores `excess_capacity_score` and `emergency_score` under the `SYSTEM_SCORE`.

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `SYSTEM_SCORE`

Many things are required for the storage system to function as intended.  It needs

* to be **robust** enough to survive 2-3 nodes going down at the same time
* **redundancy** in case of a burst of new uploads
* to be **configured** well enough to function without intervention in case of personal issues or other
* to be **responsive** enough to handle changing circumstances quickly
* **monitoring** to notice the changing circumstances

This score will likely see changes over time, to add remaining metrics.

* This means we want all new objects to be, by default, without manual intervention, to be stored by multiple nodes.
* "Operating/operated" means that a bucket is assigned to a Worker, the worker is running a node that can be uploaded to (by a channel owner) and downloaded from (by a distributor)
* Having configured the `dynamic_bag_policy` policy is only the first step! Example:
  * dynamic bag policy is 3 and buckets 0-6 can all accept a new bags
    * if bucket 0 is "full" (meaning max objects or size is reached), or down, that means the system CAN in fact halt, despite 1-5 all working.

#### Parameters

* The minimum replication rate is 5 (`replication_score`)
*   The excess capacity required, for objects and size, must be higher than the "worst" of:

    * 4x last period numbers (not current)
    * 3x the highest period over the last 4 periods (not including current)

    (`excess_capacity_score`)
*   Maximum allowed failure probability is 80%, meaning all bags in the top 10% of EITHER:

    * total size stored
    * total objects stored
    * amount of uploads over the last period

    must be able to have at least 80% chance of being able to upload 1 object successfully, despite 2 storage nodes hypotethically being down (`emergency_score)`
* The maximum response time is 2h (`response_score)`

The first three subscores are measured at some point during the last 14400 blocks.

The latter will be measured by creating an opening for `@bwhm` without any rewards, that should be invited to a bucket, but not set to accept new bags, and only (manually) assigned a single existing "testing" bag. If the node goes down, the bag must be removed.

#### Scoring Calculations

Then:

```
 All subscores are graded binary

  SYSTEM_SCORE = 0.25*(replication_score + excess_capacity_score + emergency_score + response_score)
```

### `UPLOAD_SCORE`

_Objective:_ `Keep failed uploads under 5%`

#### Notes

* In general, dataObjects added that was not part of the migration, where `isAccepted=false` means a failed upload. However, to keep it "fair":
  * if it can be "proven" that the error was caused by Jsgenesis, or the uploader, it isn't counted. The burden of proof is on the Storage Lead/Worker/Council
  * neither are multiple instances of the same failure (say, a user tries again, and the same bucket/storage-node fails), that occurs within an hour of the first error
    * after that, we assume the operator will resolve the problem, the bag will be moved, or the issue is fixed in some other way

#### Scoring Calculations

Let:

* `successful_uploads` be any new dataObject added (that counts) where `isAccepted=true`
* `counting_uploads` be any new dataObject added, (that counts)
* `UPLOAD_SCORE` be the final score \[-1,1]

Then:

```
  UPLOAD_SCORE = (successful_uploads/total_uploads - 0.85)/0.15
```

### `RESEARCH_SCORE`

**Notes**

In order to drive improvements, we need the group to also consider how we can improve the functionality of their core focus.

**Research Logging**

To evaluate a system like this, we need to make sure the individual node logs are available, and useful.

**`DEFAULT_LOGGING`** Review what is currently being logged by a storage node, for each configurable `log-level`. Describe what information it provides, and in what way it can be used to improve the data in the current report, or what new statistics can be derived from it.

**`ELASTIC_LOGGING`** There is an option for the storage node to run with `-e URL`, meaning logs, with configurable verbosity can be uploaded to an endpoint.

* deploy a server to act as the endpoint
* have a storage node or two report to it, and compare the resource consumption before/after (a couple of times)
* make it public, so it can be used to debug and collect data
* create a guide that explains how to set it up, and use it to look at the logs
* use the most verbose log level, and IF that `LOG_LEVEL` differs from what was found in `DEFAULT_LOGGING`, outline what is added

Note that the distributors will have a similar task - consider collaborating.

#### Scoring Calculations

Jsgenesis will assign a score in the range \[0,1] based on:

* The quality of the report
* The quality of the guide
* The amount of nodes that connected to the server

### Catastrophic Errors

#### Permanent Data Object Loss

A confirmed data object can no longer be recovered from storage nodes, despite not being deleted on chain.

#### Incorrect Reporting

Whereas a failure to provide the storage specific report, or omission of certain values will simply cause a bad score, incorrect data will, if discovered, count as a catastrophic error.



### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
