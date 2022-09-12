# Accounts and Membership

If you pass the verification, you will receive an email about submitting accounts for your allocation in the genesis block. As there are some nuances in this step for Founding Members compared to the general information found in [account-generation.md](../../system/accounts-and-staking/account-generation.md "mention"), some additional steps are outlined below.

### Membership Accounts

Your membership will be migrated over to the Carthage network, the last testnet before mainnet, by taking a snapshot at some cutoff. The same will be the case for the mainnet rather quickly after Carthage has been launched.

The critical part here are the `root_account` and `controller_account` for your membership. For most members, they are currently the same, but you will probably want separate ones.&#x20;

As explained in [memberships.md](../../system/memberships.md "mention"), the `controller_account` is what you use to act as the member, whereas the `root_account` is only valid for updating both, or either, of these for your membership. That means your `root_account` could be an offline key, whereas the `controller_account` should not.&#x20;

You may want to change your `root_account` to a more secure key, as that significantly reduces the risk of losing (control of) your membership.

## Submitting Accounts

There will be 1 Billion (1\*10^9) JOY in the genesis block.

As an example, suppose the member with Member ID `0` have earned 0.15% of the supply before the end of the Founding Member program. They will then be allocated...

```
1*10^9 *0.15/100 = 1500000 JOY
```

...in the genesis block. Each Founding Member will be able to decide on that allocation themselves, but we recommend that you ensure some tokens are available in both your `root` and `controller_account`.&#x20;

Your options and outcomes are described below.

### Email Format

When drafting the email, please stick to the following format:

* From: The address you provided in the verification
* To: `founding.members-at-jsgenesis.com`&#x20;
* Subject: Genesis Block Accounts for  `<memberId>` v0
  * Where `<memberId>` is replaced by your Member ID,
  * and v0 is the version index. If you want to update later on, please increment to v1.

Unless requested, the reply should contain just the accounts and balances. Questions can be sent, but in separate email(s).

If you were inducted as a Founding Member before August of this year, you have to sign the provide a signature of your accounts and balances with your _current_ membership root or controller.

#### No Account Submitted

If you, for whatever reason, do not respond, your full allocation will be split between your `root_account` and  `controller_account` at the time of the snapshot.

_Example_&#x20;

For the member with `memberId` 0, the accounts are both `5DaDUnNVzZPwK9KLwyPFgeSbc9Xeh6G39A2oq36tiV9aEzcx`.&#x20;

As Carthage (and mainnet) will use the new account format, the corresponding address will be `j4Sq83pcTsGty9km6DwpwXo9b8XcEByqCs6fFCb9D9ZJCtXF2.`

\->

```csv
account,balance
j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw,1500000
```

#### Single Account

If you submit a single account, your full allocation will be placed in that account:

_Example_

Account `j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw` submitted:

&#x20;\->

```csv
account,balance
j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw,1500000
```

#### Multiple Accounts, No Balances

If you submit `n` accounts, without any additional context, the tokens will be distributed evenly across those accounts.

_Example_

Accounts `j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw, j4Ux2pWDH4iSkKzmpWf1WpvjRmDFENcQkFruv4Jv78jQ8TjjZ, j4Sq83pcTsGty9km6DwpwXo9b8XcEByqCs6fFCb9D9ZJCtXF2` submitted:

\->&#x20;

```csv
account,balance
j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw,500000
j4Sq83pcTsGty9km6DwpwXo9b8XcEByqCs6fFCb9D9ZJCtXF2,500000
j4Ux2pWDH4iSkKzmpWf1WpvjRmDFENcQkFruv4Jv78jQ8TjjZ,500000
```

#### Multiple Accounts, With Balances

If you have specific wishes, such as to ensure that you have enough to stake for a couple roles, and have some in a stash, you have to submit as a csv, in the format below

```csv
id,account,balance
0,<account_0>,<balance_0>
1,<account_1>,<balance_1>
...
n,<account_n>,<balance_n>
```

To account for the fact that it's not yet _known_ exactly how much you will be allocated given that you may still earn more, you may leave a one balances open. If so, the remainder will be allocated equally across those.

_Example_

The member had earned 0.15% when submitting, but knew they would earn some more - but not how much. They submitted the following:

```csv
id,account,balance
0,j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw,x
1,j4UBhsq2pUWDRaiHnQuiYYvkVDmzLuefZXP96uynp9PMzhoHG,x
2,j4Ux2pWDH4iSkKzmpWf1WpvjRmDFENcQkFruv4Jv78jQ8TjjZ,800000
3,j4Sq83pcTsGty9km6DwpwXo9b8XcEByqCs6fFCb9D9ZJCtXF2,200000
4,j4SzsCgiKyf6Y2BiWqsjCLdUR619LWFvFGi6F8BawG1Njjxc4,200000
5,j4VJvghvFR8b9xVsBDAahfkg7PrbWWpVsaKjPkcZsjUPDKSCR,200000
```

At the end of the program, the member had earned a total of 0.1637% -> 1637000 JOY

That means the final allocation would be:

```csv
account,balance
j4Rsj3T87RPJs3q8yHiSpf24TByjtRTKzwcaMmQK1aLpcYGDw,118500
j4UBhsq2pUWDRaiHnQuiYYvkVDmzLuefZXP96uynp9PMzhoHG,118500
j4Ux2pWDH4iSkKzmpWf1WpvjRmDFENcQkFruv4Jv78jQ8TjjZ,800000
j4Sq83pcTsGty9km6DwpwXo9b8XcEByqCs6fFCb9D9ZJCtXF2,200000
j4SzsCgiKyf6Y2BiWqsjCLdUR619LWFvFGi6F8BawG1Njjxc4,200000
j4VJvghvFR8b9xVsBDAahfkg7PrbWWpVsaKjPkcZsjUPDKSCR,200000
```

### General Notes

#### Address Types

You don't have to submit accounts in the "new" joystream format, eg. `j4...`. instead of `5...`. This is covered with some depth [here](https://joystream.gitbook.io/testnet-workspace/system/accounts-and-staking/account-generation). TL;DR - your current key will work just fine, as long as you have either of:

* the `<5...key>.json`, which is currently stored in your [Polkadot{.js} extension](https://polkadot.js.org/extension/),
* the mnemonic phrase,
* the raw seed, OR;
* the `//suri`

If you want to confirm it is working, please try one our current staging networks. Unfortunately, these changes frequently, so we can't provide a link.

If you want to provide the keys in a different format, and are submitting multiple accounts and addresses as a csv, please replace `account` with `substrate` for `5...` or `pubkey` for `0x...`.

#### Multisig

The latest staging networks supports multisig. To create one, simply go to [polkadot-js apps](https://polkadot.js.org/apps/#/accounts), set the endpoint to one of these staging networks, and create one. We do not have any guides written for this yet, but polkadot has a lot of resources, for example [this](https://support.polkadot.network/support/solutions/articles/65000181826-how-to-create-and-use-a-multisig-account).

Warning: Pioneer will not support this in quite some time. Only use multisig for accounts that you don't intend to use for anything but balance transfers and the likes, as it will be tough to create transactions otherwise.

#### Changing Allocation

If you respond in time for the Carthage release, you will be able to test your accounts then. After that, you will be given a window of 2 weeks to change accounts **once**.

#### Maximum Accounts Exceeded

Although we haven't decided on any such limits yet, we may decide to limit either the minimum balance for a single account, or a maximum number of accounts. If so, we will try to reach out the affected parties.

#### Encrypting the Message

If you wish to keep this confidential, please use our [pgp key](https://keys.openpgp.org/search?q=86CF5F2F8450B13A557470E3232F7CE09F8DCAE9) when responding to the email.
