---
description: Metrics used to compute score for HR working group.
---

# Human Resources Score

## Overview

The HR working group activities relevant to scoring will generally fall into one of the following categories:

* **Greeting:** Engage with every new person entering the official [Official Discord](https://discord.com/invite/DE9UN3YpRP).
* **Onboarding:** Get new persons setup with a first membership and added to the [#crm](human-resources-score.md#crm "mention").
* **Catalyzing:** Get persons started with a concrete activity, such as creating a bounty, working on an existing bounty or applying for a role.
* **Nurture:** To engage and re-engage existing persons in the CRM who are not yet founding members, to encourage them to continue, help them get answers to questions, and gather insights about their experience to support the overall success of the founding member program.
* **Bounty management:** Get new, and existing, people to work on small one off tasks as a way to get into more permanent and long running roles in the system.

## Greeting

New people will continuously be arriving in the Discord, both directly, and through a website chat widget installed on the Joystream website.

`<add picture of Widgetbot on site>`

All new persons should be

* greeted by a member in the HR working group in the `#welcome` or `#general` channels,
* offered assistance in solving CAPTCHAs if needed,

## Onboarding

As soon as possible after being greeted, the objective of the HR worker is to do the following in the given order

1. Capture the person in the CRM, so that they can be catalyzed later and the project captures relevant up to date information about who is arriving, and from where,
2. Get the person to create a membership on-chain, with accurate referral information and metadata, and also some initial $tJOY to get started using the chain,
   * This data must also be ado the person in the CRM
3. Get the person into a specific activity, aligned with their skills and interests, and with the needs of the network, allowing them to earn $tJOY and $JOY. This is first achieved by developing an understanding of the person in terms of skills and interests, and the filtering the set of near term opportunities through this profile. The major opportunities are
   1. Starting to work on an existing bounty, from the bounty template in the CRM, or assist them in creating a custom bounty.
   2. Getting a role in a working group where there is soon space for newcomers.
   3. Running as a candidate for the council.
   4. Creating a new bounty specifically based on this persons skills and interests.

This onboarding should always be initiated right after the initial greeting stage, however, it may also be attempted as part of a catalyzing effort for a dormant person who never graduated into a substantive activity. The outcome of an attempt should be recorded in the CRM.

## Catalyzing

Invariably, people will drop off at various level of progression before becoming founding members. Some may never even get started beyond setting up a membership. This could be for a variety of reasons. Since we are recording all interactions in th CRM, we have visibility into the history of correspondences between the HR group and a given person, and we can see the history of activities they have been involved in. This allows the HR group to check in with people as they stall and _catalyze_ them to continue their journey, as well as capture valuable information about why they stalled.

## Bounty Management

### Creation

As mentioned prior, [bounties](../../system/bounties/ "mention") are an excellent low barrier to entry means of allowing total newcomers to participate, start earning $tJOY and $JOY, and learning the system and community. Bounties are created on-chain using either

* Pre-prepared bounties living in the `BountyTemplate` table of the CRM. Bounties may only be added here by
  * the HR lead
  * Jsgenesis staff
* Input from a user about doing a project which does not exist may be added upon request by the HR lead or Jsgenesis based on the scope and associated reward of the bounty

The funding from the bounties always come from the HR working group workers, who should be provided small $tJOY cash funds from the lead, allowing them to create new bounties on an ongoing basis for new people showing up continuously in the community.&#x20;

It is the responsibility of the lead to responsibly manage how much each worker is entrusted with over any given period of time. A bounty created on-chain _must_ reference the relevant `BountyTemplate` instance in the CRM, by ID, which is why those instances can never be deleted, and they _must_ respect the $tJOY budget limit specified in the template. If this limit is found to be too low, only the lead or Jsgenesis can update the budget. The worker creating the on-chain bounty must make sure to select the appropriate oracle, which is most likely the HR worker with most experience in the relevant area of the platform. If the bounty requires specific knowledge not currently available in the HR group, the HR group is responsible for recruiting in the system to perform this role, and agreeing on any payment for said service. Just as for the funding of a bounty, said reward must be set aside in the budget, and held in escrow in some reasonable way agreed by to by all parties.

Lastly, the worker must negotiate a plausible working period, and oracle judgement duration for the bounty.\
\
<mark style="color:red;">**`Be aware that Jsgenesis staff will be conducting probing experiments to see how funds are allocated to bounties under false identities.`**</mark>

### **Management**

It is the responsibility of each worker acting as the oracle for a bounty to check up on progress and log this using the on-chain discussion system. If the contributor is getting stuck or delayed, this must be logged publicly, and the oracle should help to push the contributor forward, but also establish clear forward looking expectations about the possibility that the bounty will be cancelled without the contributor getting anything, if sufficient progress is not made in due time.

### Resolution

At some point, the oracle must decide the outcome of the bounty during the judgment period. This really boils down to determining how much, if any, part of the initial $tJOY bounty budget the contributor should earn, which also implies how much $JOY they will earn.

### Reporting

The [#working-group-summary](general-working-group-score.md#working-group-summary "mention") for the HR working group must include information about the f

## CRM

The Jsgenesis Customer Relationship Management (CRM) system is a datawarehouse operated by Jsgenesis as a central source of truth for the state and histroy of the Joystream testnets, it will go away on mainnet. It holds information about

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

```
HR_SCORE = [GENERAL_WG_SCORE + REPORT_SCORE + GREETING_SCORE + BOUNTY_GENERATION_SCORE]/(4^{N})
```

### `GENERAL_WG_SCORE`

Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention") where the opportunity target is **`20%`**.

### `REPORT_SCORE`

In addition to what is outlined in the [#working-group-summary](general-working-group-score.md#working-group-summary "mention"), the working group report must include a section covering

* How many new people reached out to the group in discor, and how many of them were captured in the CRM.
* What, and how many, bounties were funded by the group during the council period, and for each bounty
  * Which bounty template id was used for which bounty on-chain id&#x20;
  * Which HR worker created, assigned and funded it
  * Whom the bounty was created for
  * Who was assigned as the oracle
* What bounties, regardless of which council period it was started, are being worked on, which are not yet completed, and what progress was made in this period, as well as a new ETA on delivery.
* What, and how many, bounties created by the group were completed during the council period, and for each bounty
  * What was the result, meaning how much was paid (if any), to whom and why
  * How much was given to the oracle for providing the judgement
  * A timeline of all steps
* What bounties failed during the judgement period because the oracle did not submit a valid judgement.
* An overview of which bounty templates, and in general types of bounties, are the most and least sought after, and what types of bounty templates more options are needed.
* Recommendations for "graduates" that should be considered for a role and a specific working group, or handed a spot the council.
* What template bounties should have their budgets adjusted, and why.

Whereas the same deadline as general report applies, there is no requirement to submit a temporary report for this.

### `GREETING_SCORE`

_Objective:_ `Ensuring WG is responsive and helpful on Discord, and are capturing interactions in the CRM.`

#### Instructions

* Availability to respond to newly arriving participants is an essential element of participation within the HR Working Group.
  * Working group lead directs the creation of a table within Notion or an alternative platform to show the availability of the WG participants for the week
  * Checks of CRM form for reporting availability reflect accurately the same information.
  * Pings in #start-here channel get a response from one of the available integrators in a timely fashion.
  * New members are directed to create new memberships as a first step in the onboarding, and to allow them to be tracked in the CRM (before that, store the data somewhere else)
  * Conduct a quick round of questions, in order to get a flavor for what they would like to do on/for the platform

#### Scoring Calculations

Let:

* `delta_t_a` be the average difference in timestamp \[min] from a user posts in the #start-here channel, until a greeter responds
  * if the user posts between midnight and noon (CET), it counts as being posted at noon
* `ONBOARDING_SCORE` be the fraction of users posting in #start-here that gets an entry in the CRM

Then:

```
TIMELINESS_SCORE = max(delta_t_a/10,1)

GREETING_SCORE = (TIMELINESS_SCORE + ONBOARDING_SCORE)/2
```

### `BOUNTY_SCORE`

#### Instructions

The first step after capturing a new person in the CRM should be to help them getting a bounty to work on.

Note that in the calculations below, only bounties that are created by the HR group for onboarding purposes counts.

#### Scoring Calculations

Let:

* `BOUNTIES_STARTED` be the amount of bounties created on chain and funded by the group, for a person that has gone through the groups greeting and onboarding process.
* `BOUNTIES_COMPLETED` be the amount of bounties completed, and with a full or partial payment. Note that bounties created in previous council periods counts.

Then:

```
BOUNTY_SCORE = max(BOUNTIES_STARTED/10,1) + (BOUNTIES_COMPLETED/5,1)
```

### Catastrophic Errors

#### **Inadequate Report**

An inadequate report addendum about the bounties was provided, for example by missing or incorrect information.

**Budget Template Violation**

A bounty was created with an amount of $tJOY exceeding the current template budget.

**Missing Judgement**

A bounty did not receive oracle judgement, and the person assigned the bounty wasn't compensated within 24h of the oracle judgement period expriring.
