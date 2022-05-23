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
DISTRIBUTOR_SCORE = [2*GENERAL_WG_SCORE + REPORT_SCORE + THUMBNAIL_SCORE + RESEARCH_SCORE]/(5*2^{N})

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



### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
