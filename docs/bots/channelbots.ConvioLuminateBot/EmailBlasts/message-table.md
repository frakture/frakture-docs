|field|description|source|
|---|---|---|
|from_email|Putative from address assigned to the email's envelope|Sender Email Address|
|from_name|Putative from name assigned to the email's envelope|Sender Name|
|message_id|Frakture-assigned unique ID number of the message (joins to same ID used in message stats tables)|n/a|
|publish_date|Timestamp of the email's send time||
|remote_id|Unique identifier of the email delivery, provided by the CRM (note: delivery, variant, and message are subtly distinct in Luminate and Frakture's hewing to the delivery might introduce apparent reporting discrepancies compared to Luminate A/B test variants)|Delivery ID (dlv_id)|
|subject|Subject line text of the email|Mesage Subject|