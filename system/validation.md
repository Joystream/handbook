---
description: Maintaining agreement over the growing history of the system.
---

# 🏭 Validation

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

## Validator

### Responsibilities

* Run and maintain screening nodes that are always available and performant
* Help enforce the consensus rules of the network

### Requirements

* Experienced with how to setup and maintain high performance IT infrastructure
* Access to highly performant and reliable IT infrastructure, with high storage, (up & down) bandwidth and processing capacity
* Able to securely store keys
* Hold sufficient amount of the native platform token to put at stake

## Guides

The instructions below cover Linux binaries only. If you want to build from source, clone the [repo](https://github.com/Joystream/joystream) and follow the build steps there.

### Install and Deploy

* Every time something is written in `<brackets>`, this means you have to replace this with your input, without the `<>`.
* When something is written in `"double_quotes"`, it means the number/data will vary depending on your node or the current state of the blockchain.
* For terminal commands:
  * `$` means you must type what comes afterwards
  * `#` means it's just a comment/explanation for the readers convenience

```
# This is just a comment, don't type or paste it in your terminal!
$ cd ~/
# Only type/paste the "cd ~/, not the preceding $ !
```

For the purposes of simplicity, we will assume:

1. You are user `joystream`, with sudo priveliges.
2. You want to save everything in `/home/joystream/bin/`

#### Download Node Binary

Find the latest release [here](https://github.com/Joystream/joystream/releases/latest) or get the tag from the command line with:

```
$ curl -sL https://api.github.com/repos/Joystream/joystream/releases/latest | jq -r ".tag_name"
```

At the time of writing, the latest release is `v11.3.0` a.k.a. Carthage, the latest and last testnet before mainnet.

```
# Create the directory, and go there
$ mkdir ~/bin && cd ~/bin

# Assuming the latest version is still v11.3.0
$ curl -sL https://api.github.com/repos/Joystream/joystream/releases/latest | jq -r ".tag_name"

# Download the binary:
$ wget https://github.com/Joystream/joystream/releases/download/v11.3.0/joystream-node-7.4.1-d2243721017-x86_64-linux-gnu.tar.gz

# unzip it:
$ tar -vxf joystream-node-7.4.1-d2243721017-x86_64-linux-gnu.tar.gz

# Download the chain spec:
$ wget https://github.com/Joystream/joystream/releases/download/v11.3.0/joy-testnet-7-carthage.json

# test that your node works:
$ ./joystream-node --chain-spec joy-testnet-7.json --pruning archive
```

Assuming it starts syncing, you can stop it right away with `ctrl+c`

#### Configuration

The node lets you set a variety of option flags. You can display them all with `./joystream-node --help` Some basic `options` you should enable or consider:

> \--chain \<CHAIN\_SPEC>
>
> Specify the chain specification. It can be one of the predefined ones (dev, local, or staging) or it can be a path to a file with the chainspec (such as one exported by the `build-spec` subcommand).

* **Required**
  * Without this flag, you will not connect the chain.

> \--pruning \<PRUNING\_MODE>
>
> Specify the state pruning mode, a number of blocks to keep or 'archive'. Default is to keep all block states if the node is running as a validator (i.e. 'archive'), otherwise state is only kept for the last 256 blocks.

* **Required for validators**
  * If you want to be a validator, the node must run with `--pruning archive`
  * If you start syncing without that flag enabled, you will have to wipe your node and sync again if you change your mind.

> \--validator
>
> Enable validator mode. The node will be started with the authority role and actively participate in any consensus task that it can (e.g. depending on availability of local keys).

* **Required for validators**
  * Unlike with `--pruning`, it only has to be set when you are actually in the validator set to have an effect, so you don't have to re-sync if you forget while syncing.

> \--name
>
> The human-readable name for this node. The node name will be reported to the telemetry server, if enabled.

* **Optional**
  * May serve some benefits if you want someone to nominate you, but may make it easier to identity you.

***

As a validator, you should (as a bare minimum) be very restrictive in terms of RPC access to your node. Go through the options, and double check that the defaults are in line with your preferences and risk tolerance.

#### Run as a Service

Running as a service means that the node will continue running as a daemon, and you can enable it to restart in case of crashes and on reboot.

It requires sudo privileges. If you are not user `root`, add `sudo` before commands.

Example file below, with essentials only:

```
[Unit]
Description=Joystream Node
After=network.target

[Service]
Type=simple
User=joystream
WorkingDirectory=/home/joystream/bin/
ExecStart=/home/joystream/bin/joystream-node \
        --chain /home/joystream/bin/joy-testnet-7.json \
        --pruning archive \
        --validator
Restart=on-failure
RestartSec=3
LimitNOFILE=10000

[Install]
WantedBy=multi-user.target
```

```
# Create/open a file with your favorite editor (I use nano below)
$ sudo nano /etc/systemd/system/joystream-node.service

# Paste in the example file above, and do "ctrl+x", then "y" and "return" to save

# start it up:
$ sudo systemctl start joystream-node

# check that it's working:
$ sudo systemctl status joystream-node
# For a brief status, OR
$ sudo journalctl -f -n 100 -u joystream-node
# To monitor the log

# If you are happy, enable it so it will start automatically on boot:
$ sudo systemctl enable joystream-node
```

### Setup Keys and Validate

With your validator node up and running, you are now ready to set up keys and announce your intentions on chain.

#### Generate Session Keys

In the terminal on your node (will only work if you are on running the chain on the same machine!):

```
$ curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933

# Which should return:
{"jsonrpc":"2.0","result":"0xabc...123","id":1}
```

Where `0xabc...123` (a much longer string in reality) is a concatenation of four public keys hex-encoded. The private keys should have been injected in your `base-path`. Make sure you copy this string over somewhere, as you need it later.

Assuming you only did this once (while running this _this_ chain), and you didn't set a different `--base-path` flag:

```
# On the current network, replace <chain-name> with joy_testnet_7
$ ls -a ~/.local/share/joystream-node/chains/<chain-name>/keystore

# Which should return 4 files, each a long string starting with a 6.

# You can confirm more precisely by:

$ curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_hasSessionKeys", "params":["0xabc...123"]}' http://localhost:9933

# Which, if you have the corresponding ready to sign, should return:
{"jsonrpc":"2.0","result":true,"id":1}
```

**Warning:**

* It's both bad practice, and a possible slashing risk, to keep multiple set of session keys on one node. If you wanted to try the command, made a mistake, or for whatever reason want to switch them, delete them. If you have had set them on chain (see next steps), you can change them before you get into the validator set.
* Keeping the same set of keys, on multiple nodes, all running with the `--validator` enabled, will cause a slash. A good backup system could include backup nodes, but be careful. It's better to get "booted" for an era than to double sign blocks. It will be treated as an attack even if just by accident.

#### Configure Validator on Chain

For the time being, we will only show how to do this with [Polkadot{.js} apps](https://polkadot.js.org/apps/#/explorer). As this serves lots of projects in the substrate ecosystem, you have to set an endpoint. This can be done by [this](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.joystream.org%3A9944#/explorer) link, which connects to the current "default" Joystream endpoint, or by clicking the with a logo, project/network name and block height in the top left corner.

<figure><img src="../.gitbook/assets/endpoint.png" alt=""><figcaption></figcaption></figure>

**With Polkadot-js**

You need two keys for this, one to be the `controller` and one as the `stash`. The latter holds the stake and must sign at least once to "delegate" to the `controller` which is running the "day to day" operations.

Assuming you are fully synched, and your node is running:

**Steps:**

1. Go to the "staking actions" tab - "Network" -> "Staking" -> "Accounts", and click the "+ Validator" button in the top right corner.
2. Select a `stash` and `controller` account from the dropdown, set the "value bonded" as the amount you want to stake, and choose a "payment destination", then hit "next".
3. Paste in the public session keys (`0xabc...123`), choose a "reward commission percentage" and whether you want to allow nominations or not, then click "Bond & Validate".

If you are preparing this for later, click the "+ Stash" button instead. This allows you to wait for your session keys and/or synching your node.

**With joystream-cli**

`TODO`

#### Being a Validator

Assuming the transaction went through, you will now appear under the "waiting" tab [here](https://polkadot.js.org/apps/#/staking). That means you are in the queue for joining the validator set, but when (and whether) you actually join depends on the competition for getting a slot.

At all times, there is a limit to how many can become validators. What that number is set by the council. The current value can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "validatorCount".

Suppose that number is `n`, and that there are `m` validators that, towards the end of each `era` were already validating or joined the queue:

* If `n >= m`, all will be elected
* If `n<m`, the `n` validators with the highest **total active stake** will be elected for the upcoming `era`

_Notes:_

* An `era` lasts \~6h.
* **total active stake** refers to the active stake for the validator itself, plus all of their nominators.

**Transaction Rejected**

There is a minimum threshold of funds required to stake as a validator. As you can get slashed, that means you can not "re-use" tokens that are staked for other "slashable" purposes, such as role stake.

That number can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "minValidatorBond". (In base value `HAPI`, meaning `1*10^-10 JOY`)

Another reason the transaction can be rejected is if the maximum number of `bonded` accounts have declared as validators. That number can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "maxValidatorsCount". How many there are currently can be found in the [chain state](https://polkadot.js.org/apps/#/chainstate) -> "staking" -> "counterForValidators".

There are of course a limitless amount of other reasons the transaction could be rejected if you constructed it yourself in the cli.

### Advanced Setup

`TODO`

##
