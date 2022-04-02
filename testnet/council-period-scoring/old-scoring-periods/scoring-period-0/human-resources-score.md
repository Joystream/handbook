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

It is the responsibility of each worker acting as the oracle for a bounty to check up on progress and log this using the on-chain discussion system. If the contributor is getting stuck or delayed, this must be logged publicly, and the oracle should help to push the contributor forward, but also establish clear forward looking expectations about the possibility that the bounty will be cancelled without the contributor getting anything, if sufficient progress is not made.

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

```
HR_SCORE = 0.1*GENERAL_WG_SCORE + 0.2*PROTOCOL_SCORE + 0.25*CRM_SCORE + 0.2*TIMELINESS_SCORE + 0.25*WELCOMING_SCORE
```

### `GENERAL_WG_SCORE`
Is computed with metric defined in [general-working-group-score.md](general-working-group-score.md "mention"). where the opportunity target is **`0%`**.


### `PROTOCOL_SCORE`
*Objective:* `Working out the protocols`

#### Instructions
Working group (emphasis on lead) coordinates with Robert and Ben to establish the protocols for communicating with new joiners. This can be an informal process on Discord which then results in some basic principles for communicating with new participants being shared in the community notion. It can also involve the working group members suggesting changes to the Discord/Chatbot/Onboarding design to optimize any aspect of their work.

#### Scoring Calculations
The `PROTOCOL_SCORE` is graded subjectively.

### `CRM_SCORE`
*Objective:* `Familiarity with tools (principally CRM)`

#### Instructions
- All HR WG participants are added to the community notion, timesheet spreadsheet/table and retool CRM tool.
- All HR WG participants participate in a brief training session with Ben to get them familar (and added to) with CRM, or alternatively watch brief video series created by him, then are briefly tested and scored by him on their understanding (this will be a very simple test just to show they understand how to use the CRM forms).
  - The HR Group is responsible for organizing this

#### Scoring Calculations
The `CRM_SCORE` is graded subjectively.

### `TIMELINESS_SCORE`
*Objective:* `Ensuring WG is responsive in Discord in timely fashion`

#### Instructions
- Availability to respond to newly arriving participants is an essential element of participation within the HR Working Group.
- Therefore, even in this first week, there will be an emphasis on responding to new people and JSG dummy accounts within the #start-here channel.
  - Working group lead directs the creation of a table within Notion or an alternative platform to show the availability of the WG participants
  - Checks of CRM form for reporting availability reflect accurately the same information.
  - Pings in #start-here channel get a response from one of the available integrators.

#### Scoring Calculations
The `TIMELINESS_SCORE` is graded subjectively.


### `WELCOMING_SCORE`
*Objective:* `Ensuring WG is responsive in Discord in timely fashion`

#### Instructions
- New members are directed to create new memberships as a first step in the onboarding, and to allow them to be tracked in the CRM (before that, store the data somewhere else)
  - Conduct a quick round of questions, in order to get a flavor for what they would like to do on/for the platform
  - They are further told to check in next week, and that a Bounty will be created for them then

#### Scoring Calculations
The `WELCOMING_SCORE` is graded subjectively.
