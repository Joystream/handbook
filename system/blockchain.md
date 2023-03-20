---
description: The centerpiece of the Joystream Network
---

# ⛓ Blockchain

## Introduction

At the heart of the Joystream Network sits a content, social, governance and asset ledger that coordinates the activity of all consumers, service providers, creators and applications.

## Overview

The blockchain is a standalone L1 blockchain with it's own independent validator set. Currently, there is only a single reference implementation, which is written in Rust, and is based on the [Substrate](https://docs.substrate.io/) blockchain development framework. This means that the consensus and networking logic have already been implemented, and the community can focus on the domain specific state machine which is core to Joystream. This is also written in Rust, and this state machine - called the _Runtime_, runs in a [WebAssembly](https://en.wikipedia.org/wiki/WebAssembly) execution environment. _While it is possible to incorporate a smart contract environment, like the_ [_EVM_](https://substrate-developer-hub.github.io/docs/en/knowledgebase/smart-contracts/evm-pallet)_, that is currently not part of the Joystream runtime._

<figure><img src="../.gitbook/assets/Substrate node.svg" alt=""><figcaption><p>Overview of Joystream node architecture, built on Substrate.</p></figcaption></figure>

## Consensus

Validators are selected based on [Nominated PoS](https://arxiv.org/abs/2004.12990), and block production occurs in a slot-based stochastic block authoring schedule called [BABE](https://research.web3.foundation/en/latest/polkadot/block-production/Babe.html), or Blind Assignment for Blockchain Extension. Deterministic finality is produced through a classical BFT agreement protocol called [GRANDPA](https://arxiv.org/abs/2007.01560), or HOST-based Recursive Ancestor Deriving Prefix Agreement), which depends on ⅓ honest validator assumption.

## Genesis Block

The genesis block contained the initial state of the blockchain, which primarily concerned the initial distribution of [account balances](../usdjoy.md#genesis-block) and initial state variables for various subsystems, please consult description of each subsystem to find each such initial value, but be aware that subsequent transactions may have altered them.



* chain specification? this concept needs to be explained here...@
* WebAssembly or native Rust\


```
/// This runtime version.
#[sp_version::runtime_version]
pub const VERSION: RuntimeVersion = RuntimeVersion {
    spec_name: create_runtime_str!("joystream-node"),
    impl_name: create_runtime_str!("joystream-node"),
    authoring_version: 12,
    spec_version: 1001,
    impl_version: 0,
    apis: crate::runtime_api::EXPORTED_RUNTIME_API_VERSIONS,
    transaction_version: 1,
    state_version: 1,
};
```

## Boot Nodes

`TODO`

## Forkless Upgrades

The Joystream blockchain takes advantage of a core feature of Substrate, which is that runtime itself - as an executable WebAssembly state machine, is held in the state of the chain. This awareness of the underlying state transition function allows for the blockchain to update it's own runtime on the fly, based on it's on domain specific rules. In Joystream this can be triggered by a [runtime upgrade proposal](proposal-system.md#runtime-upgrade) being passed by the council. This has the benefit of providing a binding and transparent mechanism by which the rules of the protocol change, reducing the risk of permanent forks either due to contention or simple human coordination failures in the upgrade deployment itself.

Here is a running list of upgrades that have taken place.

| Network | Deployed        | Runtime\*                                                                                 |
| ------- | --------------- | ----------------------------------------------------------------------------------------- |
| Ephesus | ETA: 7th April  | <pre><code>b0b35055b27a00c6a6be9c287049c79a9060e923c268de4ba148badcd435c184
</code></pre> |

_\* blake2-256 hash of runtime WASM object._

## Resource Accounting & Fees

### Resources

There are three scarce resources which are accounted for when pricing transactional use of the blockchain

* **Block space:** the size of the transaction in a block.
* **Weight:** the worst-case case compute time for the transaction on reference hardware.
* **State:** the added size to the state of the blockchain after the transaction.

TODO: what is reference hardware.

### Reference Hardware

TODO add specification + link



The transaction weights in Polkadot are benchmarked on reference hardware. We ran the benchmark on VM instances of two major cloud providers: Google Cloud Platform (GCP) and Amazon Web Services (AWS). To be specific, we used `c2d-highcpu-8` VM instance on GCP and `c6id.2xlarge` on AWS. It is recommended that the hardware used to run the validators at least matches the specs of the reference hardware in order to ensure they are able to process all blocks in time. If you use subpar hardware you will possibly run into performance issues, get less era points, and potentially even get slashed.

Not hard requirements, but best practice.... used to generate fees



| Resource | Requirements                                                                                                                                                                                                                                                                                                             |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| CPU      | <ul><li>Prefer single-threaded performance over higher cores count.</li><li>Simultaneous multithreading disabled (Hyper-Threading on Intel, SMT on AMD)</li><li>4 physical cores @ 3.4GHz</li><li>Intel Ice Lake, or newer (Xeon or Core series); AMD Zen3, or newer (EPYC or Ryzen)</li><li>x86-64 compatible</li></ul> |
| Storage  | An NVMe SSD of 1 TB (As it should be reasonably sized to deal with blockchain growth).  In general, the latency is more important than the throughput.                                                                                                                                                                   |
| Memory   | 16GB DDR4 ECC.                                                                                                                                                                                                                                                                                                           |
| System   | Linux Kernel 5.16 or newer.                                                                                                                                                                                                                                                                                              |
| Network  | The minimum symmetric networking speed is set to 500 Mbit/s (= 62.5 MB/s).                                                                                                                                                                                                                                               |

### Fees

In a distributed system, a user can require nodes to perform costly computation. Depending on the design of the system, the compute may be a one time event, or it may need to be replicated by multiple parties when they attempt to validate the integrity of the system. Regardless, this ability to command the compute resources of system participants means that some mechanism is needed to restrict and ration access to such resources. In blockchain systems specifically, access is intended to be open and permissionless, hence paying for access is has been considered the most neutral solution to this problem. Fees associated with inclusion of transactions in the blockchain plays the role of such payments in blockchains.



include point about dynamic adjustment

## Parameters

Here are the most important blockchain level parameters.

| Concept           | Reference Codebase Token | Value |
| ----------------- | ------------------------ | ----- |
| Target block time |                          |       |
| Max block space   |                          |       |
| Max block weight  |                          |       |

_Warning: There is always a risk of such table values going stale, so only use these as baseline references, and any_&#x20;

* target block time: 6s
* block sapce
* weight to fee
* byte to fee
*
* max weight
* Curent runtime version (as of 2011) [https://docs.substrate.io/build/chain-spec/](https://docs.substrate.io/build/chain-spec/)
* Substrate version (as of)
