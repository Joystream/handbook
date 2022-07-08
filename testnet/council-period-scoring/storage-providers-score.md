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
STORAGE_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + 2*SYSTEM_SCORE + UPLOAD_SCORE + COST_SCORE]/(7*2^{N})
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
* An overview of which nodes that running with `--elasticSearchEndpoint`, what log level they are using, and how this information is used.

The report should be posted in the forum category `Working Groups >[Working Group Name]` where `[Working Group Name]`is the name of the working group, as a thread which has the `Report for [council period ID]`. As these reports should have lots of tables, links and difficult formatting, some key statistics with link to a page on notion is acceptable.

### `SYSTEM_SCORE`

Many things are required for the storage system to function as intended.  It needs

* to be **robust** enough to survive 2-3 nodes going down at the same time
* **redundancy** in case of a burst of new uploads, some nodes going down, or a datacenter crashes
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

* The minimum replication rate is 4 (`replication_score`)
  * Meaning **all** objects must be stored by at least 4 operated buckets at the end of the term
* If any four storage nodes goes down at the same time, every object must still be available from at least two storage nodes (`redundancy_score`)
* If any four storage nodes goes down at the same time, every channel must still be able to upload to at least two storage nodes (`emergency_score)`
* All storage nodes are on the latest version of `colossus` (`version_score`)
* All storage that has been in the working group for more than 1 week (100,800 blocks), must maintain their own query node, and share the public url in the metadata (`autonomy_score`)
  * Will not be measured before scoring period 16
* All storage nodes displays their location coordinates, node storage capacity and caching in the metadata,  (`transparancy_score`)
* No storage node stores more than 80% of their capacity (`excess_capacity_score`)
  * This may severely reduce performance
* The maximum response time is 2h (`response_score)`

The first three subscores are measured at some point during the last 14400 blocks.

The latter will be measured by creating an opening for `@bwhm` without any rewards, that should be invited to a bucket, but not set to accept new bags, and only (manually) assigned a single existing "testing" bag. If the node goes down, the bag must be removed.

#### Scoring Calculations

Then:

```
 All subscores are graded binary

SYSTEM_SCORE = 0.125*(replication_score + redundancy_score + emergency_score + version_score + autonomy_score + transparancy_score + excess_capacity_score + response_score)
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
  UPLOAD_SCORE = (successful_uploads/total_uploads - 0.95)/0.05
```

### `COST_SCORE`

The cost score will try to measure how the group allocates their resources. Although being cost efficient is not a top priority for a testnet in general, it doesn't make much sense to:

* Employ a lot of operators that are not receiving or storing content
* Have operators store significantly less content than their capacity
* Have operators run with costly hardware, and/or in expensive datacenters unless the benefit outweighs the extra costs

he score is the sum of two subscores:

1. A report documenting
   * Current costs
   * What can be done to reduce them (without impacting other scores)
   * What could be done to reduce them (may impact other scores), and why this may, or may not, be worth it
2. A subjective analysis by Jsgenesis, based on the report above and chain data. Any "excessive" costs not covered in the report will reduce the score, whereas costs that are documented will not.  An exeption to this rule is if a "cut" is not enacted in subsequent council periods.&#x20;

Jsgenesis will assign a score in the range \[0,1] based on this.

### Catastrophic Errors

#### Permanent Data Object Loss

A confirmed data object can no longer be recovered from storage nodes, despite not being deleted on chain.

#### Incorrect Reporting

Whereas a failure to provide the storage specific report, or omission of certain values will simply cause a bad score, incorrect data will, if discovered, count as a catastrophic error.



### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
