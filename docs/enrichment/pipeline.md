# Transaction and Source Coding Pipeline

Processing transaction and source code information is a multi-stage process, with automated and human elements involved.


## 1.Loading data from remote systems -- a.k.a. ETL
FraktureBots retrieve data from many different sources, in many different ways.  After all the waiting and pulls, and cleaning up and transforming, we get at least the following fields.

* ts  - The transaction date
* amount - The transaction amount
* source code - The source code on that transaction
* (numerous other fields not relevant to the pipeline)

The result is a table `<bot_prefix>_transaction`, if you're looking at the raw data

## 2. Assigning source codes

### Messages
Source codes are unique strings, often passed in a URL, that identify the source of a given link or interaction, and typically carry through the whole transaction.  Depending on the platform or organization, messages have many potential source codes.  Often there are source codes buried in links, or perhaps the name of the message, or the name of the campaign, etc, etc.  Frakture extracts source codes from all these places and stores them in the global message_source_code table.

In addition, for reporting purposes, Frakture identifies ONE source code as the *primary* source code.  This is so statistics can be rolled up per channel, per campaign, etc, without double counting any performance statistics.  To identify the primary source code, Frakture will use a number of heuristics, including parseability, length, format, etc.

Messages that do not have identifiable source codes, or no source codes that appear to be a primary code, will be assigned a "fkauto-<type>" source code, that identifies the bot that source code came from.


### Transactions
Transaction source coding comes from the source CRM or payment processor.  Often called a source, refcode, code, etc, it's a string of characters that has passed from the link or channel, the payment form, and stored in the payment processor.

For transactions that are NOT source coded in their source system, Frakture will assign a source code 	
`<payment form name>_NO_SOURCE`
 based on the name of the payment form (if available in the source platform).


## 2.Metadata tables

### Transactions
Frakture stores transaction overrides in a global metadata table.  Other data exists in that table, as well, and note that this is an account-wide table.  It can have no prefix (transaction_metadata), or be prefixed with the account_id (`<account_id>_transaction`).


## 3.Overriding source codes -- (optional)

### Transactions
Sometimes the data that's coming in is difficult to parse, or was never coded, or you need to do some human cleaning.
Frakture provides a Google sheets implementation that pushes out a list of transactions and supporting information to allow you to override the source code.  This is useful when you have transactions coming in that
may not have been source coded.  Frakture can deploy a Google sheet with a tab name `<account_id>_transaction` that will list the last 30 days of transactions, and optionally beyond that.
In this sheet, there are two columns

| Column         	| Purpose |
| ------------- |:-------------:|
|transaction_source_code_override|Replace a source code with another one.  This code will later be parsed, so should have as much useful info as possible -- e.g. EOQ_FB_C1_2020-01-01|

This data will be stored in the `<global_prefix>transaction_metadata_override` table.


## 4.Source code dictionary
Every source code that is used anywhere in Frakture is put into the <global_prefix>source_code_dictionary table.  This is the canonical list of source codes, actively in use or perhaps slated for use later.  It also contains 0-N columns to represent the broken-out elements of that source code.  For example, an organization may have configured 'channel_prefix' and 'campaign_name' source code elements -- those columns exist in the source code dictionary.

`<global_prefix>_source_code_dictionary` -- Full list of source codes, and columns for elements of that source code.

Source code elements are organization specific, and are not stored in the warehouse, but in the master Mongo DB that contains all the configurations.  Agencies tend to have the same set of elements across all their clients.

There is also a `<element>_label` field for every element in the source code dictionary -- in our example, the element value would be "FB", and the label would be "Facebook".  Labels are suitable for human viewable reporting, whereas the value is what the Bots and tables work with.

## 5.Auto-parsing of source codes

For every source code that comes in, we need to break out -- or parse -- individual elements from a source code.  For example, we need to extract the Facebook (FB) element from EOQ_FB_C1_2020, and the campaign name (End of Quarter).

In the real world, there's LOTS of different source codes for an organization, both legacy and new source codes, that don't all match the same format.

As such, Frakture supports multiple algorithms, known as "source code formats", to extract meaning from a source code.  A source code format defines what the source code looks like, typically using regular expressions or simplified merge fields.  For example: `{{channel_prefix}}_{{campaign}}_{{platform}}_{{variant}}_{{date}}`.

During this auto-parsing stage, Frakture will go through the different formats and attempt to use them to parse the source code.  The results will be stored in the source_code_dictionary table, along with the format that matched.

### Sample source codes and formats
| Source code         	| Matching Format | Channel | Campaign | Signer |
| ------------- |:-------------:| -----:| -----:|-----:|
| FB_EOQ1         | {{channel_detail}}_{{campaign}} | Facebook | End of Q1 | |
| EM_Sharks         | {{channel_detail}}_{{campaign}} | Email | Sharks | |
| v2_PITT_YT_TW         | v2_{{signer}}_{{channel_detail}}_{{campaign}}  | YouTube | Twitter | Pitt|
| website         | (unknown)  | ? | ? | |

## 6.Overrides of source code parsing (Optional)
Unfortunately automated parsing of source codes can only go so far.  Often a human must be involved to apply some intelligence to a parsing of a source code.  This is particularly necessary when there's lots of legacy, or poorly formed source codes.  To allow for this, Frakture supports pushing the full source code dictionary to a Google spreadsheet, where humans can assign values to all the elements.  The source code tab is named `<account_id>_source_code`.


## 7.Source code aggregation by date

To optimize reporting by source code, Frakture aggregates dozens of statistics by source code, and caches them in the source_code_stats_by_date table.

`<global_prefix>_source_code_stats_by_date` -- global statistics by source code by date

This includes things like total transactions and revenue, and messaging data like impressions/clicks/spend, based on the primary_source_code of a message.


## 7.Source code aggregation all time

To optimize reporting by source code, Frakture aggregates dozens of statistics by source code, and caches them in the source_code_stats_by_date table.

`<global_prefix>_source_code_stats_by_date` -- global statistics by source code by date

This includes things like total transactions and revenue, and messaging data like impressions/clicks/spend, based on the primary_source_code of a message.



## 8. Pulling it all together -- the summary tables

A typical final report or view will summarize data broken out by element - "How much money did we raise, grouped by channel?"  "How did each of our campaigns do?", etc.  To enable this, there are two standard Frakture views:

`<global_prefix>_source_code_summary_by_date`

and

`<global_prefix>_source_code_summary`

which includes information from source_code_dictionary, source_code_dictionary_override, and the source_code_stats/source_code_stats_by_date table.  It is the final output from all the previous stages of automation and manual cleanup, suitable for GDS or other reporting suites.
