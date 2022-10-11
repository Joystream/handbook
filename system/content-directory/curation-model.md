---
description: A temporary one page explainer for curators
---

# Curation Model

This is meant as a placeholder description for the benefit of the content curation working group before a full article can be prepared.

The curator model is centered around workers, and the lead, in the curator working group. These actors can engage in a range of special activities in the content directory which others cannot.

## Moderation Actions

These actions, referred to as _curation_, are currently

```
pub enum ContentModerationAction {
    // Related extrinsics:
    // - `set_video_visibility_as_moderator`
    HideVideo,
    // Related extrinsics:
    // - `set_channel_visibility_as_moderator`
    HideChannel,
    // Related extrinsics:
    // - `set_channel_paused_features_as_moderator` - each change of `PausableChannelFeature` `x` requires permissions
    //   for executing `ChangeChannelFeatureStatus(x)` action
    ChangeChannelFeatureStatus(PausableChannelFeature),
    // Related extrinsics:
    // - `delete_video_as_moderator`
    DeleteVideo,
    // Related extrinsics:
    // - `delete_channel_as_moderator`
    DeleteChannel,
    // DeleteVideoAssets(is_video_nft_status_set)
    // Related extrinsics:
    // - `delete_video_assets_as_moderator` - deletion of assets belonging to a video which has an NFT issued
    //   requires permissions for `DeleteVideoAssets(true)` action, deleting other video assets requires permissions for
    //   `DeleteVideoAssets(false)`.
    DeleteVideoAssets(bool),
    // Related extrinsics:
    // - `delete_channel_assets_as_moderator`
    DeleteNonVideoChannelAssets,
    // Related extrinsics:
    // - `update_channel_nft_limit`
    UpdateChannelNftLimits,
}
```

Notice a few things

* hiding is a signal which causes Argus to not distribute this content to end-users, for channels it implies all dataobjects for the channel and any video in the channel, and for a video it implies all data objects for that video.
* deleting a video is only possible if no NFT has been issued, however, deleting data objects for this video is always possible.
* deleting a channel is only possible if it has no videos, and it involves delting all data objects for this channel.
* where `PausableChannelFeature` encompasses the following channel features which can be paused.

```
pub enum PausableChannelFeature {
// Affects:
// -`withdraw_from_channel_balance`
// -`claim_and_withdraw_channel_reward`
ChannelFundsTransfer,
// Affects:
// - `claim_channel_reward`
// - `claim_and_withdraw_channel_reward`
CreatorCashout,
// Affects:
// - `issue_nft`
// - `create_video` (if `auto_issue_nft` provided)
// - `update_video` (if `auto_issue_nft` provided)
VideoNftIssuance,
// Affects:
// - `create_video`
VideoCreation,
// Affects:
// - `update_video`
VideoUpdate,
// Affects:
// - `update_channel`
ChannelUpdate,
// Affects:
// - `issue_creator_token`
CreatorTokenIssuance,
}
```

## Cruator Groups and Permissions

Since many of these actions are quite invasive, there is a permissionsing system which constrains exactly what curator can do what actions on a given channel. To make the management of curators, and their permissions, practical at scale, the concept of _curator groups_ has been introduced. A curator can be part of none or many such groups, and the permissions exist at the group level, not curator. Channels are partitioned into permission levels called _channel permission levels_. When first created a channel has a default permission level, but this can be updated later by the lead. The levels themselves have no direct meaning, and are identified by integers, but there is no relationship between the permissions of a channel and the level. The permissions of a curator group describe what moderation actions group members can do for different permission levels. If no such action description exists for a given permission level, then group members cannot do any moderation action at all for channels with this level.
