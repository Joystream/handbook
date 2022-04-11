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
STORAGE_SCORE = [GENERAL_WG_SCORE + MAINTENANCE_SCORE + UPLOAD_SCORE]/(3^{N})
```

where

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

Whereas the same deadline as general report applies, there is no requirement to submit a temporary report for this.

### `MAINTENANCE_SCORE`

_Objective:_ `Maintain excess capacity, with a replication_rate of at least 4`

#### Notes

* This means we want all new objects to be, by default, without manual intervention, to be stored by multiple nodes.
* "Operating/operated" means that a bucket is assigned to a Worker, the worker is running a node that can be uploaded to (by a channel owner) and downloaded from (by a distributor)
* Having configured the `dynamic_bag_policy` policy is only the first step! Example:
  * dynamic bag policy is 3 and buckets 0-6 can all accept a new bags
    * if bucket 0 is "full" (meaning max objects or size is reached), or down, that means the system CAN in fact halt, despite 1-5 all working.

#### Scoring Calculations

Let:

* `dynamic_configuration_i` be the maximum amount of operated storage buckets, that with the current configuration, in a worst case scenario, can accept and store new bags, assuming some random checks (indexed `i`) are made
* `existing_bag_configuration_i` be the maximum amount of operated storage buckets, that with the current configuration, in a "worst case scenario" will accept new data objects to an existing bag, assuming some random checks (indexed `i`) are made
* `excess_capacity_objects_true/false_i` and `excess_capacity_size_true/false_i` be the extra capacity for objects and size \[GB] the system has, to accept new data objects, whether the bucket accepts new bags or only additions to existing bags, assuming some random checks (indexed `i`) are made
* `MAINTENANCE_SCORE` be the final score \[0,1]

Then:

```
  dynamic_configuration_score = Zigma[max(dynamic_configuration_i-3,1)]/i
  existing_bag_configuration_score = Zigma[max(existing_bag_configuration_i-3,1)]/i
  excess_capacity_objects_false_score = Zigma[max((excess_capacity_objects_i-75)/75,1)]/i
  excess_capacity_size_false_score = Zigma[max((excess_capacity_size_i-10)/20,1)]/i
  excess_capacity_objects_true_score = Zigma[max((excess_capacity_objects_i-200)/200,1)]/i
  excess_capacity_size_true_score = Zigma[max((excess_capacity_size_i-30)/20,1)]/i

  # finally
  MAINTENANCE_SCORE = 0.25*(dynamic_configuration_score + existing_bag_configuration_score + excess_capacity_objects_score + excess_capacity_size_score)
```

### `UPLOAD_SCORE`

_Objective:_ `Keep failed uploads under 2%`

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
  UPLOAD_SCORE = (successful_uploads/total_uploads - 0.96)/0.04
```

### Catastrophic Errors

#### Permanent Data Object Loss

A confirmed data object can no longer be recovered from storage nodes, despite not being deleted on chain.

#### Incorrect Reporting

Whereas a failure to provide the storage specific report, or omission of certain values will simply cause a bad score, incorrect data will, if discovered, count as a catastrophic error.



### Need help understanding something?

### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
