# Attribution Models

How to assign credit for transactions and revenue is not a trivial matter.  In fact it's one that has widely varying strategies, and no 'right' answer.

Attribution in Frakture is heavily tied to source coding -- the process of assigning a source code to transactions and individuals.  Much of the below is relevant to other conversion mechanisms -- see [Conversion Methods](enrichment/conversions "Conversion overview") for more info.

First, some definitions:

## Last Click Source Coding

This is the source code from the last message someone clicked on before their transaction.  It is usually carried through the payment form with a string of characters in the URL, and attached to the transaction record.

Last Click is particularly useful when comparing performance between different messaging strategies and channels.  A/B message testing, or testing between Facebook and Google are good examples where Last Click performance is key.

### Last Click -> Initial Transactions
The subset of last click transactions that are one-time transactions, or the *first* transaction of a recurring transaction.  It is useful to understand the immediate impact of a message.

### Last Click -> Subsequent Transactions
Recurring transactions *after* the first transaction.  This is useful to see how well upsell drives, or recurring transaction messaging is working.  It may take a few months to understand how a particular fundraising drive did on activating your existing membership -- subsequent transactions helps with that understanding.  For clarity, Initial Transactions + Subsequent Transactions=Last Click transactions

## Origin Source Code
One other major attribution component is the *origin* source code.  It represents the *first* occasion an individual has interacted with your organization.

Origin source coding is particularly useful when calculating the long term value of a particular strategy.  It's heavily used when deciding where to spend money to acquire new members, or which partnerships to pursue.

Origin source code is tracked independently of the Last Click source code.  Some source codes may exclusively be origin codes (think of a list acquisition).  Some codes may be exclusively Last click codes (a donation email).  Some source codes may accrue last click transactions, and *also* lead to new people to sign up, in which case they useful for both Last Click and Origin transactions.

## Attribution Models
Coming up with just one source code 'value' number to inform all the possible questions about organizing is a challenging, verging on impossible task.  There are literally thousands of different models in the wild, and they all are variations on how much to credit

Most attribution models strive to *span* all of the transactions once and only once.  It's often deceiving to overcredit transactions -- for example, if you credit a whole $100 transaction to *both* the last click source code, and the origin source code where that person originally came from, you might be running numbers based on raising $200, when in reality you only raised $100.  Because of that, many attribution models use fractional attribution -- so you would credit each responsible source code for *part* of a gift.  That way you can compare apples to apples, and not worry about over-crediting one strategy over another.

For this example, we'll explore 3 different models -- "100% Last Click", "100% Origin", and "50% Adjusted".  The event column shows the interaction, the source code is for that specific interaction, and the model columns show the amount of total money credited to that interaction.

|Date | User interaction | Source Code | 100% Last Click | 100% Origin | 50% Adjusted |
|: -----|: ------------- |:-------------| -----:| -----:|-----:|
|Jan 10, 2019| First Acquired (Origin)  | EMAIL_JAN_2019 | - | $150 | $75 |
|Mar 12, 2019| Clicked on an email    | EM_CAN_456 | - | - | - |
|Jul 09, 2019| Clicked on a Banner ad | BAN_456 | - | - | - |
|Aug 10, 2019| Clicked through a FB Ad, started $50 recurring  | FB_123 | $50 | - | $25 |
|Sep 10, 2019| $50 Recurring  | FB_123 | $50 | - | $25 |
|Oct 10, 2019| $50 recurring  | FB_123 | $50 | - | $25 |
|Total|   |  | $150 | $150 | $150 |

Looking at performance by source code on these different models, we'd get:

|Source Code | 100% Last Click | 100% Origin | 50% Adjusted |
|:-------------| -------:| -----:|-----:|
|FB_123	|$150 | $0 | $75|
|EMAIL_JAN_2019	|$0 | $150 | $75|
|EM_CAN_456	|$0 | $0 | $0|
|BAN_456	|$0 | $0 | $0|

If you're using the first model, Facebook gets all the credit.  If you're using the Origin model, Email Acquisition gets all the credit.  If you're using the 50% adjusted model, they both get *some* credit, but the other interactions are left out to dry.

Frakture currently provides Last Click and Origin performance reporting out of the box.  We believe both models are useful to answer different questions.  We also believe that multiple attribution models are appropriate to many different scenarios, it's up to you to decide the best ones.  We do recommend that any models you derive *span* all the transactions, exactly once, so when you compare performance with that model you don't over-credit multiple sources.


There's millions of variations on how to pick an attribution model.  The best starting point is to know what question you're trying to answer (Best lifetime performance, most immediate impact, most recurring transactions, etc), and then select a model designed to answer that question.
