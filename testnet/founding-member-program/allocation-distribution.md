---
description: How tokens may be distributed across multiple accounts
---

# Allocation Distribution

When thinking about how token allocations "should" be distributed across accounts, there are some aspects to consider.

Some of these are general, and should be in the back of the mind of anyone seasoned in crypto, whereas others are somewhat Joystream specific.

#### Reputation or Anonymity

For Founding Members especially, their reputation is tied to their membership. Although someone may claim the same, or a similar handle, your account and FM badge can not be copied.

Still, there reasons one should avoid putting all your tokens in your membership root address. One is that you can not act anonymously, if you so wish.

#### The Complexity of Security

Keeping all your eggs in one basket makes the risk of losing that key or getting hacked extra concerning. A derivation of the same seed, for example with a passphrase, reduces the risk that a hack means all your keys are gone, but for loss, it does nothing.

On the other hand, distributing funds across ten 6 of 6 multisig accounts, all with unique seeds generated offline, and etched into metal disks buried across the globe, may virtually remove any risk of getting hacked, but you will cause loss of funds.

#### Active Participation vs HODLing

Although the main purpose of the Founding Member program was, and is, to source and train a community that are capable and incentivized to run infrastructure, operate roles, allocate resources and improve the platform, we expect some fraction of tokens to into cold storage.&#x20;

In addition to choosing a good key management setup for you, how to size these accounts needs some consideration as well. Although the individual accounts are anonymous, the total allocation to any founding member is public. If all your accounts in the genesis block have unique balances, anyone will be calculate which accounts are yours.

#### Staking and Vesting

Whereas the considerations above are there for all projects in our space, the combination of staking locks and vesting terms are, although not unique, something that requires more thinking for Joystream.

For most stakeholders, their token allocation have a vesting schedule imposed in the genesis block. For the Jsgenesis team, Founding Members and other stakeholders involved in the community, only 8% of their tokens, are "free", (meaning no consensus based restrictions) in the genesis block. The rest are "freed" linearly over 24 months. Until a token is vested, it can only be used for a specific set of whitelisted transactions, that allows participation, but blocks everything that could be used to transfer or circumvent the vesting schedule.&#x20;

In the context of distributing tokens pre-launch, the main mechanics and implications of this is

1. Tokens can **not** be _moved_ to another account, or freed up in any way, until they are vested.
2. Tokens **can**, however be used to stake for roles, elections and validation in the meantime.
3. Due to the concept of "rivalrous locks", a specific account may only be put up as stake for a single slash-able purpose at the time.

Tying this together, this means:

> If you put all your tokens in one account, you may only be able stake for a single role or purpose at the time.
>
> If you spread your tokens evenly across too many accounts, you may not be able to stake for a single role or purpose.

Although the Council and/or Leads should take this into consideration in the early stages of mainnet, it's in everyones interest that stakeholders considers this.

More details about how staking locks can be found in the [accounts-and-staking](../../system/accounts-and-staking/ "mention") section in the more technical [system](broken-reference) part of the Handbook.

## Good Practices

Founding Members, and anyone else with the same vesting scheme, should consider coordinating their token allocations for a few different purposes.

* What are reasonable values to require as stake for the various roles. Although the Storage Lead should probably require a lot more stake than an HR worker, there will be common ground.
* As there are benefits in coordinating amounts for the purposes of anonymity as well, some "default sizes" can go a long way to avoid all of your accounts getting linked.

When submitting addresses for the genesis block, consider

* Any tokens you don't know for sure you want associated with your membership should be of a default size, or a multiple of one.
* Tokens in my membership account will be linked to my membership anyway, so that would be a good place to put any remainders.
* Some roles will require substantial stake to apply, or for an application to be taken seriously, and others (such as validators) will (at some level) be rewarded according to the stake.
* Depending on the purpose of an account, consider your key generation and management protocol.

The membership controller key, which you will need to vote on elections and create proposals might be impractical to keep in an airgapped multisig, but the membership root key, which allows you change your controller if it's lost or compromised, should probably not be saved in the browser at your local library computer.



## Summary

