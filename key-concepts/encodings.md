# Encodings

<!-- Member metadata -->

## Membership Metadata

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| name | string | optional | Member&#39;s real name |
| avatar | uint32 | optional | Member&#39;s avatar - index into external assets array |
| about | string | optional | Member&#39;s md-formatted about text |

<!-- Working Group Action (set_status_text metadata) -->

## Working Group Action

**Only one of the fields should be set.**

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| set_group_metadata | [SetGroupMetadata](#setgroupmetadata) | optional |  |
| add_upcoming_opening | [AddUpcomingOpening](#addupcomingopening) | optional |  |
| remove_upcoming_opening | [RemoveUpcomingOpening](#removeupcomingopening) | optional |  |

### SetGroupMetadata

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| new_metadata | [WorkingGroupMetadata](#workinggroupmetadata) | optional | New working group metadata to set (can be a partial update) |
### AddUpcomingOpening

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| metadata | [UpcomingOpeningMetadata](#upcomingopeningmetadata) | optional | Upcoming opening metadata |

### RemoveUpcomingOpening

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| id | string | optional | Upcoming opening query-node id |

### UpcomingOpeningMetadata

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| expected_start | uint32 | optional | Expected opening start (timestamp) |
| reward_per_block | uint64 | optional | Expected reward per block |
| min_application_stake | uint64 | optional | Expected min. application stake |
| metadata | [OpeningMetadata](#openingmetadata) | optional | Opening metadata |

### WorkingGroupMetadata

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| description | string | optional | Group description text (md-formatted) |
| about | string | optional | Group about text (md-formatted) |
| status | string | optional | Current group status (expected to be 1-3 words) |
| status_message | string | optional | Short status message associated with the status |

<!-- Working Group Opening metadata -->

## Working Group Opening Metadata

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| short_description | string) | optional | Short description of the opening |
| description | string | optional | Full description of the opening |
| hiring_limit | uint32 | optional | Expected number of hired applicants |
| expected_ending_timestamp | uint32 | optional | Expected time when the opening will close (Unix timestamp) |
| application_details | string | optional | Md-formatted text explaining the application process |
| application_form_questions | [ApplicationFormQuestion](#applicationformquestion) | repeated | List of questions that should be answered during application |

### ApplicationFormQuestion

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| question | string | optional | The question itself (ie. &#34;What is your name?&#34;&#34;) |
| type | [InputType](#inputtype) | optional | Suggested type of the UI answer input |

### InputType

| Name | Number | Description |
| ---- | ------ | ----------- |
| TEXTAREA | 0 |  |
| TEXT | 1 |  |

<!-- Working Group Application metadata -->

## Working Group Application Metadata

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| answers | string | repeated | List of answers to opening application form questions |

## Council Candidacy Note

| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| header | string | optional | Candidacy header text |
| bullet_points | string | repeated | Candidate program in form of bullet points |
| banner_image_uri | string | optional | Image uri of candidate&#39;s banner |
| description | string | optional | Candidacy description (md-formatted) |
