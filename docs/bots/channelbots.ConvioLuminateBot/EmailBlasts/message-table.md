|field|description|source|
|---|---|---|
|campaign_id|Unique identifier of the message's parent campaign, provided by the CRM|Campaign ID|
|from_email|Putative from address assigned to the email's envelope|Sender Email Address|
|from_name|Putative from name assigned to the email's envelope|Sender Name|
|message_id|Frakture-assigned unique ID number of the message (joins to same ID used in message stats tables)|n/a|
|publish_date|Timestamp of the email's send time||
|remote_id|Unique identifier of the email delivery, provided by the CRM (note: variant, delivery, and message are subtly distinct in Luminate and Frakture's totaling at the delivery level might introduce apparent reporting discrepancies compared to Luminate A/B test variants)|Delivery ID (dlv_id)|
|subject|Subject line text of the email|Mesage Subject|

Stats Fields

|field|description|source|
|---|---|---|
|email_clicked||Click-Throughs|
|email_delivered||Emails Delivered|
|email_total_clicks||Total Click-Throughs|
|email_unsubscribes||Unsubscribes (Opt-Outs)|
|impressions||Recipient Opens|
|luminate_delivery_forwarded_opens||Forwarded Opens|
|luminate_delivery_recipient_opens||Recipient Opens|
|luminate_delivery_soft_bounces||Soft Bounces|