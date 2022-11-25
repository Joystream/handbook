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

![](<../../.gitbook/assets/Screenshot 2022-04-29 at 14.50.27.png>)

All new persons should be

* greeted by a member in the HR working group in the `#welcome` or `#general` channels,
* offered assistance in solving CAPTCHAs if needed,

## Onboarding

As soon as possible after being greeted, the objective of the HR worker is to do the following in the given order

1. Capture the person in the CRM, so that they can be catalyzed later and the project captures relevant up to date information about who is arriving, and from where,
2. Get the person to create a membership on-chain, with accurate referral information and metadata, and also some initial $tJOY to get started using the chain.
3. Get the person into a specific activity, aligned with their skills and interests, and with the needs of the network, allowing them to earn $tJOY and $JOY. This is first achieved by developing an understanding of the person in terms of skills and interests, and the filtering the set of near term opportunities through this profile. The major opportunities are
   1. Starting to work on an existing bounty, from the bounty template in the CRM, or assist them in creating a custom bounty (a new bounty specifically based on this persons skills and interests).
   2. Getting a role in a working group where there is soon space for newcomers.
   3. Running as a candidate for the council.

This onboarding should always be initiated right after the initial greeting stage, however, it may also be attempted as part of a catalyzing effort for a dormant person who never graduated into a substantive activity. The outcome of an attempt should be recorded in the CRM.

## Catalyzing

Invariably, people will drop off at various level of progression before becoming founding members. Some may never even get started beyond setting up a membership. This could be for a variety of reasons. Since we are recording all interactions in the CRM, we have visibility into the history of correspondences between the HR group and a given person, and we can see the history of activities they have been involved in. This allows the HR group to check in with people as they stall and _catalyze_ them to continue their journey, as well as capture valuable information about why they stalled.

## Bounty Management

### Creation

As mentioned prior, [bounties](../../system/bounties/ "mention") are an excellent low barrier to entry means of allowing total newcomers to participate, start earning $tJOY and $JOY, and learning the system and community. Bounties are created on-chain using either

* Pre-prepared bounties living in the `BountyTemplate` table of the CRM. Bounties may only be added here by
  * the HR lead
  * Jsgenesis staff
    * Note that the technical bounties found in the Bounties Backlog [here](https://github.com/orgs/Joystream/projects/55) can be considered added by the Jsgenesis staff.
* Input from a user about doing a project which does not exist may be added upon request by the HR lead or Jsgenesis based on the scope and associated reward of the bounty

The funding from the bounties always come from the HR working group workers, who should be provided small $tJOY cash funds from the lead, allowing them to create new bounties on an ongoing basis for new people showing up continuously in the community. The same applies if outside resources are needed to act as oracles. There are surely many ways this funding can be handled, but we need to make sure that any costs are covered in a way that ensures the $tJOY are eligible for $JOY for the recipient when applicable. That means:

* If a worker and/or lead creates and funds the bounty, the lead should consider that reimbursing through the HR budget (ie. through increased rewards) would mean they earn JOY rewards for these amounts. Instead, create funding request, and state it is not $JOY eligeble.
* If there is a need for an outside oracle (eg. technical bounties), they can be paid by being temporarily hired as a worker in the HR group, through a funding request (that the HR lead creates and states IS eligeble for $JOY), or through the bounty itself.

It is the responsibility of the lead to responsibly manage how much each worker is entrusted with over any given period of time. A bounty created on-chain _must_ reference the relevant `BountyTemplate` instance in the CRM, by ID, which is why those instances can never be deleted, and they _must_ respect the $tJOY budget limit specified in the template. If this limit is found to be too low, only the lead or Jsgenesis can update the budget. The worker creating the on-chain bounty must make sure to select the appropriate oracle, which is most likely the HR worker with most experience in the relevant area of the platform. If the bounty requires specific knowledge not currently available in the HR group, the HR group is responsible for recruiting in the system to perform this role, and agreeing on any payment for said service. Just as for the funding of a bounty, said reward must be set aside in the budget, and held in escrow in some reasonable way agreed by to by all parties.

Lastly, the worker must negotiate a plausible working period, and oracle judgement duration for the bounty.\
\
<mark style="color:red;">**`Be aware that Jsgenesis staff will be conducting probing experiments to see how funds are allocated to bounties under false identities.`**</mark>

### **Management**

It is the responsibility of each worker acting as the oracle for a bounty to check up on progress and log this using the on-chain discussion system. If the contributor is getting stuck or delayed, this must be logged publicly, and the oracle should help to push the contributor forward, but also establish clear forward looking expectations about the possibility that the bounty will be cancelled without the contributor getting anything, if sufficient progress is not made in due time.

### Resolution

At some point, the oracle must decide the outcome of the bounty during the judgment period. This really boils down to determining how much, if any, part of the initial $tJOY bounty budget the contributor should earn, which also implies how much $JOY they will earn.

## CRM

The Jsgenesis Customer Relationship Management (CRM) system is a data warehouse operated by Jsgenesis as a central source of truth for the state and histroy of the Joystream testnets, it will go away on mainnet. It holds information about

* council periods
* founding members
* community members
* $JOY allocations
* bounty templates

and much more. The HR working group has some limited ability to manage the information here, as needed or their role. Here are the official forms for data entry and updating in the CRM relevant to the activities of this group:

* [Adding a person to the CRM](https://joystream.retool.com/embedded/public/5270b412-c53f-4620-886e-71c55a111905)
* [Updating a person in the CRM](https://joystream.retool.com/embedded/public/1fe5d08c-69ea-4c9c-844c-4a4212a7aa29)
* [Registering an interaction](https://joystream.retool.com/embedded/public/90e0966d-e253-451b-b1b7-0c27e51ebfff)
* [Update bounty template status](https://joystream.retool.com/embedded/public/24a94b16-27d6-4efb-89ce-ac9fa58d06bd)

## Reporting

The reporting for the HR working group should be split in two parts. One part addressing what is outlined in the[#working-group-summary](general-working-group-score.md#working-group-summary "mention"), the other under `REPORT_SCORE` below.

## Knowledge Base

{% embed url="https://joystream.notion.site/Human-Resources-ab782adffbdd4be497654f9e48309e2a" %}
Human Resources Working Group Knowledge Base
{% endembed %}

## Score

The HR working group score is computed as follows

```
HR_SCORE = [2*FOUNDING_MEMBER_STATUS_SCORE]/(2*2^{N})
```

where

`N` : The number of catastrophic error instances which occurred, as defined below.

### `FOUNDING_MEMBER_STATUS_SCORE`

#### HOLD

### Catastrophic Errors

#### **Inadequate Report**

An inadequate report addendum about the bounties was provided, for example by missing or incorrect information.

**Missing Judgement**

A bounty did not receive oracle judgement, and the person assigned the bounty wasn't compensated within 24h of the oracle judgement period expiring.



### Need help understanding something?

We know there are still lots of things that is unclear, and we want to address this. Async discord chats are not always the best way to communicate, so once a week, the lead of a group can reach out to `@blrhc#0162` and `@bwhm#6514` for a zoom call. Prepare a clear agenda, and propose a couple timeslots, as we won't always be available.

Only workers in the group is invited, so we can keep focus on the problems, and keep a lower barrier for asking!
