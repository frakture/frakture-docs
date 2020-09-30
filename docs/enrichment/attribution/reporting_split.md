# Message Attribution vs Metadata Reporting

Sometimes the easiest questions can actually result in some fairly complicated reporting questions.  This is usually because of assumptions we all have in our heads about what we 'mean' in the question.

To illustrate the point, let's talk about the easy question "How Much Money did we raise on Facebook in January".

We're going to look at these numbers in two ways
	* Via Metadata reporting -- this is using the source code of a transaction to derive reporting information -- what Frakture calls Metadata
	* Via Attribution reporting -- this is running reports AFTER pairing up transactions with a specific outgoing message

In an ideal world, these should be exactly the same.  Every outgoing message would have a unique correctly formatted source code, so the attributed reporting numbers for say, Facebook, would exactly match the metadata in that source code.

In the real world, these can diverge quite quickly.

Let's look at just 4 transactions -- 2 that we can directly pair up with a Facebook Ad (via automated attribution), and two we can't.

| Transaction Date         	| Amount | Source Code | Automatically attributed to a FB Ad first published on Jan 1 |
| ------------- |:-------------:| -----:| -----:|
| Jan 1         | $1 | FB_ABC_123 | No |
| Jan 7         | $7 | Facebook_123 | No |
| Jan 15         | $15 | FB_123 | Yes |
| Feb 2         | $20 | ABC_123 | Yes |


If we pull this report, we see the following 6 possible combinations of results.
##Jan 1 -> Jan 31 report

|         | Description           |  By Transaction Date  | By Publish Date |
| ------------- |:-------------:| -----:| -----:|
| Based on Transaction Source Code      |  A source code that exactly matches 'FB*' | $16|$15  |
| Based on Attribution      | A source code that has a matching source code with a FB Ad |   $15 |$35  |
| Humans | (manual rollup of FB+Facebook source codes)     |    $23| N/A (no attribution) |


If you're using humans, you might report $23.  If you're using automated attribution, and you elect the transaction source code as preferred, you'd report $16 (Facebook is easily identifiable to humans, but not bots).  If you want to see how a specific ad published in January performed, you might report $35.


Realizing that Frakture supports a number of use cases, here's the tables you'll want to use depending on how you prefer to report:

|         | Description           |  By Transaction Date  | By Publish Date |
| ------------- |:-------------:| -----:| -----:|
| Based on Transaction Source Code      |  A source code that exactly matches 'FB*' | *summary_by_date* table, Metadata* columns| summary_table, metadata* columns |
| Based on Attribution      | A source code that has a matching source code with a FB Ad |   summary_by_date table, attribution* columns |summary table, attribution* columns  |
| Humans | (manual rolloup FB+Facebook)     |    (your custom tables)| N/A (no attribution) |
