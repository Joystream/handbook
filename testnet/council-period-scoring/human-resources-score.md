---
description: Metrics used to compute score for HR working group.
---

# Human Resources Score

## Overview

The HR working group activities relevant to scoring fall into the following five categories

* **Greeting:** Engage with every new person entering the official [Official Discord](https://discord.com/invite/DE9UN3YpRP).
* **Onboarding:** Get new persons setup with a first membership and added to the [#crm](human-resources-score.md#crm "mention").
* **Catalyzing:** Get persons started with a concrete activity, such as creating a bounty, working on an existing bounty or applying for a role.
* **Nurture:** To engage and re-engage existing persons in the CRM who are not yet founding members, to encourage them to continue, help them get answers to questions, and gather insights about their experience to support the overall success of the founding member program.
* **Bounty management:** Get new, and existing, people to work on small one off tasks as a way to get into more permanent and long running roles in the system.

## Greeting

New people will continuously be arriving in the Discord, both directly, and through a website chat widget installed on the Joystream website.

`<add picture of Widgetbot on site>`

All new persons should be&#x20;

* greeted by a member in the HR working group in the `#welcome` or `#general` channels,&#x20;
* offered assistance in solving CAPTCHAs if needed,

## Onboarding

As soon as possible after being greeted, the objective of the HR worker is to do the following in the given order

1. Capture the person in the CRM, so that they can be catalyzed later and the project captures relevant up to date information about who is arriving, and from where,
2. Get the person to create a membership on-chain, with accurate referral information and metadata, and also some initial $tJOY to get started using the chain,
3. Get the person into a specific activity, aligned with their skills and interests, and with the needs of the network, allowing them to earn $tJOY and $JOY. This is first achieved by developing an understanding of the person in terms of skills and interests, and the filtering the set of near term opportunities through this profile. The major opportunities are
   1. Starting to work on an existing bounty.
   2. Getting a role in a working group where there is soon space for newcomers.
   3. Running as a candidate for the council.
   4. Creating a new bounty specifically based on this persons skills and interests.

This onboarding should always be initiated right after the initial greeting stage, however, it may also be attempted as part of a catalyzing effort for a dormant person who never graduated into a substantive activity. The outcome of an attempt should be recorded in the CRM.

## Catalyzing

Invariably, people will drop off at various level of progression before becoming founding members. Some may never even get started beyond setting up a membership. This could be for a variety of reasons. Since we are recording all interactions, we have visibility into the history of correspondences between the HR group and a given person, and we can see the history of activities they have been involved in. This allows the HR group to check in with people as they stall and _catalyze_ them to continue their journey, as well as capture valuable information about why they stalled.

## Bounty Management

_**Note: This management requires the presence of the bounty system on-chain, presumably launched with Olympia.**_

### Creation

As mentioned prior, [bounties.md](../../system/bounties.md "mention") are an excellent low barrier to entry means of allowing total newcomers to participate, start earning $tJOY and $JOY, and learning the system and community. Bounties are created on-chain using either

* Pre-prepared bounties living in the `BountyTemplate` table of the CRM. Bounties are added here by
  * the HR lead
  * Jsgenesis staff
* Input from a user about doing a project which does not exist.

The funding from the bounties always come from the HR working group workers, who should be provided small $tJOY cash funds from the lead, allowing them to create new bounties on an ongoing basis for new people showing up continuously in the community. It is the responsibility of the lead to responsibly manage how much each worker is entrusted with over any given period of time. A bounty created on-chain _must_ reference the relevant `BountyTemplate` instance in the CRM, by ID, which is why those instances can never be deleted, and they _must_ respect the $tJOY budget limit specified in the template. If this limit is found to be too low, only the lead or Jsgenesis can update the budget. The worker creating the on-chain bounty must make sure to select the appropriate oracle, which is most likely the HR worker with most experience in the relevant area of the platform. Lastly, the worker must negotiate a plausible working period duration for the bounty.\
\
<mark style="color:red;">**`Be aware that Jsgenesis staff will be conducting probing experiments to see how funds are allocated to bounties under false identities.`**</mark>

### **Management**

It is the responsibility of each worker acting as the oracle for a bounty to check up on progress and log this using the on-chain discussion system. If the contributor is getting stuck or delayed, this must be logged publicly, and the oracle should help to push the contributor forward, but also establish clear forward looking expectations about the possibility that the bounty will be cancelled without the contributor getting anything, if sufficient progress is not made.&#x20;

### Resolution

At some point, the oracle must decide the outcome of the bounty during the judgment period. This really boils down to determining how much, if any, part of the initial $tJOY bounty budget the contributor should earn, which also implies how much $JOY they will earn.

### Reporting

The [#working-group-summary](general-working-group-score.md#working-group-summary "mention") for the HR working group must include information about the following

* What bounties where started work on, with information about which were based on a template and which were based on user input.
* What bounties are being worked on, which are not yet completed, and what progress was made in this period, as well as a new ETA on delivery.
* What bounties resulted in a successful payment, to whom, and why.
* What bounties resulted in no payment, to whom, and why.
* What bounties failed during the judgement period because the oracle did not submit a valid judgement.
* What template bounties should have their budgets adjusted, and why.

## CRM

The Jsgenesis Customer Relationship Management (CRM) system is a datawarehouse operated by Jsgenesis as a central source of truth for the state and histroy of the Joystream testnets, it will go away on mainnet. It holds information about&#x20;

* council periods
* founding members
* community members
* $JOY allocations
* bounties

and much more. The HR working group has some limited ability to manage the information here, as needed or their role. Here are the official forms for data entry and updating in the CRM relevant to the activities of this group:

* **Adding**/**Updating a person to the CRM:** `add link`
* **Registering an interaction:** `add link`
* **Add/Update bounty template:** `add link`

## Knowledge Base

{% embed url="https://joystream.notion.site/Human-Resources-ab782adffbdd4be497654f9e48309e2a" %}
Human Resources Working Group Knowledge Base
{% endembed %}

## Score

The HR working group score is computed as follows

`[GENERAL_WG_SCORE + GREETING_SCORE + ONBOARDING_SCORE + CATALYZING_SCORE + BOUNTY_MANAGEMENT]/(5*2^{N})`

where

* `GENERAL_WG_SCORE` : is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`30%`**.
* `GREETING_SCORE`:  is a score computed by Jsgenesis staff for the quality and speed of the greeting activity, which will be in the range \[0, 1], and will emphasize
  * Latency: the time it takes from a new person joining until someone gets in touch. Between **`8am` ** to **`23pm`** (CET), greeting time must be less than **`2 minutes`**.
  * Capture: The% of interactions that lead to a membership getting created and data entered into CRM, and the quality of this data.
* `ONBOARDING_SCORE`: is a score computed by Jsgenesis staff for the quality of onboarding activity, which will be in the range \[0, 1], and will emphasize the % of captured persons who are&#x20;
  * assigned a bounty
  * apply for a working group role with a credible application
  * stand for the council with a credible candidacy
  * have a bounty created for them
* `CATALYZING_SCORE`: is `1/percentile(75%, [x_1, ..., x_l])` , which will be in the range \[0, 1], where&#x20;
  * `percentile(X,S)` returns the `X`th percentile in non-empty sequence of observations _S._&#x20;
  * `x_i` is the number of days since the last registered interaction in the CRM with the ith non-founding member in the CRM as of the end of the period.&#x20;
* `BOUNTY_MANAGEMENT` : is a score computed by Jsgenesis staff for the quality of bounty management, which will be in the range \[0, 1].
* `N` : The number of catastrophic error instances which occurred, as defined below.

### Catastrophic Errors&#x20;

#### **Inadequate Report**

An inadequate report addendum about the bounties was provided, for example by missing or incorrect information.

**Budget Template Violation**

A bounty was created with an amount of $tJOY exceeding the current template budget.

**Missing Judgement**

A bounty did not receive oracle judgement.



****
