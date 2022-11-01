---
description: Outlining the launch phases for the Carthage testnet and mainnet.
---

# 🧨 Launch Process

## Introduction

Launching a new blockchain secured by a new PoS validator set, which comes to consensus using a time sensitive BFT protocol, is a vulnerable process which easily can end up with liveness failure as a result of networking or operational malfunctioning. For this reason, it should be happen in a gradual process, starting very centralised  and small, and opening up to a broader set of stakeholders while block production is monitored. It also has to be a fair process which does not bias in favor of early or arbitrary participants. Lastly, there must be some room for small scale coordination to handle any unforunforeseenseen catastrophic errors which may occur early, and with minimal if any side-effects. The process for launching the Joystream blockchain was designed based on these requirements.

## Carthage and Mainnet

This process will be used for the upcoming launch of the `Carthage`  network, where runtime is feature frozen - and genesis block is largely locked in, and only unforseen circumstances will result in further changes to the process described herein.

## Overview

The launch of the final joystream testnet - `Carthage`, intended as the final test of the runtime and our intended deployment plan for the Joystream mainnet, will be rolled out as outlined in the table below:

| Stage (Runtime) | Duration | Sudo                        | Consensus | Calls Allowed                                                                                         | Main Jsgenesis Actions                  | Staking Rewarded | #Validators |
| --------------- | -------- | --------------------------- | --------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------- | ---------------- | ----------- |
| **Frozen**      | \~24h    | <p>Yes <br>(Single Key)</p> | PoA       | <p><code>sudo,</code><br><code>staking,</code><br><code>session,</code><br><code>multisig*</code></p> | <p>Bootstrap <br>-> Thawn</p>           | No               | 9-12        |
| **Thawn**       | \~6days  | <p>Yes<br>(Multisig)</p>    | PoS       | <p><code>sudo,</code><br><code>staking,</code><br><code>session,</code><br><code>multisig*</code></p> | <p>Set #Validators<br>-> Supervised</p> | Yes              | 12-24       |
| **Supervised**  | Weeks    | <p>Yes<br>(Multisig)</p>    | PoS       | Everything`**`                                                                                        | <p>Set #Validators<br>-> Liberated</p>  | Yes              | 12-?        |
| **Liberated**   | NA       | No                          | PoS       | Everything`**`                                                                                        | NA                                      | Yes              | NA          |

* `*` All transaction related to the `sudo`, `staking`, `session` and `multisig` modules will not be filtered, regardless of origin. This means:
  * Prospective validators and nominators can prepare and configure their validator (on chain), and/or nominate. There will be no changes to the actual set however during the `Frozen` stage.
  * Any `multisig` transactions can be initiated and approved, but the actual call will be filtered unless the call is:
    * `sudo.*`
    * `staking.*`
    * `session.*`
  * Although any `sudo.*` will get through the filter, unless the caller of the extrinsic is actually `sudo`, the transaction will, of course, still fail.
* `**` Some filters will still apply, but they are only applied to certain features that are in the runtime, but not properly integrated. The main example being the `bounty` module.
