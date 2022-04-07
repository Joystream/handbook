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
```
DISTRIBUTOR_SCORE = 0.2*GENERAL_WG_SCORE 0.35*THUMBNAIL_SCORE + 0.1*PLAYABLITIY_SCORE + 0.3*SERVICE_SCORE + 0.15*GUIDE_SCORE
```

### `GENERAL_WG_SCORE`
Is computed with the metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`0%`**.

### `THUMBNAIL_SCORE`
*Objective:* `Get a "clean" landing page on play.joystream.org`

#### Notes
- Unless all thumbnails are cached on the server side, a new user scrolling through the player will have a bad experiences.
- It's not clear to us how to best achieve this. It will likely playing around with both node and system configs

#### Scoring Calculations
Let:
- `blockheight_start` be block #100400 (12h after officially publishing the incentives)
- `blockheight_end` be block #151200 (12h after the end of the Term, so the new Council has time to react)
- `avg_rendering_time_i` be the average time [ms] it takes to GET all thumbnails (on screen) when opening [the player](play.joystream.org) (and optionally scrolling), for a test run `i`
- `max_rendering_time_i` be the longest time [ms] it takes to render a thumbnail when opening [the player](play.joystream.org), (and optionally scrolling), for a test run `i`
- `THUMBNAIL_SCORE` be the final score [0,1]

Then:
```
  avg_rendering = Zigma[max((1500-avg_rendering_time_i)/1000,1)]/i
  max_rendering_score = max((2500-avg_rendering_time_i/1000),1)

  # finally
  THUMBNAIL_SCORE = 0.6*avg_rendering + 0.4*max_rendering_score
```

### `PLAYABLITIY_SCORE`
*Objective:* `All content should be playable from at least 3 sources`

#### Notes
- At any point in time, at least 3 operated buckers should have each bag
- Note that having configured that to be the case is only some fraction of the job. Unless the content can be fetched from that/those sources, it doesn't do much good!

#### Scoring Calculations
Let:
- `avg_configured_sources_i` be the average number of buckets (where `distributing=true`), that holds each bag, for a spot check `i`
- `min_configured_sources_i` be the lowest number of buckets (where `distributing=true`), that holds a bag, for a spot check `i`
- `unavailable_distributors_i` be the amount of operated buckets (where `distributing=true`), that should have a dataObject that, for whatever reason, can't be fetched
- `PLAYABLITIY_SCORE` be the final score [0,1]

Then:
```
  avg_configured_sources_score = Zigma[max(avg_configured_sources_i-2.5,1)]/i
  min_configured_sources_score = Zigma[max(min_configured_sources-2,1)]/i
  unavailable_distributors_score = Zigma[max(1-unavailable_distributors_i,1)]/i

  # finally
  PLAYABLITIY_SCORE = 0.3*(avg_configured_sources_score + min_configured_sources_score) + 0.4*unavailable_distributors_score
```


### `SERVICE_SCORE`
*Objective:* `Download and playback quality`

#### Notes
- Measurements will be done by spotchecks from Europe.
- Latency caused ping will be removed from the equation (we'll ping the server and deduct)

#### Scoring Calculations
Let:
- `blockheight_start` be block #100400 (12h after officially publishing the incentives)
- `blockheight_end` be block #151200 (12h after the end of the Term, so the new Council has time to react)
- `avg_download_ratio_i` be the average playtime [s] divided by download time [s] (for a sample of videos), assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `min_download_ratio_i` be the lowest playtime [s] divided by download time [s] (for a sample of videos), assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `avg_buffering_i` be the average time [s] of buffering, when playing a video and skipping ahead, assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `max_buffering_i` be the highest time [s] of buffering, when playing a video and skipping ahead, assuming some random checks (indexed `i`) are done between `blockheight_start` and the `blockheight_end`
- `SERVICE_SCORE` be the final score [0,1]

Then:
```
  avg_download_ratio_score = Zigma[max(avg_download_ratio_i-1,1)]/i
  min_download_ratio_score = Zigma[max(min_download_ratio_i-0.5,1)]/i
  avg_buffering_score = Zigma[max((5-avg_buffering_i)/3,1)]/i
  max_buffering_score = Zigma[max((10-max_buffering_i)/6,1)]/i

  # finally
  service_score = 0.25*(avg_download_ratio_score + min_download_ratio_i + avg_buffering_i + max_buffering_i)
```


### `GUIDE_SCORE`
*Objective:* `Update, improve and migrate the howto guide to match Olympia`

#### Notes
Until now, the Joystream "howto" guides in general, aDistributors are no exception, has been available in the helpdesk. We are moving away from this, and want them to hosted in the groups [notion space](https://joystream.notion.site/Distribution-1f4cfbbb2e934c79bf20b8db7f019d32).
The existing ones will also need some updates, to stay current. Unlike the other SoW, this will be graded subjectively.

#### Instructions
- Create a user friendly "landing page", that explains:
  - the purpose of the role
  - the tools required
  - how to apply for the role
  - other relevant information and links
- Add the technical instructions required for starting out as a distributors
  - we have imported the current and outdated [helpdesk README.md](https://github.com/Joystream/helpdesk/tree/master/roles/distributors#readme), but that will of course have a lot of broken links and incorrect information

#### Scoring Calculations
The `GUIDE_SCORE` is graded subjectively.
