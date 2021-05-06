
# Transactions vs Messages vs Source Code reporting
## AKA The Attribution Discontinuity

So, you want to report on all messages and all transactions.  All of it.  Not hard, right?  Well, there's a couple things you need to know.  Unless you have 100% perfect attribution -- meaning every transaction is connected to one and only one message -- your choice of "where to start" becomes very important.

Let's say you're a finance human, and believe that transactions are the most important thing.  You want to pull every transaction, and then figure out where it came from.  If there's messages without transactions attached to them, no worries, ignore those messages, at least you have all the money included!  Use the transaction_summary table.  It has a record for every donation, then (possibly empty) information about the message we can pair it up with.

Let's say you're a content human, and are looking at the world like someone who sends out messages and wants to figure out how they performed.  Donations are probably coming in elsewhere, but that's someone else's problem -- you want every message you've sent and how they've performed.  Awesome.  Use the global_message_summary table, or it's sibling, the global_message_summary_by_date.  It has an entry for every message, and then (possibly empty) data about transactions from that.

And in fact, if every transaction is perfectly attributed, you'll get the exact same results ... although structured slightly differently ... because everything pairs up.

Sadly, that's often not the case.  So we also provide another view of your data -- the source_code_summary_by_date.  It starts at the source code, and adds up all transactions with that source code, and then aggregates the statistics of messages with that source code.  (It uses a messages primary source code so there's not duplicates).  With this table, you can show a Source code, how much money it raised, how much you spent on it, how many impressions/clicks/opens on it.  If we can break out the source code, you can then roll that up by channel, or by campaign -- however you want to.



## Tables you'll want to use
|         | Description           |  Tables |
| ------------- |:-------------:| -----:|
| Based on Transactions      |  You must have all transactions | transaction_summary |
| Based on Messaging      | Your must have all messages (ads/emails/etc) |  global_message_summary & global_message_summary_by_date (for ads) |
| Based on Source Codes      | You want it all, and source coding is good. |   source_code_summary_by_date  |
