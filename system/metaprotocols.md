---
description: We are all just here for transaction ordering, the rest is gravy.
---

# 🪐 Metaprotocols

## Introduction

The fundamental service of a any consensus system is to maintain and build a transaction ordering, whether it is a blockchain or anything else. Once transactions are ordered, one can trivially establish consensus about any higher level abstraction, such as a token, exchange, registry or anything else. In all blockchains, the native L1 transactions carry some minimal amount of semantics that are also validated by the validator enforced consensus rules, for example rules for creation, transfer, locking and destruction of the native asset (BTC, ETH, .etc), as this is needed to generate the game theoretic incentives for validators/miners to participate at all. Beyond this, some systems have very rich validator in state machines, like the EVM, while others do nothing else, like Bitcoin (more or less). In both systems however, one can build arbitrarily complex consensus state machines on top by simply overloading raw data fields in the native transactions, such as `calldata` in the EVM, or `OP_RETURN` in Bitcoin. There are many examples of this, such as

* **Counterparty:** an asset protocol on top of Bitcoin which actually implemented the [EVM on top of Bitcoin before Ethereum was aout](https://counterparty.io/news/counterpartys-evm-port-moves-forward/).
* **Omni:** an asset protocol on top of Bitcoin which was the foundation of the Tether system for a long time.
* **Blockstack:** a namespace protocol on top of Bitcoin.
* **Colored Coin:** another very old asset protocol on top of Bitcoin.

These systems all work by having a separate group of indexing nodes that can identify the embedded transactions in the blockchain, and understand their semantics, so as to allow these nodes to build and maintain a separate state machine.

These embedded consensus systems are often referred to as _metaprotocols_.

The computational load of the metaprotocol computation load on those nodes can even be charged using the normal transactional fee system of the blockchain, by having the metaprotocol require extra tip to be added above and beyond the base fee of the on-chain transaction itself in order to process the transaction and incurr the computational cost.&#x20;

## Benefits and Limits

There are a number of benefits to such metaprotocols

* Third party developers can innovate in a permissionless way, requiring buyin from community to upgrade consensus rules.
* Additional state can be introduced which can be ignored by most, or al, of the other system participants. This allows for introduction of transaction and migration computations that violate upper compute capability bounds on validators, which typically exist to ensure decentralization.
* Failures, or bugs, are less costly to remedy.
* Separate, or no, resource accounting. There is substantial complexity assocaited with managing both state bloat and transaction processing time natively.

## Usage

There are a range of different metaprotocols in use in Joystream, documentation will need to be enhanced on this in the future, hence for now the most useful reference will just be the message definitions in the monorepo.

{% embed url="https://github.com/Joystream/joystream/tree/master/metadata-protobuf" %}
