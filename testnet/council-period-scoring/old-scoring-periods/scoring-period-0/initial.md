## Storage Provider Working Group
- **Goal**: Get the all data objects migrated from Giza to a storage node running on Olympia.
- **Global Weight** 0.60
- **Scope of Work 1:**
    - `Create an opening for the SP Lead`
  - *Notes:*
    - What goes into the opening should be agreed in advance. Feel free to go through the `Create Working Group Lead Opening` flow, sending the tx will fail until a Council is elected!
    - Publish the questions and advance (on discord -> `#storage-providers`) so that applicants can "pre-apply".
    - Review and discuss these application, both amongst yourselves, and perhaps with the applicants themselves, to speed up the process of the actual hiring.
  *Scoring Calculations*
    1. Weight: `0.2`
      - let:
        - `opening_approved_block` be the blockheight where the opening is approved
        - `quality_of_opening` be the subjective evaluation [0,1] of the questions the Council asks the applicants in the actual opening.
        - `create_opening_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(44000 - opening_approved_block)/1000 + 0.2*quality_of_opening`

- **Scope of Work 2:**
    - `Hire a qualified SP Lead`
  - *Notes:*
    - Qualified, in this context means one that is prepared. That again means:
      - The user has deployed a VPS for the purpose
      - The user has downloaded and compiled and deployed all the software for `olympia`:
        - running a synced `joystream-node`
        - running a synced `query-node`
        - prepared hosting
  *Scoring Calculations*
    2. Weight: `0.3`
      - let:
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `preparation_score` be the subjective evaluation [0,1] of how well the Lead is prepared for the role
        - `hire_lead_score` be the final score [-1,1]
      - then:
        - `hire_lead_score` = `(45000 - lead_hired_block)/3600 + 0.5*preparation_score`

- **Scope of Work 3:**
    - `Lead migration readiness`
  - *Notes:*
    - In addition to having prepared the "hardware", the Lead should also be ready to go as quickly as possible
      - after getting hired, the Lead is ready to make the initial transactions
      - the Lead is proposing reasonable transactions
  *Scoring Calculations*
    3. Weight: `0.3`
      - let:
        - `approved_lead_transactions` be the transaction the Lead proposes to make before starting the migration, that gets approved as is
        - `required_lead_transactions` be the amount of transaction the Lead will need to make, in order to start the migration
          - note that the amount can vary depending on the Leads preferred setup (eg. amount of Workers and nodes)
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `lead_readiness_block` be the blockheight the Lead has completed the "approved" transactions
        - `migration_readiness_score` be the final score [-1,1]
      - then:
        - `migration_readiness_score` = `0.5*(lead_readiness_block - lead_hired_block)/600 + 0.5*preparation_score + 0.5*approved_lead_transactions/required_lead_transactions`

- **Scope of Work 3:**
    - `Lead migration availability and responsiveness`
  - *Notes:*
    - Unlike the other scores, this will be purely subjective
      - Is the Lead generally available until the migration is complete?
      - Is the Lead responsive on discord, and providing warnings if unavailable for the next `n` hours?
  *Scoring Calculations*
    4. Weight: `0.2`
        - `lead_availability`

## Content Working Group
- **Goal**: Get the video and channel categories created on Olympia.
- **Global Weight** 0.1
- **Scope of Work 1:**
    - `Hire a Content Lead`
  - *Notes:*
    - As no action is required by the Content Lead, there are no further requirements
  *Scoring Calculations*
    1. Weight: `1.0`
      - let:
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `hire_lead_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(45000 - lead_hired_block)/1800`


## Distributor Working Group
- **Goal**: Reduce content downtime by having distributor nodes set up for Olympia by the time migration is completed
- **Global Weight** 0.15
- **Scope of Work 1:**
    - `Create an opening for the Distributor Lead`
  - *Notes:*
    - What goes into the opening should be agreed in advance. Feel free to go through the `Create Working Group Lead Opening` flow, sending the tx will fail until a Council is elected!
    - Publish the questions and advance (on discord -> `#distributors`) so that applicants can "pre-apply".
    - Review and discuss these application, both amongst yourselves, and perhaps with the applicants themselves, to speed up the process of the actual hiring.
  *Scoring Calculations*
    1. Weight: `0.3`
      - let:
        - `opening_approved_block` be the blockheight where the opening is approved
        - `quality_of_opening` be the subjective evaluation [0,1] of the questions the Council asks the applicants in the actual opening.
        - `create_opening_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(44000 - opening_approved_block)/1000 + 0.2*quality_of_opening`

- **Scope of Work 2:**
    - `Hire a qualified Distributor Lead`
  - *Notes:*
    - Qualified, in this context means one that is prepared. That again means:
      - The user has deployed a VPS for the purpose
      - The user has downloaded and compiled and deployed all the software for `olympia`:
        - running a synced `joystream-node`
        - running a synced `query-node`
        - prepared hosting
  *Scoring Calculations*
    2. Weight: `0.3`
      - let:
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `preparation_score`  be the subjective evaluation [0,1] of how well the Lead has prepared for the role
        - `hire_lead_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(45000 - lead_hired_block)/3600 + 0.5*preparation_score`

- **Scope of Work 3:**
    - `Bucket and node deployment`
  - *Notes:*
    - When the migration is completed, the Lead has deployed a system that can serve all `olympia` content
      - The user understands the concept of (distributor) `buckets-families` and `buckets`, how to create them, and how to set policies that will distribute them in a way that ensures we can quickly achieve "good" coverage
      - The user hires the necessary Workers, and have them operate "correct" buckets
        - operate in this context means that they are working, and serves the content on request
   *Scoring Calculations*
    3. Weight: `0.4`
      - let:
        - `bags_total` mean the total amount of `bags` in the system
        - `bags_covered` mean the amount of `bags` served by at least one **operating** distributor node
          - `bag_coverage_score` = `(bags_covered - 0.9*bags_total)/(0.1*bags_total)`
        - `assets_total` mean the total amount of (accepted) `dataObjects` in the system
        - `assets_covered` mean the amount of `dataObjects` served by at least one
          - `asset_coverage_score` = `(assets_covered - 0.9*assets_total)/(0.1*assets_total)`
         **operating** distributor node
        - `bag_duplication` mean the average amount of "independent", **operating** nodes (not workers) serving each `bag`
      - then:
        - `deployment_score` = `0.3*bag_coverage_score + 0.3*asset_coverage_score + 0.4*bag_duplication/2`


## Forum Working Group
- **Goal**: Enable usage of the Forum by creating an initial set of categories.
- **Global Weight** 0.15
- **Background:**
  - The forum can't be used without any categories.
  - Without first hiring a Lead, these can't be created
  - Creating categories is done with the `joystream-cli`
- **Scope of Work 1:**
  - `Hire a Forum Lead`
  - *Notes:*
    - The is free to choose whether to hire the "actual" Lead right away, or go for a temporary Lead (for example one of their own)
  *Scoring Calculations*
    1. Weight: `0.2`
      - let:
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `hire_lead_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(44000 - lead_hired_block)/800`
- **Scope of Work 2:**
  - `Create a reasonable set of initial categories`
  - *Notes:*
    - What is reasonable for the initial categories are of course open to interpretation
    - Note once a category has been (regardless of the name/description), all newly created Bounties will create a discussion thread in the first category, so make sure to make that one Bounty related!
  *Scoring Calculations*
    1. Weight: `0.8`
      - let:
        - `bounty_category_block` be the blockheight where the first forum category is created, and titled appropriately
        - `initial_categories` be the blockheight where some set of categories is created, such that users can discuss the most pertinent, urgent and important topics on the platform, without having to create thread in inappropriate categories
      - then:
        - `create_opening_score` = `0.5*(44400 - bounty_category_block)/1200 + 0.5*(45000 - initial_categories)/1800`

## Member Working Group
- **Goal**: Get the membership faucet working without the need for
- **Global Weight** 0.05
- **Scope of Work 1:**
    - `Create Membership Lead Opening`
  - *Notes:*
    - As no action is required by the Content Lead, there are no further requirements
  *Scoring Calculations*
    1. Weight: `1.0`
      - let:
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `hire_lead_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(45000 - lead_hired_block)/1800`


---

results:
#### Storage Providers
  1. Storage Opening Prop Made: #43404 -> Opening #43465


#### Distributors
  1. Storage Opening Prop: #43387 -> Opening #43455

#### Forum
  1. Prop Made / Opening Created: #43236 / #43286
  2. Opening Fill / Hired: #43710 / #43710
  3. Bounty Cat: [#44850](https://polkadot.js.org/apps/#/explorer/query/44850)

Membership:
Opening Proposal: [#43272](https://polkadot.js.org/apps/#/explorer/query/43272)
Opening Created: [#43318](https://polkadot.js.org/apps/#/explorer/query/43318)
Applied: [#43405](https://polkadot.js.org/apps/#/explorer/query/43405)

Lead set: [#43483](https://polkadot.js.org/apps/#/explorer/query/43483)


# After Migration
## Storage Provider Working Group
- **Goal**: Get a robust storage system
- **Global Weight** `xxx`
- **Scope of Work 1:**
    - `Ensure content directory integrity through redundancy`
  - *Notes:*
    - If all `bags` are stored by a single node only, or in one data center/VPS provider only, the system may crash entirely
    - "Operating/operated" means that a bucket is assigned to a Worker, the worker is running a node that can be uploaded to (by a channel owner) and downloaded from (by a distributor)
  *Scoring Calculations*
    1. Weight: `0.2`
      - let:
        - `replication_rate` be the number of operated buckets currently holding a bag
        - `Sig`
        - `quality_of_opening` be the subjective evaluation [0,1] of the questions the Council asks the applicants in the actual opening.
        - `create_opening_score` be the final score [-1,1]
      - then:
        - `create_opening_score` = `(44000 - opening_approved_block)/1000 + 0.2*quality_of_opening`

- **Scope of Work 2:**
    - `Hire a qualified SP Lead`
  - *Notes:*
    - Qualified, in this context means one that is prepared. That again means:
      - The user has deployed a VPS for the purpose
      - The user has downloaded and compiled and deployed all the software for `olympia`:
        - running a synced `joystream-node`
        - running a synced `query-node`
        - prepared hosting
  *Scoring Calculations*
    2. Weight: `0.3`
      - let:
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `preparation_score` be the subjective evaluation [0,1] of how well the Lead is prepared for the role
        - `hire_lead_score` be the final score [-1,1]
      - then:
        - `hire_lead_score` = `(45000 - lead_hired_block)/3600 + 0.5*preparation_score`

- **Scope of Work 3:**
    - `Lead migration readiness`
  - *Notes:*
    - In addition to having prepared the "hardware", the Lead should also be ready to go as quickly as possible
      - after getting hired, the Lead is ready to make the initial transactions
      - the Lead is proposing reasonable transactions
  *Scoring Calculations*
    3. Weight: `0.3`
      - let:
        - `approved_lead_transactions` be the transaction the Lead proposes to make before starting the migration, that gets approved as is
        - `required_lead_transactions` be the amount of transaction the Lead will need to make, in order to start the migration
          - note that the amount can vary depending on the Leads preferred setup (eg. amount of Workers and nodes)
        - `lead_hired_block` be the blockheight where the Lead is hired
        - `lead_readiness_block` be the blockheight the Lead has completed the "approved" transactions
        - `migration_readiness_score` be the final score [-1,1]
      - then:
        - `migration_readiness_score` = `0.5*(lead_readiness_block - lead_hired_block)/600 + 0.5*preparation_score + 0.5*approved_lead_transactions/required_lead_transactions`

- **Scope of Work 3:**
    - `Lead migration availability and responsiveness`
  - *Notes:*
    - Unlike the other scores, this will be purely subjective
      - Is the Lead generally available until the migration is complete?
      - Is the Lead responsive on discord, and providing warnings if unavailable for the next `n` hours?
  *Scoring Calculations*
    4. Weight: `0.2`
        - `lead_availability`
