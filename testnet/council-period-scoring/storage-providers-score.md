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
STORAGE_SCORE = [DISTRIBUTOR_SCORE = [3*OPERATIONAL_SCORE + LOG_SCORE + DEPLOYMENT_GUIDE_SCORE]/(5*2^{N})]/(7*2^{N})
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `OPERATIONAL_SCORE`

Get the system operational as soon as possible, meaning:

* Sufficient buckets (as required by the runtime) operational
* System and bucket level configurations are "good"
* Non-operational buckets are turned off, to avoid failed requests
* Bags quickly "moved" as new buckets are online, and others fail

### `LOG_SCORE`

Each transaction `tx:n` performed by the Lead role key, successful or not, must be logged.

* This is not about the Council or JSG catching mistakes, but ensuring that the deployment is reproducible for mainnet (if/when successful)
* Helpful for reviewing improvements, and lessons learned

### `DEPLOYMENT_GUIDE_SCORE`

With the above in hand, the Lead, the Council, the community and JSG can try to improve the process for later. Includes

* The Goal, as in a somewhat stable system with a specific setup of buckets and operators etc.
* Step by step process, as in the log above except:
  * "incorrect" transactions are removed
  * more emphasis on why
  * other options, if you wanted to achieve goal `x` instead of `y`
* Troubleshooting, as in how to avoid `x` and recover from `y`

### Catastrophic Errors

#### Permanent Data Object Loss

A confirmed data object can no longer be recovered from storage nodes, despite not being deleted on chain.

#### Incorrect Reporting

Whereas a failure to provide the storage specific report, or omission of certain values will simply cause a bad score, incorrect data will, if discovered, count as a catastrophic error.



### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
