# 🔑 Memberships

## Introduction

A membership is a representation of an actor on the platform, and it exist to serve the following purposes

* **Profile:** A membership has an associated rich profile that includes information that support presenting the actor in a human friendly way in applications, much more so than raw accounts in isolation.
* **Reputation:** Facilitates the consolidation of all activity under one stable identifier, allowing an actor to invest in the reputation of a membership through prolonged participation with good conduct. This gives honest and competent actors a practical way to signal quality, and this quality signal is a key screening parameter allowing entry into more important and sensitive activities. While nothing technically prevents an actor from registering for multiple memberships, the value of doing a range of activities under one membership should be greater than having it fragmented, since reputation, in essence, increases with the length and scope of the history of consistent good conduct.

It's important to be aware that a membership is not an account, but a higher level concept that involves accounts for authentication. The membership subsystem is responsible for storing and managing all memberships on the platform, as well as enabling the creation of new memberships, and the terms under which this may happen.

## Concepts

### Membership

A membership includes the following

* **Id:** A unique immutable non-negative integer identifying the member, automatically assigned when membership is created.
* **Root Account:** A required account that is used only to update the controller account. Need not be unique across members, but in practice probably will be.
* **Controller Account:** A required account that is used to authenticate as the member, both in this and other parts of the platform. Need not be unique across members, but in practice probably will be.
* **Name:** A human readable mutable string.
* **Handle:** A unique mutable string handle.
* **Invites:** A mutable non-negative integer that represents how many invitations this member has.
* **Verified:** A mutable boolean indicator that reflects whether the implied real world identity in the profile corresponds to the true actor behind the membership.
* **Avatar:** A mutable URI for an avatar image.
* **About:** A mutable human readable text description.
* **Founding Member**: A signifier that this member holds some specific historical significance to the launch of the platform. This value will be stored in the chain state when mainnet launches, but for now, since we want to grant founding member status on an ongoing member through a SUDO call, this is in history.
* **Staking Accounts:** A set of accounts that have been bound to this membership for the purpose of holding staked funds. One account can only be used to stake for at most two separate purposes simultaneously, and one of them has to be an election related purpose, i.e. voting or council candidacy. One account can only be a staking account for a single member, and once associated in this way, it cannot be de-associated and associated with another member. Every candidate as an staking account requires staking to stay as such.

#### Metadata

For the sake of the runtime the following fields are completely opaque:

* Name
* Avatar
* About

Therefore these fields aren't saved into the storage, aren't checked, and in the extrinsics parameters they are all bundled together in a single `meta_data` field.

### Working Group

The membership subsystem has a working group. The purpose of the group is to effectively distribute invitation quotas and verified status. The lead, called the _membership lead_ has the extra task of refreshing the quotas to workers, which they can in turn then distribute to other members. Workers are referred to as _membership evangelists_.

### Buying a Membership

The primary means of establishing a membership is buying one by burning tokens, the number of which is held in a mutable parameter denoted as `membership_price`. When purchasing a membership, another member, called a _reference,_ can be referenced, resulting in a portion of the burned funds being credited to the reference. This portion is a mutable parameter denoted as `referral_cut` and defined as the membership fee percentage. Currently, there is a limit of 50% for the referral cut.

### Invitations

The long-term objective is to have most memberships established by being purchased, however, currently the various costs associated with gaining access to a digital asset are considerable. As a result, person-to-person invitations is an alternative mechanism for giving new community members direct access to participate on the platform. When buying a membership, an initial number of invitations are granted, the number of which is held in a mutable parameter denoted as `default_invite_count`. On accepting membership invitations make sure that you're controlling both controller and root accounts. Losing (or not having in the first place) control of the root account could result in a hostile takeover of your membership.

#### Quotas

This works by giving each person an _invite quota_, that is a certain number of outstanding invitations available at any given time. The quota is initially set when buying a membership, but it can also be increased by having another member transfer some of theirs. The quota of the lead can also be set by the council through a proposal.

#### Initial Balance

When a member is invited, they are also credited some initial balance to their controller account so that they can engage in some initial set of activities. These funds are however only spendable on transaction fees, nothing else, such as transferring to another member. The amount credited is held in a mutable parameter denoted as `invited_initial_balance`.

## Constants

The following constants are hard coded into the system, they can only be updated with a runtime upgrade.

| Name                    | Description                                                               | Value     |
| ----------------------- | ------------------------------------------------------------------------- | --------- |
| `INVITE_LOCK_ID`        | The identifier value for the lock applied to root account of a new member | `fill-in` |
| `MAX_NUMBER_OF_WORKERS` |                                                                           | `fill-in` |

## Extrinsics

### Buy a Membership

**Parameters**

| Name                 | Description                                     |
| -------------------- | ----------------------------------------------- |
| `root_account`       | To be root account of membership.               |
| `controller_account` | To be controller account of membership.         |
| `handle`             | To be handle of membership.                     |
| `metadata`           | Encoded [membership metadata](broken-reference) |
| `referer_id`         | Optional identifier of some existing member.    |

#### Conditions

* Free balance of the signer account exceeds `membership_price`.
* `handle` must be unique among all existing handles.
* If provided, `referer_id` must correspond to an existing member.

#### Effect

* A new membership is created with the provided information, and initial invites set to `default_invite_count`.
* If `referer_id` is provided, then the corresponding member has`X = membership_price * referral_cut / 100%` credited to their controller account and `membership_price - X` is burned, otherwise `membership_price` is burned.

### Invite a Member

**Parameters**

| Name                 | Description                                     |
| -------------------- | ----------------------------------------------- |
| `member_id`          | Identifier of inviting member.                  |
| `root_account`       | To be root account of membership.               |
| `controller_account` | To be controller account of membership.         |
| `handle`             | To be handle of membership.                     |
| `metadata`           | Encoded [membership metadata](broken-reference) |

#### Conditions

* Signer matches controller account of member corresponding to `member_id`.
* Invitation quota of member is non-zero.
* `handle` must be unique among all existing handles.
* Working group budget is no less than `invited_initial_balance`.

#### Effect

* A new membership is created with the provided information, and initial invites set to zero, and the root account is credited with`invited_initial_balance`.
* Working group budget is deducted by `invited_initial_balance`.
* `controller_account` is encumbered with lock with ID `INVITE_LOCK_ID` and of size `invited_initial_balance` that only allows transaction fees, and credited with the same amount of tokens.
* Invite quota of member corresponding to `member_id` is decremented.

### Update Profile

**Parameters**

| Name           | Description                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------- |
| `member_id`    | Identifier of member wishing to update profile.                                                         |
| `handle`       | Optional new handle for membership.                                                                     |
| `new_metadata` | Optional new encoded [membership metadata](broken-reference) (only the provided fields will be updated) |

#### Conditions

* Signer matches controller account of member corresponding to `member_id`.
* if set `handle` must be unique among all existing handles.
* at least one of the optional fields must be set.

#### Effect

Profile of member corresponding to `member_id` is updated with new field values.

### Transfer Invites

**Parameters**

| Name                  | Description                                       |
| --------------------- | ------------------------------------------------- |
| `member_id`           | Identifier of member wishing to send invites.     |
| `recipient_member_id` | Identifier of member to be credited with invites. |
| `number_of_invites`   | Number of invites to transfer.                    |

#### Conditions

* Signer matches controller account member corresponding to `member_id`.
* `recipient_member_id` corresponds to a existing recipient member.
* `number_of_invites` is no greater than invitation quota of sender.

#### Effect

`number_of_invites` is transferred from invite quota of sender to recipient.

### Update Accounts

**Parameters**

| Name                 | Description                                       |
| -------------------- | ------------------------------------------------- |
| `member_id`          | Identifier for member wishing to update accounts. |
| `root_account`       | Optional new root account for membership.         |
| `controller_account` | Optional new controller account for membership.   |

#### Conditions

* Signer matches controller account member corresponding to `member_id`.
* At least one new account is provided.

#### Effect

Update provided accounts on member.

### Update Verified Status

**Parameters**

| Name          | Description                                  |
| ------------- | -------------------------------------------- |
| `worker_id`   | Identifier of membership evangelist.         |
| `member_id`   | Identifier of member to have status updated. |
| `is_verified` | New status of member.                        |

#### Conditions

* Signer matches controller account of worker corresponding to `worker_id`.
* `member_id` corresponds to some existing member.

#### Effect

Verification status of member is set to `is_verified`.

### Bind Staking Account

**Parameters**

| Name        | Description                           |
| ----------- | ------------------------------------- |
| `member_id` | Identifier of member to bind account. |
| `account`   | Account to be bound.                  |

#### Conditions

* Signer matches controller account of member corresponding to `member_id`.
* `account` is not already bound to any other member.

#### Effect

`account` is bound to member.
