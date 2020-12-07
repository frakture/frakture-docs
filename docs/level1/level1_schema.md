# Level 1 Data Schema Overview

Level 1 tables store information directly after translating from the source system into Frakture's standard schema -- universal Frakture field labels used in place of the idiosyncratic field names applied by various source systems. We do this for several reasons:

* Standardized naming makes like data sets comparable and like systems hot-swappable, so that the warehouse is frictionless when  you add a new digital channel or switch to a new platform.
* Standardized naming makes data machinable so that second-order automated processes (e.g., attribution in Frakture's Level 2 services) can be deployed with ease.

Level 1 data is generally stored with a three-part field format:

<platform>\_<bot_id>\_<data_type>

_Platform_ is simply the name of the platform (e.g. googleads, facebook, or luminate). The _bot_id_ is a random identifier unique to one specific bot on one specific account (e.g. kce or xfp); this identifier might be repeated for several tables, if all those tables are obtained from the same source system. The _data_type_ is described by a word or two (e.g. person or transaction).

> **_EXAMPLE:_**  Frakture is loading gift and donor data from your Raiser's Edge NXT system, and the NXTBot on your account happens to have the unique identifier "bzt". Your table names are renxt_bzt_person and renxt_bzt_transaction.

## People Data

<platform>\_<bot_id>\_person

One record per person in the source system.

While some bots might extract some additional boutique fields, the core person fieldset is as follows:

_*remote\_person\_id*_ [sometimes simply _id_] Table's primary key; the unique identifier assigned to the person by the source system
_*date\_created*_ The timestamp for the record's creation date in the source system, if available
_*remote\_last\_modified*_ The timestamp for the record's most recent modification or update in the source system, if available
_*given\_name*_ The first name or personal name
_*family\_name*_ The last name or surname
_*email*_ The canonical or primary email address associated with the person record.
_*phone*_ The canonical or primary phone number associated with the person record.
_*street*_ The first or primary street address line
_*street\_2*_ The second street address line, where available
_*street\_3*_ The third street address line, where available (most often, this field is not extant)
_*city*_ The
_*region*_ The state, province, or other regional designation.
_*postal\_code*_ The post code or zip code. Note that Frakture does not append postal code data based on other address information, in the absence of a postcode provided by the source system.
_*country*_ The country. Note that Frakture does not append country data based on other address information, in the absence of a country provided by the source system.

## Transaction Data

<platform>\_<bot_id>\_transaction

One record per monetary transaction in the source system. Note that the flexible word "transaction" is used in some outside systems to denote interactions other than monetary (such as form submissions or clicks). Frakture's Level 1 transaction data consists solely of financial transactions.

While some bots might extract some additional boutique fields, the core transaction fieldset is as follows:

_*remote\_transaction\_id*_ [sometimes simply _id_] Table's primary key; the unique identifier assigned to the transaction by the source system.
_*remote\_person\_id*_ The unique identifier assigned to the donor by the source system; maps to the field of the same name on the warehouse person table for the same system.
_*amount*_ Currency units (most commonly US Dollars) for the transaction, expressed as a decimal, e.g., 10.00 for a $10 transaction.
_*ts*_ The timestamp associated with the gift in the source system (in a word, the date of the gift).
_*source_code*_ The canonical source code associated with the gift, a key field for Frakture's Level 2 attribution analytics.

## Messaging data and summary views

<platform>\_<bot_id>\_message
<platform>\_<bot_id>\_stats
<platform>\_<bot_id>\_stats_by_date
<platform>\_<bot_id>\_<channel> (e.g., \_emails or \_ads or \_surveys)
<platform>\_<bot_id>\_<channel>\_summary
<platform>\_<bot_id>\_<channel>\_summary\_by\_date (where available)

While person and transaction data loads straightforwardly into a single table, messages data is a bit more nuanced. In Frakture, "messages" is a catchall term encompassing any, well, "message" that's being sent to actual or potential supporters. Both emails and digital ads are messages, and each generate their own types of performance metrics.

All forms of messaging data generate a _\_message_ table, with information about the message itself -- such as the campaign it belonged to and when it was posted or sent.

The message's associated raw metrics go to a _\_stats_ table.

Raw message and stats data is compiled together into a _\_summary_ view with more convenient and intuitive per-message rows suitable for reporting. When the channel facilitates it (this is more typical of ad performance data than email performance data, for example), we'll also create a _\_summary\_by\_date_ view capturing per-message, per-date statistics.
