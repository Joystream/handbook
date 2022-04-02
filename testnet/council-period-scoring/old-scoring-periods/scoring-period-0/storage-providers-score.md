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

## Report

The working group report should include a special section with information about

* What data objects were permanently lost.
* How many bags were created.
* How many bags were deleted.
* How many data objects were uploaded, and
  * what was their total size,
  * what was the size distribution.
* Distribution of bag sizes in terms of data object counts.
* Distribution of bag sizes in terms of total data object size.
* List of failed data upload upload attempts on chain which failed due to storage bucket size being too low.
* Total capacity of all storage bucket limits.
* Total used capacity of all storage buckets.

## Score

The score is computed as follows

```
STORAGE_SCORE = 0.1*GENERAL_WG_SCORE + 0.25*REPLICATION_SCORE + 0.3*MAINTENANCE_SCORE + 0.20*UPLOAD_SCORE + 0.15*GUIDE_SCORE
```

where

### `GENERAL_WG_SCORE`
Is computed with the metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`0%`**.


### `REPLICATION_SCORE`
*Objective:* `Ensure content directory integrity through redundancy`

#### Notes
If all `bags` are stored by a single node only (or in one data center/VPS provider only) the system may crash entirely.

"Operating/operated" means that a bucket is assigned to a Worker, the worker is running a node that can be uploaded to (by a channel owner) and downloaded from (by a distributor)

#### Scoring Calculations
Let:
- `replication_rate` be the number of operated buckets currently holding a bag
  - `min_replication_rate` be be the lowest `replication_rate` of any (accepted) object at that moment
  - `avg_replication_rate` be be the average `replication_rate` of any (accepted) object at that moment
- `blockheight` be a target blockheight
- `*_@#<blockheight>`
- `REPLICATION_SCORE` be the final score [0,1]

Then:
```
  replication_score_@#100400 = 0.5*[max(min_replication_rate-2,1)+max(avg_replication_rate-2.5,1)]
  replication_score_@#151200 = max(min_replication_rate-3,1)

  # finally
  REPLICATION_SCORE = 0.5*(replication_score_@#100400 + replication_score_@#151200)
```

### `MAINTENANCE_SCORE`
*Objective:* `Maintain excess capacity, with a replication_rate of at least 4`

#### Notes
- This means we want all new objects to be, by default, without manual intervention, to be stored by multiple nodes.
- "Operating/operated" means that a bucket is assigned to a Worker, the worker is running a node that can be uploaded to (by a channel owner) and downloaded from (by a distributor)
- Having configured the `dynamic_bag_policy` policy is only the first step! Example:
  - dynamic bag policy is 3 and buckets 0-6 can all accept a new bags
    - if bucket 0 is "full" (meaning max objects or size is reached), or down, that means the system CAN in fact halt, despite 1-5 all working.

#### Scoring Calculations
Let:
- `blockheight_start` be block #100400 (12h after officially publishing the incentives)
- `blockheight_end` be block #151200 (12h after the end of the Term, so the new Council has time to react)
- `dynamic_configuration_i` be the maximum amount of operated storage buckets, that with the current configuration, in a worst case scenario, can accept and store new bags, assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `existing_bag_configuration_i` be the maximum amount of operated storage buckets, that with the current configuration, in a "worst case scenario" will accept new dataObjects to an existing bag, assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `excess_capacity_objects_true/false_i` and `excess_capacity_size_true/false_i` be the extra capacity for objects and size [GB] the system has, to accept new dataObjects, whether the bucket accepts new bags or only additions to existing bags, assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `MAINTENANCE_SCORE` be the final score [0,1]

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
*Objective:* `Keep failed uploads under 2%`

#### Notes
- In general, dataObjects added that was not part of the migration, where `isAccepted=false` means a failed upload. However, to keep it "fair":
  - if it can be "proven" that the error was caused by Jsgenesis, or the uploader, it isn't counted. The burden of proof is on the Storage Lead/Worker/Council
  - neither are multiple instances of the same failure (say, a user tries again, and the same bucket/storage-node fails), that occurs within an hour of the first error
    - after that, we assume the operator will resolve the problem, the bag will be moved, or the issue is fixed in some other way

#### Scoring Calculations
Let:
- `successful_uploads` be any new dataObject added (that counts) where `isAccepted=true`
- `counting_uploads` be any new dataObject added, (that counts)
- `UPLOAD_SCORE` be the final score [-1,1]

Then:
```
  UPLOAD_SCORE = (successful_uploads/total_uploads - 0.96)/0.04
```


### `GUIDE_SCORE`
*Objective:* `Update, improve and migrate the howto guide to match Olympia`

#### Notes
Until now, the Joystream "howto" guides in general, and Storage Providers are no exception, has been available in the helpdesk. We are moving away from this, and want them to hosted in the groups [notion space](https://joystream.notion.site/Storage-9dc5a16444934dc4bda08b596bc15375).
The existing ones will also need some updates, to stay current. Unlike the other SoW, this will be graded subjectively.

#### Instructions
- Create a user friendly "landing page", that explains:
  - the purpose of the role
  - the tools required
  - how to apply for the role
  - other relevant information and links
- Add the technical instructions required for starting out as a storage provides
  - we have imported the current and outdated [helpdesk README.md](https://github.com/Joystream/helpdesk/blob/master/roles/storage-providers/README.md), but that will of course have a lot of broken links and incorrect information

#### Scoring Calculations
The `GUIDE_SCORE` is graded subjectively.
