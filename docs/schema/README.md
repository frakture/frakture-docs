# Frakture Schema

A Frakture Warehouse holds many types of objects that have been mapped from various source systems into a normalized schema.
The most common object types in a Frakture Warehouse are:

- **Messages**: Emails, Ads, Surveys... Any form of data that presents information to a person, and their statistics
- **Transactions**: Donations, Gifts, Pledges... Any form of data that represents a monetary transfer
- **People**: Constituents, Volunteers, Donors... Any form of data that represents a single person


Frakture classifies it's data into multiple "Levels", where each successive level adds in and extends the raw data.

MOST users will want to use the `summary` tables, which are views that incorporate data from multiple useful core data tables.  These summaries are optimized for use by third party reporting suites, as well as Frakture native reporting.



## Level 1 - Extract Transform Load
Level 1 tables store information directly after downloading and translating from the source system.  Level 1 data is stored with the table format:

`<platform>_<bot_id>_<data_type>`

where the `platform` is a prefix for the platform (e.g. googleads, facebook, luminate, etc), the `bot_id` is a random unique identifier for a specific login for that platform (e.g. kce, xfp), and the data_type depends on the type of data.

### Messaging data and summary views

#### Tables
`<platform>_<bot_id>_message`,`<platform>_<bot_id>_stats`,`<platform>_<bot_id>_stats_by_date`:
	Emails, Ads, Surveys... Any form of messaging has their raw data in the message and stats tables.

#### Views
`<platform>_<bot_id>_<channel>_summary`,`<platform>_<bot_id>_<channel>_summary_by_date`:
	Each channel (email,ad, etc) also has a summary view, that joins in the stats tables into more convenient layouts for reporting.  There may be more than one channel per bot (signup pages, donation pages, emails, etc), the summary views display the most useful statistics for each channel.

### People Data
`<platform>_<bot_id>_person`: One record per person in the source system.  Data is mapped into a common schema, with the remote_person_id as the unique key

### Transaction Data
`<platform>_<bot_id>_transaction`: One record per *monetary* transaction in the source system (if available).  This does NOT include other types of transactions (form submissions, clicks, etc), which are considered level 5 data.  

## Level 1A - Transaction Attribution

Attribution is the process of assigning a transaction to a particular outbound message.  It is a global process, as many organizations use multiple messaging and payment platforms, and primarily leverages source codes to identify the source message.  As such, there is only one instance of these tables for any group.

### Tables
`message_source_code` - Stores one entry for every source code and message.  Can store multiple source codes per message.
`attribution` -- The attribution table contains one entry per attributed transaction.  A transaction is attributed when it is uniquely paired up with a source message, using Frakture's attribution algorithm.
`transaction_metadata` - Global tables that store additional metadata about transactions, including overrides, origin sourcing, etc.

### Summary Views
`transaction_summary` - Global view that includes information from the source code dictionary


## Level 2 - Source Code parsing and Global Stats
Level 2 is all about source code management and parsing.  For most advanced users, source codes are the core to quality cross-channel reporting.  Frakture aggregates the source codes, then attempts to auto-parse them into elements designed for reporting.

`source_code_dictionary` - A full list of all source codes from your organization, whether it be from messages, transactions, or people.  Also contains information on auto-parsing, such as the format that matched, and the resulting extracted elements (like source_code_channel, agency, audience, etc).  Elements also have corresponding _label fields that are suitable for humans.

`source_code_dictionary_override` - Contains human provided overrides for source codes.  Bots don't put data into this table, but do consume it for building reports.

`source_code_stats` - Statistics grouped by source code
`source_code_stats_by_date` - Statistics grouped by source code and by date

### Summary Views
Summary views are the most commonly used views to report on.  They include data from the source code dictionary, including labels and other metadata, as well as statistics gathered from all components of Frakture.

`source_code_summary` - Statistics grouped by source code, with additional dictionary definitions joined in.
`source_code_summary_by_date` - Statistics grouped by Source code and date, with additional dictionary definition fields joined in




## Messages

Frakture Warehouse messages for a given system can be found in the a view named `<table_prefix><channel>_summary`. For instance,
the Facebook Ads for a bot with table_prefix "fb_biz_1t5" would be "fb_biz_1t5_ads_summary".

The standard message definition fields are:

| Field | Description |
| --- | --- |
| remote_id | The unique identifier of the message within the source system |
| publish_date | The date when the message was published - this can be the send date of an email, the first day an ad is displayed, etc |
| label | A shortened title for the message - this can be the subject of an email, the title of an ad, etc |

In addition to these fields that are captured from the source system, there are several appended by Frakture:

| Field | Description |
| --- | --- |
| message_id | The unique identifier of the message within Frakture |
| channel | A short word describing the type of message - "email", "ad", "form", etc |
| primary_source_code | A Frakture Bots best guess at the source code associated with this message. Can be overriden |

Individual Message Statistics are also pulled into the Warehouse and supplied alongside these definition fields.

The standard message stat fields are described below, along with the standard definition for each*:

| Field | Description |
| --- | --- |
| impressions | How many times this message was seen by a target |
| clicks | How many times a link from that message was clicked |
| interactions | |
| revenue | The system reported amount of money generated by this Message |

* Systems have different ways of calculating, tracking, and presenting these values. To see how each maps to the source system, check the documentation for that system.

In addition to these fields, Frakture appends the following [Attribution](/enrichment/attribution/) fields:

| Field | Description |
| --- | --- |
| attributed_transactions | The number of monetary transactions that Frakture has attributed to this message |
| attributed_revenue | The sum total of monetary transactions that Frakture has attributed to this message |

Specific Message schema definitions can be found [here](/schema/messages).

## Transactions

Monetary transactions for a given system can be found in a table named `<table_prefix>transaction`.

The standard fields collected for monetary transactions are:

| Field | Description |
| --- | --- |
| remote_transaction_id | The unique identifier for this transaction in the source system |
| ts | The timestamp when this transaction was processed, as reported by the source system |
| amount | The amount of money reported by the source system |
| recurs | String defining the frequency of the transaction - `null`, "weekly", "monthly", and "annually" currently supported |
| recurring_number | Integer representing the number of transactions that have been made in this sequence. `null` if not recurring, 1 if first gift. Not supported by all systems, and some may show 2 for all subsequent gifts |
| source_code* | An identifier from the source system that identifies how a transaction entered the system |


 * Systems have different ways of representing source code information, and occasionally this is spread across multiple fields.

## People

Person records within a given system can be found in `<table_prefix>person`. The standard person fields pulled into the Frakture warehouse are:

| Field | Description |
| --- | --- |
| remote_person_id | The unique identifier for this record in the source system |
| date_created | The date this record was created in the source system |
| remote_last_modified | The date this record was last modified in the source system. **Note:** Not all systems report the date that a record was last modified - in this case this field is left null |
| given_name | The given name as reported by the source system. Normally corresponds to *First* name |
| family_name | The family name as reported by the source system. Normally corresponds to *Last* name |
| email | The email address associated with this record in the source system. If the source system stores multiple email addresses, Frakture defaults to the *Primary* email address. A standard Frakture deployment only loads one email address per person record |
| phone | The phone number associated with this record in the source system. If the source system stores multiple phone numbers, Frakture defaults to the *Primary* phone number. A standard Frakture deployment only loads one phone number per person record |
| street_1 | The first line of the *Primary* street address associated with this record in the source system |
| street_2 | The second line of the *Primary* street address associated with this record in the source system |
| city | The city of the *Primary* street adddress associated with this record in the source system |
| region | The region (state, province, territory, etc) of the *Primary* street address associated with this record in the source system |
| country | The country of the *Primary* street address associated with this record in the source system |
| postal_code | The postal code (zip code) of the *Primary* street address associated with this record in the source system |
| source_code | The *source_code* used when this record was created in the source system. Used as an *origin_source_code* for purposes of attribution |

## Advocacy Actions

For systems that support it, advocacy actions can be loaded into the warehouse on a per-person per-action basis - each action that a person takes is stored as an individual record in the `<table_prefix>advocacy_action` table.

| Field | Description |
| --- | --- |
| remote_action_id | The unique identifier for this record in the source system. **Note:** many source systems (such as Engaging Networks and Convio Lumninate) do not provide a unique identifier for individual actions taken. In these cases Frakture does it's best to assign a unique identifier to each action |
| remote_person_id | The unique identifier for this person record in the source system |
| ts | The timestamp recorded by the source system of when the action took place |
| source_code | The *source code* associated with this action, based on the link used to take the action |
| campaign_name | The name of the campaign associated with this action |

## Per-Person Message Stats

For systems that support it, mailing actions (opens, clicks, etc) can be loaded into the warehouse on a per-person per-mailing basis - each message that a person receives is stored as an individual record in the `<table_prefix>per_person_message_stat` table

| Field | Description |
| --- | --- |
| message_id | The Frakture assigned ID for this message. Links to the `<table_prefix>message` table using `message_id` |
| remote_person_id | The unique identifier for this person record in the source system |
| ts | The last time these stats were updated within the source system |
| recieved | Whether or not (1/0) this message was received by the person. Some systems _only_ report those who received a message |
| opened | Whether or not (1/0) the source system recorded this person opening the message |
| clicked | Whether or not (1/0) the source system recorded this person clicking a link within the message |
| action | Wether or not (1/0) the source system recorded this person taking an action inspired by this message |
| hard_bounce | For email messages - whether the source system records a hard_bounce for this person |
| soft_bounce | For email messages - whether the source system records a soft_bounce for this person |
| unsubscribe | Whether or not (1/0) the source system recorded this person unsubscribing as a result of this message |

**Note** General message stats can be found in `<table_prefix>_message_summary` tables. For general reporting on how a message performed, we recommend using those tables. The *per_person_message_stat* tables be used for deeper reporting - how a message performed acros a given segment.
