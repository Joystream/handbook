---
description: Outlining the roll out phases for the Carthage testnet, and later the mainnet!
coverY: 0
---

# 🧻 Carthage Rollout Plan

## Executive Summary

The launch of the final joystream testnet - `Carthage`, intended as the final test of the runtime and our intended deployment plan for the Joystream mainnet, will be rolled out as outlined in the table below:

| ID | Stage (Runtime) | Duration | Sudo                        | Consensus | Calls Allowed                                                                                         | Main Jsgenesis Actions                  | Staking Rewarded | #Validators |
| -- | --------------- | -------- | --------------------------- | --------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------- | ---------------- | ----------- |
| 1  | **Frozen**      | \~24h    | <p>Yes <br>(Single Key)</p> | PoA       | <p><code>sudo,</code><br><code>staking,</code><br><code>session,</code><br><code>multisig*</code></p> | <p>Bootstrap <br>-> Thawn</p>           | No               | 9-12        |
| 2  | **Thawn**       | \~6days  | <p>Yes<br>(Multisig)</p>    | PoS       | <p><code>sudo,</code><br><code>staking,</code><br><code>session,</code><br><code>multisig*</code></p> | <p>Set #Validators<br>-> Supervised</p> | Yes              | 12-24       |
| 3  | **Supervised**  | Weeks    | <p>Yes<br>(Multisig)</p>    | PoS       | Everything`**`                                                                                        | <p>Set #Validators<br>-> Liberated</p>  | Yes              | 12-?        |
| 4  | **Liberated**   | NA       | No                          | PoS       | Everything`**`                                                                                        | NA                                      | Yes              | NA          |

* `*` All transaction related to the `sudo`, `staking`, `session` and `multisig` modules will not be filtered, regardless of origin. This means:
  * Prospective validators and nominators can prepare and configure their validator (on chain), and/or nominate. There will be no changes to the actual set however during the `Frozen` stage.
  * Any `multisig` transactions can be initiated and approved, but the actual call will be filtered unless the call is:
    * `sudo.*`
    * `staking.*`
    * `session.*`
  * Although any `sudo.*` will get through the filter, unless the caller of the extrinsic is actually `sudo`, the transaction will, of course, still fail.
* `**` Some filters will still apply, but they are only applied to certain features that are in the runtime, but not properly integrated. The main example being the `bounty` module.
