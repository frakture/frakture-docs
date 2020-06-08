|field|description|source|
|---|---|---|
|amount|||
|id|Unique identifier of the donation, provided by the CRM.|Transaction ID|
|remote_person_id|Unique identifier of the donor constituent, provided by the CRM. (Maps to person table's id/remote_person_id field(s))|Cons ID/Constituent ID/Contact ID|
|remote_transaction_id|Unique identifier of the donation, provided by the CRM.|Transaction ID|
|ts|Timestamp of the gift as provided by the CRM, and normalized by Frakture to UTC|Transaction Date|