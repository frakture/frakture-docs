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
|email_ecommerce_purchases||eCommerce Purchases|
|email_ecommerce_purchase_amount||eCommerce Purchase Amount($)|
|email_forwarded_actions||Forwarded Actions|
|email_forwarded_click_count||Forwarded Click-Throughs|
|email_forwarded_open_count||Forwarded Opens|
|email_hard_bounces||Hard Bounces|
|email_opened|Opens by the primary recipient pool|Recipient Opens|
|email_open_count|Sum of primary and forwarded opens|Total Opens|
|email_registrations||Registrations|
|email_rsvps||RSVPs|
|email_sent||Emails Sent aka Total Recipients|
|email_soft_bounces||Soft Bounces|
|email_spam_complaints||Spam Complaints|
|email_surveys_taken||Surveys Taken|
|email_teamraiser_registrations||Teamraiser Registrations|
|email_tell_a_friend_forwards||TellAFriend Forwards|
|email_tell_a_friend_forward_recipients||TellAFriend Forward Recipients|
|email_ticket_purchases||Ticket Purchases|
|email_total_clicks||Total Click-Throughs|
|email_unsubscribes||Unsubscribes (Opt-Outs)|
|impressions||Recipient Opens|
|luminate_delivery_forwarded_opens|Opens by the non-recipients who received the email "secondhand" via a forward or re-post|Forwarded Opens|
|luminate_delivery_recipient_opens||Recipient Opens|
|luminate_delivery_soft_bounces||Soft Bounces|