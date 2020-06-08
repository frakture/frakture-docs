|field|description|source|
|---|---|---|
|amount|Amount of the transaction|Net Transaction Amount|
|frequency|If a recurring gift, the frequency with which the charge repeats (most commonly "Monthly")|Frequency|
|id|Unique identifier of the transaction, provided by the CRM|Transaction ID|
|initial_gift_id|If a recurring gift, the transaction ID of the gift that initiated the series|Initial Gift ID|
|remote_person_id|Unique identifier of the donor or purchaser, provided by the CRM (joins to person table's id/remote_person_id field(s))|Cons ID/Constituent ID/Contact ID|
|remote_transaction_id|Unique identifier of the transaction, provided by the CRM|Transaction ID|
|source_code|Source code assigned the transaction in the CRM|Source Code Text|
|ts|Timestamp of the transaction as provided by the CRM, and normalized by Frakture to UTC|Transaction Date|