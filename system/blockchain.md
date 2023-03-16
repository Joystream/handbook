---
description: The centerpiece of the Joystream Network
---

# ⛓ Blockchain

## Introduction

At the heart of the Joystream Network sits a content, social, governance and asset ledger that coordinates the activity of all consumers, service providers, creators and applications.

## Overview

The blockchain is a standalone L1 blockchain with it's own independent validator set. Currently, there is only a single reference implementation, which is written in Rust, and is based on the [Substrate](https://docs.substrate.io/) blockchain development framework. This means that the consensus and networking logic have already been implemented, and the community can focus on the domain specific state machine which is core to Joystream. This is also written in Rust, and this statemachine - called the _Runtime_, runs in a [WebAssembly](https://en.wikipedia.org/wiki/WebAssembly) execution environment. While it is possible to incorporate a smart contract environment, like the [EVM](https://substrate-developer-hub.github.io/docs/en/knowledgebase/smart-contracts/evm-pallet), that is currently not part of the Joystream runtime.

## Consensus

Validators are selected based on [Nominated PoS](https://arxiv.org/abs/2004.12990), and block production occurs in a slot-based stochastic block authoring schedule called [BABE](https://research.web3.foundation/en/latest/polkadot/block-production/Babe.html), or Blind Assignment for Blockchain Extension. Deterministic finality is produced through a classical BFT agreement protocol called [GRANDPA](https://arxiv.org/abs/2007.01560), or HOST-based Recursive Ancestor Deriving Prefix Agreement), which depends on ⅓ honest validator assumption.

## Resource Accounting

Weight and size



## Parameters

table of key params

* target block time: 6s
* block sapce
* weight to fee
* byte to fee
*
* max weight
* Curent runtime version (as of 2011)
* Substrate version (as of)



Forkless Upgrades

xxx

## Interoperability

## Fees

In a distributed system, a user can require nodes to perform costly computation. Depending on the design of the system, the compute may be a one time event, or it may need to be replicated by multiple parties when they attempt to validate the integrity of the system. Regardless, this ability to command the compute resources of system participants means that some mechanism is needed to restrict and ration access to such resources. In blockchain systems specifically, access is intended to be open and permissionless, hence paying for access is has been considered the most neutral solution to this problem. Fees assocaited with inclusion of transactions in the blockchain plays the role of such payments in blockchains.





Incorporate from [https://wiki.polkadot.network/docs/learn-transaction-fees](https://wiki.polkadot.network/docs/learn-transaction-fees)
