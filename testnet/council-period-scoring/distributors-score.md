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
DISTRIBUTOR_SCORE = [GENERAL_WG_SCORE + REPORT_SCORE + THUMBNAIL_SCORE + PLAYABLITIY_SCORE + SERVICE_SCORE]/(5^{N})
```

### `GENERAL_WG_SCORE`

Is computed with the metrics defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-period-plan](general-working-group-score.md#working-group-period-plan "mention"), the working group report must include a section covering

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

Whereas the same deadline as general report applies, there is no requirement to submit a temporary report for this.

### `THUMBNAIL_SCORE`

_Objective:_ `Get a "clean" landing page on play.joystream.org`

#### Notes

* Unless all thumbnails are cached on the server side, a new user scrolling through the player will have a bad experiences.
* It's not clear to us how to best achieve this. It will likely playing around with both node and system configs

#### Scoring Calculations

Let:

* `avg_rendering_time_i` be the average time \[ms] it takes to GET all thumbnails (on screen) when opening [the player](play.joystream.org) (and optionally scrolling), for a test run `i`
* `max_rendering_time_i` be the longest time \[ms] it takes to render a thumbnail when opening [the player](play.joystream.org), (and optionally scrolling), for a test run `i`
* `THUMBNAIL_SCORE` be the final score \[0,1]

Then:

```
  avg_rendering = Zigma[max((2000-avg_rendering_time_i)/1000,1)]/i
  max_rendering_score = max((3000-avg_rendering_time_i/1000),1)

  # finally
  THUMBNAIL_SCORE = 0.6*avg_rendering + 0.4*max_rendering_score
```

### `PLAYABLITIY_SCORE`

_Objective:_ `All content should be playable from at least 3 sources`

#### Notes

* At any point in time, at least 3 operated buckers should have each bag
* Note that having configured that to be the case is only some fraction of the job. Unless the content can be fetched from that/those sources, it doesn't do much good!

#### Scoring Calculations

Let:

* `avg_configured_sources_i` be the average number of buckets (where `distributing=true`), that holds each bag, for a spot check `i`
* `min_configured_sources_i` be the lowest number of buckets (where `distributing=true`), that holds a bag, for a spot check `i`
* `unavailable_distributors_i` be the amount of operated buckets (where `distributing=true`), that should have a dataObject that, for whatever reason, can't be fetched
* `PLAYABLITIY_SCORE` be the final score \[0,1]

Then:

```
  avg_configured_sources_score = Zigma[max(avg_configured_sources_i-2.5,1)]/i
  min_configured_sources_score = Zigma[max(min_configured_sources-2,1)]/i
  unavailable_distributors_score = Zigma[max(1-unavailable_distributors_i,1)]/i

  # finally
  PLAYABLITIY_SCORE = 0.3*(avg_configured_sources_score + min_configured_sources_score) + 0.4*unavailable_distributors_score
```

### `SERVICE_SCORE`

_Objective:_ `Download and playback quality`

#### Notes

* Measurements will be done by spotchecks from Europe.
* Latency caused ping will be removed from the equation (we'll ping the server and deduct)

#### Scoring Calculations

Let:

* `avg_download_ratio_i` be the average playtime \[s] divided by download time \[s] (for a sample of videos), assuming some random checks (indexed `i`) are performed during the period
* `min_download_ratio_i` be the lowest playtime \[s] divided by download time \[s] (for a sample of videos), assuming some random checks (indexed `i`) are performed during the period
* `avg_buffering_i` be the average time \[s] of buffering, when playing a video and skipping ahead, assuming some random checks (indexed `i`) are performed during the period
* `max_buffering_i` be the highest time \[s] of buffering, when playing a video and skipping ahead, assuming some random checks (indexed `i`) are performed during the period
* `SERVICE_SCORE` be the final score \[0,1]

Then:

```
  avg_download_ratio_score = Zigma[max(avg_download_ratio_i-1,1)]/i
  min_download_ratio_score = Zigma[max(min_download_ratio_i-0.5,1)]/i
  avg_buffering_score = Zigma[max((5-avg_buffering_i)/3,1)]/i
  max_buffering_score = Zigma[max((10-max_buffering_i)/6,1)]/i

  # finally
  service_score = 0.25*(avg_download_ratio_score + min_download_ratio_i + avg_buffering_i + max_buffering_i)
```

### Catastrophic Errors

#### **No available sources to fetch a data object from**

A data object is not available from any distributor, despite being held be an available storage node
