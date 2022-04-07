---
description: Deeper dive on to the councils own metrics and rewards structure.
---

# Overview
The Councilors themselves are the only participants whose rewards are _directly_ impacted by the metrics we are, and will measure.

XXX
Looking closely at the two most natural comparisons to what the Council means to Joystream, namely - what the executive branch of a government means to a state and what the board of directors means to a company, we see:

## Governments
Broken down to the core, the executive branch of a government;
- Uses polls do get an understanding what the people want
- Campaigns based on said input
- XXX

The Councils activities relevant to scoring will, generally, fall into one of the following categories:

* Use the current scoring metrics to delegate tasks and allocate resources to the Leads
  * This could be conveyed sufficiently in a good [Council Period Plan](#plan_score), but some extra communication is likely needed.
* Follow up the working groups (leads), to ensure they are indeed pulling the same way
* Vote on proposals, and generally be responsive

## `PLAN_SCORE`
The Council Plan is the Councils formal way of instructing their Leads, and informing stakeholders what their focus will be for their Term.

Where Jsgenesis will provide a clear way to calculate the individual Working Groups scores, and a weighting that may be somewhat indicative of how the budget should be distributed, in the end it's the Council whose rewards depends on how well the Leads organize their Workers, allocates the groups resources, and pushes an agenda.

### Purpose of the Plan Score
Some examples of the importance of the Council Period Plan:

#### Monitor the Outputs
Oftentimes, the `<WG>_SCORE` depends on submitting reports, documenting their actions and other tasks that aren't solely determined by getting and parsing chain-state data. Suppose Jsgenesis requires that it's added to the groups [notion space](https://joystream.notion.site/joystream/Joystream-Workspace-1175fcb1cc644fdb874558181fd2dbee) by the end of the term (block `n`). As it's the Council that loses out if this isn't done, it might be wise for the Council to require that it's done by block `n-m`, so they can review the work in advance.


#### Differences in Priorities
A "bad" Lead may have "bad" priorities or simply not be fit for the role. A good Lead may have "good" priorities, but not necessarily the same as the Councils!

For every group, some metrics will be more appealing than others. For the HR group, it can be how _quickly_ they respond to all inquires, for a Distributor Lead how great the playback speed is. These are great metrics that are very visible to the outside world, and does indeed indicate something is working! However, this may cause them to sacrifice on the _quality_ of responses and follow up for newcomers, or completely ignore offering opportunities to new Workers.

#### Differences in how to Achieve a Goal
A group Lead should have, or at least be able to develop a path to address and improve a bad metric. However, some of the Councilors should also have some insight here. In some cases, the Council may want to force their opinion here and require path `X`, but asking the Lead to present a plan could be an alternative. Jsgenesis may not care how a goal is achieved, and if so, won't ask. That doesn't necessarily mean the Council shouldn't care either - after all, it's their rewards on the line.

#### Explain the Budget
The weights assigned to a WG in a particular term MAY be a good indication on how to allocate your budget, but it's unlikely to be ideal. Although the Leads are working for you, they may be easier to work with if they understand why they are seeing their budget cut while getting a great score and a high weight.


### Grading of the Plan Score
Although the plan will get a grading, it won't be weighted very heavily, for the simple reason that it will carry enough "weight" on its own. If the Council ignores this, it's likely that the `<WG>_SCORE` will suffer as a result, and their rewards will follow.

### Tips
The below list should not be seen as requirements. It's simply suggestions based on theory or empirical observations made by Jsgenesis:
- Consider assigning the "main" responsibility for different Working Groups etc to individual Council Members.


## `SUMMARY_SCORE`
The summary serves multiple purposes:
- Acts as a handover to the next/incoming Council
- Used to grade some of the `<WG>_SCORE` metrics (eg. `*_OPPORTUNITIES_SCORE`)
- Used to update some of the parameters in `<WG>_SCORE` metrics, or change the metrics outright (if argued sufficiently)
- General feedback and suggestions for improvements to Jsgenesis

### Handover
No organization can thrive (or even survive) unless there's a "peaceful transition of power". A Councilor that ragequits if not re-elected can't expect another chance from Jsgenesis, and shouldn't from the community either. Ideally, the handover should be a conversation, but the very least one should require is to:
- leave without "broken" budgets
- lessons learned

### Basis of Grading
Jsgenesis will not require, or grade, the individual working groups reports. The Council however, will need a variety of data for their reports.

It will also serve as the basis for grading some of metrics.

### Feedback
For new metrics especially, but also due to some specific events, Jsgenesis may have set the expectations to high, or chosen a bad way to measure something. In that case, the Council may do themselves (assuming some of them are elected again), the project or at the very least, future councilors a service by raising it.

It's also a great way to raise that documentation is poor (and where), that some parameters or constants in the chain is bad, etc.
