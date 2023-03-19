---
description: We are all just here for transaction ordering, the rest is gravy.
---

# 🪐 Metaprotocols

## Introduction

It has long been known that using an existing blockchain purely as a transaction ordering infrastructure can allow third party developers to innovate in a permissionless way, without requiring buyin from community to upgrade consensus rules, but also to introduce computational primitives that are not constrained by the compute resources requirements for validators ... allow people to ignore.. complex resource accounting sidestep

## Metaprotocols

The fundamental service of a any consensus system is to maintain and build a transaction ordering, whether it is a blockchain or anything else. Once transactions are ordered, one can build consensus about any higher level abstraction, such as a token, exchange, registry or anything else. In all blockchains, the transactions carry some minimal amount of semantics that are also validated by the validator enforced consensus rules, for example rules for creation, transfer, locking and destruction of the native asset (BTC, ETH, .etc), as this is needed to generate the game theoretic incentives for validators/miners to participate at all. Beyond this, some systems have very rich validator in state machines, like the EVM, while others do nothing else, like Bitcoin (more or less). In both systems however, one can build arbitrarily complex consensus state machines on top by simply overloading raw data fields in the native transactions, such as `calldata` in the EVM, or `OP_RETURN` in Bitcoin. There are many examples of this, such as

* **Counterparty:** an asset protocol on top of Bitcoin which actually implemented the [EVM on top of Bitcoin before Ethereum was aout](https://counterparty.io/news/counterpartys-evm-port-moves-forward/).
* **Omni:** an asset protocol on top of Bitcoin which was the foundation of the Tether system for a long time.
* **Blockstack:** a namespace protocol on top of Bitcoin.
* **Colored Coin:** another very old asset protocol on top of Bitcoin.

These systems all work by having a separate group of indexing nodes that can identify the embedded transactions in the blockchain, and understand their semantics, so as to allow these nodes to build and maintain a separate state machine.

These embedded consensus systems are often referred to as _metaprotocols_.

The computational load of the metaprotocol computation load on those nodes can even be charged using the normal transactional fee system of the blockchain, by having the metaprotocol require extra tip to be added above and beyond the base fee of the on-chain transaction itself in order to process the transaction and incurr the computational cost. Those nodes would however not receive those fees themselves, but it would deter denial of service attacks.

## Limitations

The main limitation of metaprotocols is that this state cannot impact the ownership of the built in state machine, and thus most importantly, they cannot impact the ownership of the native asset. Here are examples of parts of the current Joystream system which to which this could clearly apply:

* The forum.
* The council blog.
* Proposal discussion threads.
* The content directory: here there may be some nuances depending on which part of the content directory one bares in mind, and with what functionality, but certainly the fundamental parts like videos, playlists, metadata on these and channels.

In all of these examples, the state of the given subsystem is never read by any other transaction which updates the JOY allocation in any way. It also is the case that for all the examples listed above, none could indeed impact the rules governing the Bitcoin UTXO set.

**Another limitation is that its no possible to provide light client proofs for this part of the state.**

## Benefits

The question then becomes: what are the benefits of this vs. having everything built in to the native runtime or smart contracts, so that they are fully validated by validators.

The main original motivation for these systems have been because the someone wanted to build a distributed state machine, but required a level of security around this system which was not considered easy to guarantee. In these cases, piggy backing on the secure ledger of a major existing system became an attractive option.

This reason is far less relevant to us building a new chain where we have control of the feature set.

### 1. Looser Validation Constraints

Unlike the native validation, the metaprotocol validation does not need to be done as part of a time sensitive interaction between nodes. Since each metaprotocol node validates on its own on top of a pre-existing transaction ordering, it does not need to interact with any other metaprocol nodes. This lack of need for any kind of synchrony in the processing of the node means that its not a serious problem if some validation computations take a bit longer, or take more time on certain low-end node hardware. The validation can also occur in a less constrained tooling environment, so you can depend on the optimized performance of relational databases and other tooling of choice which is much more powerful than the EVM or the Substrate Runtime Environment.

Both of these together affor greater flexibility in expressing the sort of state machine you are interested in than what is convenient natively.

Examples

1. Delete all channels created the last two weeks.
2. Compute the average number of videos per channel.

### 2. Reduced Cost of Upgrades

While we may know the initial features we want to ship, we also know that it will need to change, and in some respects ideally very often, hence the issue of the costs of changes still remain.

The activity of upgrading a state machine involves a mix of the following

1. Dropping existing transactions.
2. Introducing new transaction.
3. Migrating state.

Changing a transaction in any way can just be understood as 1+2. These changes obviously have knock-on effects, and possible migrations, in query infrastructure and other tooling.

These points apply both to native validation and to metaprotocols. There is however a clear difference in cost across the two. For native Substrate modules, doing any upgrade at all is risky, even if it only includes 1 and 2. The smallest change still requires an entirely new runtime to be deployed, and the scope for mistake is largely unconstrained. Doing 3 is obviously also no less difficult in this case. For smart contracts 1 and 2 are not so bad, but 3 is still very difficult and risky, in particular as the system evolves and accumulates migration related technical debt. Contrast this with metaprotocol nodes, where 1 and 2 are trivial, arguably easier than the smart contract case, as it does not even require understanding Solidity - a relatively unfamiliar and quirky language. Doing 3 is substantially easier, not lest because of the loser computational constraints described in the prior section, and there is considerable tooling and best practices established for how to do migration and updates of such classical database systems.

This amounts to a substantial difference in costs and risks.

### 3. No state bonds

State bonds are needed for any object placed in storage, this is because otherwise will lead to deliberate, or just careless, growth in the blockchain storage over time. This means that running a full node, or validator, becomes increasingly costly over time, and there is no way to prune storage state, unlike ledger history. This ultimately results in centralization in the network infrastructure. For this reason, state bloat bonds are added to all state objects which do not innately have them, this would for example be the case for representations of forum threads, posts, and similar objects in content directory or proposal system. However, such bonds are complex to manage in the runtime, see here

https://github.com/Joystream/joystream/issues/2545

and extremely confusing for users, let alone adding to transaction fees users must pay. Lifting such represetnations out of full node storage, and into query infrastructure storage, one is able to avoid the need for such bonds. These representations no longer make full node state heavy. It does of course make query node state heavy, however these are not consensus nodes, and each query node is free to process, or not process, these features. If someon wants to process and represent this state, for example to power forum like product, only they need to pay this cost. It also makes the experience infinitely better for users.
