---
description: Validator and nominator specific definition of terms
---

# Glossary

## Glossary

**`bonding duration`**

The amount of `eras` before a `bonded` account that unbonds has to wait until their tokens **can** be unlocked by the `staking` lock.

This will allow the tokens to be staked for "rivalrous" purposes, and, if no other locks are applied, be spent freely.

Set to 112 `eras`, eg \~403200 blocks, or 28 days.

**`commission`**

**`candidates`**

Validators and nominators get paid from block production on the network, where validators can set a variable commission rate, which is initially subtracted from the total rewards that validator is entitled to (for that period), where the commission determines the rate of distribution for the remaining rewards set out for the nominators that are backing that validator.

Set by the validator as a percentage of the reward for each `era`.

**`election`**

An operation performed automatically on-chain, by the runtime, to elect a new set of validators for the upcoming `era`. Who gets elected depends on a variety of factors, such as the amount of `candidates`, the number of `slots` and the `total active stake` for each validator.

**`era`**

A (whole) number of `sessions`, which is the period that the validator set (and each validator's active nominator set) is recalculated and where rewards are paid out.

Target is 6 `sessions`, eg \~3600 blocks, or 6h.

**`era points`**

Every time a specific validator produces a block, they earn points. The rewards for the individual validator for that `era` are proportional to their era points, which are reset when a new `era` begins.

**`nominator`**

Accounts that select a set of validators to nominate by bonding their tokens. Nominators receive some of the validators' rewards, but are also liable for slashing if their nominated validators misbehave.

**`rewards`**

The shared rewards earned by the entire validator set for each `era`. For the individual `validator`, they are proportional to the `era points` earned.

Note that the `total active stake` does not impact the `era points` or rewards directly, but of course, unless the validator gets a slot, they will not earn any rewards.

**`session`**

A session is a Substrate implementation term for a period that has a constant set of validators. Validators can only join or exit the validator set at a session change.

Target is \~600 blocks, or 1h.

**`session keys`**

Hot (must be online) keys that are used for performing network operations by validators, for example, signing GRANDPA commit messages.

**`slashing`**

The removal of a percentage of an account's JOY as a punishment for a validator acting maliciously or incompetently (e.g., equivocating or remaining offline for an extended period).

Will apply equally to nominators of a validator that gets slashed.

**`slots`**

Total amount of spots in the validator set at any given time. Can be adjusted up or down through a proposal.

**`staking`**

The act of bonding JOY tokens by putting them up as "collateral" for a chance to produce a valid block (and thus obtain a block reward). Validators and nominators stake their JOY in order to secure the network.

**`total active stake`**

The sum of stake put up by the validator itself, plus the amount each of the (potential) `nominators` backs the validator with. Used to the determine whether the validator gets a `slot` in the validator set or not in the `election` for the upcoming era.

## Introduction

The Joystream platform state lives on a blockchain consensus system. This consensus system is a variant of classical BFT consensus combined with Proof-of-Stake to determine who gets to be a consensus participant, i.e. validator. A validator is an actor which checks the validity of newly constructed blocks, proposes new blocks and participates in the consensus process for committing new blocks to the chain. This role has a purpose very similar to the miners in the Bitcoin blockchain. Importantly, anyone can fully check the validity of the blockchain, not just validators, and this is called validation.
