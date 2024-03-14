---
description: The centerpiece of the Joystream Network
---

# ⛓ Blockchain

## Introduction

At the heart of the Joystream Network sits a content, social, governance and asset ledger that coordinates the activity of all consumers, service providers, creators and applications.

## Overview

The blockchain is a standalone L1 blockchain with it's own independent validator set. Currently, there is only a single reference implementation, which is written in Rust, and is based on the [Substrate](https://docs.substrate.io/) blockchain development framework. This means that the consensus and networking logic have already been implemented, and the community can focus on the domain specific state machine which is core to Joystream. This is also written in Rust, and this state machine - called the _Runtime_, runs in a [WebAssembly](https://en.wikipedia.org/wiki/WebAssembly) execution environment. _While it is possible to incorporate a smart contract environment, like the_ [_EVM_](https://substrate-developer-hub.github.io/docs/en/knowledgebase/smart-contracts/evm-pallet)_, that is currently not part of the Joystream runtime._ The architecture of a Joystream validator node is shown below.

<figure><img src="../.gitbook/assets/Substrate node.svg" alt=""><figcaption><p>Overview of Joystream node architecture, built on Substrate.</p></figcaption></figure>

## Consensus

Validators are selected based on [Nominated PoS](https://arxiv.org/abs/2004.12990), and block production occurs in a slot-based stochastic block authoring schedule called [BABE](https://research.web3.foundation/en/latest/polkadot/block-production/Babe.html), or Blind Assignment for Blockchain Extension. Deterministic finality is produced through a classical BFT agreement protocol called [GRANDPA](https://arxiv.org/abs/2007.01560), or HOST-based Recursive Ancestor Deriving Prefix Agreement), which depends on ⅓ honest validator assumption.

## **Accounts and Digital Signature Schemes**

Accounts are identifiers under which transactions, for example for disposing of owned assets, can be issued. There are two kinds of accounts in the system. There are the _normal accounts_ for which some known digital signature key pair is the credential used to authenticate transactions. The signature scheme used in Joystream is Sr25519, based on the Schnorrkel variant that uses Schnorr signatures with Ristretto point compression. Then there are _keyless accounts_, which are only meant to hold assets, in particular the native asset $JOY, but which are not owned by any key pair. They are also sometimes referred to as _module accounts_. They are loosely analogous to smart contract accounts in the EVM context, and some examples are.

## Genesis Block

The genesis block was the first block, which contained no user transactions, and had a block hash of `6b5e488e0fa8f9821110d5c13f4c468abcd43ce5e297e62b34c53c3346465956`. It contained the initial state of the blockchain, which primarily concerned&#x20;

* the initial distribution of [account balances](../usdjoy.md#genesis-block) and initial state variables for various subsystems, please consult description of each subsystem to find each such initial value, but be aware that subsequent transactions may have altered them.
* the initial WebAssembly runtime.

## Boot Nodes

When starting a new full node, it needs to fetch all the data in the canonical chain, and this requires an initial list of nodes, called the _boot notes_, from which to download this data.. After initially connecting to the peer-to-peer network, a node will learn about additional nodes which can be used on next boot process after a possible session interruption.

## Execution Strategy

Using the WebAssembly runtime is important because the WebAssembly and native runtimes can diverge. For example, if you make changes to the runtime, you must generate a new WebAssembly blob and update the chain to use the new version of the WebAssembly runtime. After the update, the WebAssembly runtime differs from the native runtime. To account for this difference, all of the execution strategies treat the WebAssembly representation of the runtime as the canonical runtime. If the native runtime and the WebAssembly runtime versions are different, the WebAssembly runtime is always selected. A full-node will not attempt to use its native runtime in substitute for the on-chain Wasm runtime unless all of `spec_name`, `spec_version` and `authoring_version` are the same between `RuntimeVersion` in Wasm and native. `authoring_version` is the version of the authorship interface. An authoring node will not attempt to author blocks unless this is equal to its native runtime.

## WebAssembly Execution Environment <a href="#webassembly-execution-environment" id="webassembly-execution-environment"></a>

The WebAssembly execution environment can be more restrictive than the Rust execution environment. For example, the WebAssembly execution environment is a 32-bit architecture with a maximum 4GB of memory.

## Forkless Upgrades

The Joystream blockchain takes advantage of a core feature of Substrate, which is that runtime itself - as an executable WebAssembly state machine, is held in the state of the chain. This awareness of the underlying state transition function allows for the blockchain to update it's own runtime on the fly, based on it's on domain specific rules. In Joystream this can be triggered by a [runtime upgrade proposal](proposal-system.md#runtime-upgrade) being passed by the council. This has the benefit of providing a binding and transparent mechanism by which the rules of the protocol change, reducing the risk of permanent forks either due to contention or simple human coordination failures in the upgrade deployment itself.

Here is a running list of upgrades that have taken place.

<table><thead><tr><th width="143.33333333333331">Network</th><th>Deployed</th><th>Runtime*</th><th>spec_version**</th></tr></thead><tbody>
<tr><td>Mainnet</td><td>Friday at 9:07:42 PM CET December the 9th, 2022</td><td><code>1a1d11d2cc214edb180fd861826a9450df1acc650226db604d96f489f0a36f8f</code></td><td>1000</td></tr>
<tr><td>Ephesus</td><td>Wednesday at 9:47:12 AM CET April 12th, 2023 </td><td><code>b0b35055b27a00c6a6be9c287049c79a9060e923c268de4ba148badcd435c184</code></td><td>1001</td></tr>
<tr><td>Nara</td><td>Wednesday at 14:06:54 AM CET March 13th, 2024 </td><td><code>c3dda36a68353b12c57263ee101964b6ea80dadefa4a3d1e67903df7cae064c0</code></td><td>2002</td></tr>
</tbody></table>

_\* blake2-256 hash of runtime WASM runtime._\
_\*\* Version of the runtime specification, must be distinct for each runtime for a chain. Is involved in execution strategy and also transactions commit to this version to avoid unintended semantic changes from time of signing to time of block inclusion._

## Resource Accounting & Fees

Resource accounting is the activity of anticipating the computational resources consumed by an impending transaction or other execution trigger, such as a runtime upgrade or a block pre- or post-processing hook. The purpose of such accounting is to constrain overall consumption within blocks, so as to preserve decentralization by bounding node operational cost, and also to use as input for setting fees for pricing user transactions, which itself both funds overall consensus security budget and deters denial-of-service attacks.

### Resources

There are three scarce resources which are accounted for when pricing transactional use of the blockchain

* **Block space:** The size of the transaction in a block.
* **Weight:** Unit of compute time, specifically 1 picosecond of compute time on a reference machine. The weight of a transaction is the worst case total weight of executing it, and the process of determining how to efficiently forecast the _weight function_, i.e. the weight estimator for a concrete invocation of a given transaction, is called _benchmarking_, and is done by blockchain engineers when writing runtime and node code.
* **State:** The added size to the state of the blockchain after the transaction.

### Reference Hardware

The estimation of the weights, which is the time needed to perform various computations, is done on some reference hardware specification. Having such a specification also provides constraints for what validators should adhere to in order to process the chain in a timely manner, otherwise one can earn less era points, and potentially even get slashed.

The benchmarking is currently done on VM instances of two major cloud providers: Google Cloud Platform (GCP) and Amazon Web Services (AWS). To be specific, we used `c2d-highcpu-8` VM instance on GCP and `c6id.2xlarge` on AWS. A detailed specification is provided below.

<table><thead><tr><th width="135">Resource</th><th>Requirements</th></tr></thead><tbody><tr><td>CPU</td><td><ul><li>Prefer single-threaded performance over higher cores count.</li><li>Simultaneous multithreading disabled (Hyper-Threading on Intel, SMT on AMD)</li><li>4 physical cores @ 3.4GHz</li><li>Intel Ice Lake, or newer (Xeon or Core series); AMD Zen3, or newer (EPYC or Ryzen)</li><li>x86-64 compatible</li></ul></td></tr><tr><td>Storage</td><td>An NVMe SSD of 1 TB (As it should be reasonably sized to deal with blockchain growth).  In general, the latency is more important than the throughput.</td></tr><tr><td>Memory</td><td>16GB DDR4 ECC.</td></tr><tr><td>System</td><td>Linux Kernel 5.16 or newer.</td></tr><tr><td>Network</td><td>The minimum symmetric networking speed is set to 500 Mbit/s (= 62.5 MB/s).</td></tr></tbody></table>

### Fees

In a distributed system, a user can require nodes to perform costly computation. Depending on the design of the system, the compute may be a one time event, or it may need to be replicated by multiple parties when they attempt to validate the integrity of the system. Regardless, this ability to command the compute resources of system participants means that some mechanism is needed to restrict and ration access to such resources. In blockchain systems specifically, access is intended to be open and permissionless, hence paying for access is has been considered the most neutral solution to this problem. Fees associated with inclusion of transactions in the blockchain plays the role of such payments in blockchains.

In Joystream, fees are burned, except an extra user specifiable tip, which goes to the block producer, so as to facilitate a fee market. For a detailed explanation of how fees are derived, please consult the link below.

{% embed url="https://docs.substrate.io/build/tx-weights-fees/#how-fees-are-calculated" %}
Fee calculation in Substrate chains.
{% endembed %}

## Parameters

Here are the most important blockchain level parameters.

<table><thead><tr><th width="286.3333333333333">Concept</th><th>Reference Codebase Token</th><th>Value</th></tr></thead><tbody><tr><td>Target block time</td><td><code>ExpectedBlockTime</code></td><td>6 seconds</td></tr><tr><td>Max block space</td><td><code>MaximumBlockLength</code></td><td>5 MB</td></tr><tr><td>Max block weight (normal)</td><td><code>RuntimeBlockWeights</code></td><td>75% of 2s of weight</td></tr><tr><td>Max block weight (operational)</td><td><code>RuntimeBlockWeights</code></td><td>25% of 2s of weight</td></tr><tr><td>Weight to fee function</td><td><code>WeightToFee</code></td><td><a href="https://github.com/Joystream/joystream/blob/master/runtime/src/constants.rs#L106">Link</a></td></tr></tbody></table>

_Warning: There is always a risk of such a table of values going stale, so only use these as baseline references, and consult reference implementation for the relevant runtime._
