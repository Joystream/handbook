---
description: >-
  An on-chain index of all data stored and distributed in the system, with
  associated information about ownership and what providers are tasked with
  storing and providing bandwidth.
---

# Data Directory

## Introduction

This subsystem serves to retain an index of all static assets, including who owns them, and information about what actors are currently tasked with storing and distributing them to end users. It has no awareness of the underlying content or purpose represented by such an object, as it is used by different parts of the system. It can represent assets as diverse as

* Video media, with a particular resolution and encoding, living in the content directory.
* Image media used for the avatar of a member, an election candidate or for the cover of a channel in the content directory.
* A data attachment to a blog post, proposal or role application.

In the future it will be extended with autonomous interactive auditing features for storage providers and payments between service providers to incentive replication.

## Concepts

### Data Directory Account

The _data directory account_ is a module account for holding funds in the data directory, and it has an account id denoted by `DATA_DIRECTORY_ACCOUNT_ID`.

### Data Object

A _data object_ represents a single static data asset, like an image or video media, and it is defined by the following information

* `id`: A unique immutable non-negative integer identifying an individual data object, is automatically assigned by the blockchain upon creation.
* `accepted`: Whether the object has been verified as correctly uploaded to an initial storage providers. The storage provider making such a confirmation for a given object is referred to as the _liasion_ for the object.
* `deletion_prize`: An amount of funds locked up as a state bloat bond for the object.
* `size`: The claimed size of the object, as stipulated during creation by the owner, and implicitly understood to be verified by the liasion.
* `hash`: The IPFS CID of the object, specifically SS58 format of Multihash with blake3 hashing algorithm.

### Bag Id

A _Bag Id_ is a value which can identify a specific bag, see section on [#bag](data-directory.md#bag "mention") for further elaboration, and it takes one of the following varieties

* `static`: a _static bag id_ identifies one of the built in bags in the system, and it comes in one of the following subvarieties
  * `council`: identifies the bag reserved for the council to manage through its proposal system.
  * `membership`: identifies the bag for the membership working group.
  * `storage`: identifies the bag for the storage working group.
  * `bandwidth`: identifies the bag for the bandwidth working group.
  * `content`: identifies the bag for the content directory working group.
  * `forum`: identifies the bag for the forum working group
  * `operations_alpha`, `operations_beta` ...: each identifies the bag for the corresponding operations working group.
* `dynamic`: a _dynamic bag id_ identifies one of the dynamic, so not built in, bags in the system, and it comes in one of the following subvarieties:
  * `member`: has associated membership id and identifies bag for this member.
  * `channel`: has associated channel id, and identifies the bag for this channel.

### Bag

A _data object bag_, or _bag_ for short, is a dynamic collection of data objects which can be treated as one subject in the system. Each bag has an owner, which is established when the bag is created. A data object lives in exactly one bag, but may be moved across bags by the owner of the bag. Only the owner can create new data objects in a bag, or opt into absorbing objects from another bag. The purpose of the concept of bags is to limit the on-chain transactional footprint of administrating multiple objects which should be treated the same way. This is achieved by establishing a small immutable identifier for these objects. The canonical example would be assets that will be consumed together, such as the cover photo and different video media encodings of a single piece of video content. Storage and distribution nodes have commitments to bags, not individual data objects.

A bag is defined by the following information

* `id` : an id of type [#bag-id](data-directory.md#bag-id "mention") for this bag.
* `stored_by`: set of ids for [#storage-bucket](data-directory.md#storage-bucket "mention") tasked with storing the objects in the bag.
* `distributed_by`: set of ids for [#distributor-bucket](data-directory.md#distributor-bucket "mention") tasked with distributing the objects in the bag.
* `deletion_prize`: amount of money placed in [#undefined](data-directory.md#undefined "mention") as staking bond for cleaning up unused bag.
* `object_size`: cumulative size of all data objects in the bag.
* `object_count`: cumulative number of objects in the bag.

### Storage Bucket

A _storage bucket_ represents a commitment to hold some set of bags for long term storage. A bucket may have a _bucket operator_, which is a single worker in the storage working group. There is distinct _bucket operator metadata_ associated with each, which describes things such as how to resolve the host. The operator of a bucket may change over time. As previously described, when new dynamic bags are created, they are allocated to one or more such buckets, unless the bucket has been temporarily disabled from accepting new bags.

* `id` **:** a unique immutable non-negative integer identifying an individual storage bucket, is automatically assigned by the blockchain upon creation.
* `operator_status`**:** status of bucket operator, is one of the following varieties
  * `missing`: when there is no operator.
  * `invited`: with associated [broken-reference](broken-reference/ "mention") id in storage working group, when the lead has invited the given worker to operate the bucket.
* `accepting_new_bags`: whether this this bucket is an acceptable destination for additional bags.
* `total_size_limit`: upper bound on cumulative size of all data objects in bucket.
* `object_count_limit`: upper bound on cumulative number of all data objects in bucket.
* `total_size`: cumulative size of all data objects in bucket.
* `object_count`: cumulative number of all data objects in bucket.

### Distribution Bucket

A _distribution bucket_ represents a commitment to distribute a set of bags to end users. A bucket may have multiple _bucket operators_, each being a worker in the distribution working group. The same metadata concept applies here as well, and additionally covers whether the operator is live or not. Bags are assigned to buckets when being uploaded, or later by the lead by manual intervention.

* `id` : a unique immutable non-negative integer identifying an individual distributor bucket, is automatically assigned by the blockchain upon creation.
* `accepting_new_bags` : whether this bucket is an acceptable destination for additional bags.
* `distributing`: whether assigned operators are servicing this bucket at the moment.
* `pending_invitations`: set [broken-reference](broken-reference/ "mention") ids from bandwidth working group for workers who have been invited and can join as operators.
* `operators`: set [broken-reference](broken-reference/ "mention") ids from bandwidth working group for workers currently acting as operators.
* `assigned_bags`: the number of bags currently assigned to this bucket.

### Distribution Bucket Family

Buckets are partitioned into so called _distribution bucket families_. These families group buckets with interchangeable semantics from distributional point of view, and the purpose of the grouping is to allow sharding over the bag space for a given service level when creating new bags. Here is an example that can make this more clear. A subset of families could for example represent each country in East Asia, where each family corresponds to a specific country. The buckets in a family, say the family for Mongolia, will be operated by infrastructure which can provide sufficiently low latency guarantees w.r.t. the corresponding country. The bag for a channel known to be particularly popular in this area could be setup so as to use these buckets disproportionately.

* `id`: a unique immutable non-negative integer identifying an individual distribution bucket family, is automatically assigned by the blockchain upon creation.
* `distribution_buckets`: a map which sends [#distribution-bucket](data-directory.md#distribution-bucket "mention") `id` to the corresponding bucket, and holds all buckets that are part of this family.

### Dynamic Bag Creation Policy

A _dynamic bag creation policy_ holds parameter values impacting how exactly the creation of a new dynamic bag occurs, and there is one such policy for each type of dynamic bag, so two, one for `member` and one for `channel`. It describes how many storage buckets should store the bag, and from what subset of distribution bucket families (described below) to select a given number of distribution buckets, specifically

* `number_of_storage_buckets`: number of storage buckets which should replicate the new bag.
* `families`: map of [#distribution-bucket-family](data-directory.md#distribution-bucket-family "mention") id to the number of distribution buckets in the given family one must assign to a new bag for distribution when subject to this policy.

### Blacklist

The _blacklist_ is a collection hashes, managed by the lead, which are not allowed for future introductions of data objects in the directory.

## Figures

### Overview

The following overview summarizes the main relationships between the primary concepts.

![Entity Diagram](../../.gitbook/assets/storage\_and\_distribution.png)

## Parameters

The following mutable parameters are part of the system.

| Name                            | Type      | Description                                 |
| ------------------------------- | --------- | ------------------------------------------- |
| `uploading_blocked`             | `Bool`    | Whether all new uploads blocked.            |
| `data_object_per_mega_byte_fee` | `Balance` | Size based pricing of new objects uploaded. |

## Internal Methods

The following set of method can be invoked from within the blockchain itself by other systems, and it is the way that different subsystems unlock the ability to have end-users interact with the storage and bandwidth system, for example allowing channel owners to publish video media into this infrastructure.

### can\_upload\_data\_objects

Validates upload parameters and conditions (like global uploading block). Validates voucher usage for affected buckets.

### upload\_data\_objects

Upload new data objects.

### can\_move\_data\_objects

Validates moving objects parameters, voucher usage for affected buckets.

### move\_data\_objects

Move data objects to a new bag.

### can\_delete\_data\_objects

Validates `delete_data_objects` parameters, voucher usage for affected buckets.

### delete\_data\_objects

Delete storage objects. Transfer deletion prize to the provided account.

### delete\_dynamic\_bag

Delete dynamic bag. Updates related storage bucket vouchers.

### can\_delete\_dynamic\_bag

Validates `delete_dynamic_bag` parameters and conditions.

### create\_dynamic\_bag

Creates dynamic bag. BagId should provide the caller.

### can\_create\_dynamic\_bag

Validates `create_dynamic_bag` parameters and conditions.

### ensure\_bag\_exists

Checks if a bag does exists and returns it. Static Always exists

### get\_data\_objects\_id

Get all objects id in a bag, without checking its existence

## Constants

| Name                                                 | Description                                                                   |
| ---------------------------------------------------- | ----------------------------------------------------------------------------- |
| `DataObjectDeletionPrize`                            | A prize for a data object deletion.                                           |
| `BlacklistSizeLimit`                                 | maximum size of the "hash blacklist" collection.                              |
| `DATA_DIRECTORY_ACCOUNT_ID`                          | A prize for a data object .                                                   |
| `StorageBucketsPerBagValueConstraint`                | "Storage buckets per bag" value constraint.                                   |
| `DistributionBucketsPerBagValueConstraint`           | "Distribution buckets per bag" value constraint.                              |
| `DefaultMemberDynamicBagNumberOfStorageBuckets`      | The default dynamic bag creation policy for members (storage bucket number).  |
| `DefaultChannelDynamicBagNumberOfStorageBuckets`     | The default dynamic bag creation policy for channels (storage bucket number). |
| `MaxRandomIterationNumber`                           | Max random iteration number (eg.: when picking the storage buckets).          |
| `MaxDistributionBucketFamilyNumber`                  | Max allowed distribution bucket family number.                                |
| `MaxDistributionBucketNumberPerFamily`               | Max allowed distribution bucket number per family.                            |
| `MaxNumberOfPendingInvitationsPerDistributionBucket` | Max number of pending invitations per distribution bucket.                    |
| `MaxDataObjectSize`                                  | Max data object size in bytes.                                                |

## Extrinsics

### create\_storage\_bucket

WIP.

### update\_storage\_buckets\_for\_bag

WIP.

### delete\_storage\_bucket

WIP.

### invite\_storage\_bucket\_operator

WIP.

### cancel\_storage\_bucket\_operator\_invite

WIP.

### remove\_storage\_bucket\_operator

WIP.

### update\_uploading\_blocked\_status

WIP.

### update\_storage\_buckets\_per\_bag\_limit

WIP.

### update\_storage\_buckets\_voucher\_max\_limits

WIP.

### update\_number\_of\_storage\_buckets\_in\_dynamic\_bag\_creation\_policy

WIP.

### update\_blacklist

WIP.

### set\_storage\_bucket\_voucher\_limits

WIP.

### accept\_storage\_bucket\_invitation

WIP.

### set\_storage\_operator\_metadata

WIP.

### accept\_pending\_data\_objects

WIP.

### create\_distribution\_bucket\_family

WIP.

### delete\_distribution\_bucket\_family

WIP.

### create\_distribution\_bucket

WIP.

### delete\_distribution\_bucket

WIP.

### update\_distribution\_bucket\_status

WIP.

### update\_distribution\_buckets\_for\_bag

WIP.

### distribution\_buckets\_per\_bag\_limit

WIP.

### update\_families\_in\_dynamic\_bag\_creation\_policy

WIP.

### cancel\_distribution\_bucket\_operator\_invite

WIP.

### remove\_distribution\_bucket\_operator

WIP.

### set\_distribution\_bucket\_family\_metadata

WIP.

### accept\_distribution\_bucket\_invitation

WIP.

### set\_distribution\_operator\_metadata

WIP.
