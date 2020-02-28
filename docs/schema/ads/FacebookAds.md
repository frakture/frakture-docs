# Facebook Business Manager Ads

Facebook Business Manager Ads are loaded into Frakture using the Message framework - they are separated into Ad Definitions,
Ad lifetime statistics and Ad by day statistics.

All fields are pulled from the FB Business Manager API.

## Ad Definitions and stats

The following **Ad Definition** Fields can be found in both the `<table_prefix>ad_summary` and
`<table_prefix>ad_summary_by_day` views:

| Frakture Field | Source |
| --- | --- |
| message_id | The Frakture Assigned ID for this Facebook Ad |
| remote_id | Calculated as: `<Ad id>` |
| label | Will be the Label of the Facebook Ad |
| publish_date | Will be the date the Ad was created |

The following *Ad Statistics** Fields can be found in both the `<table_prefix>ad_summary` and
`<table_prefix>ad_summary_by_day` views:

| Frakture Field | Source |
| --- | --- |
| transactions | Count of fb_pixel_purchase stats (number of transactions)|
| revenue | Sum of the amount of fb_pixel_purchase stats (dollar value of transactions) |
| website_purchases | Total count of offsite conversion fields, e.g. offsite_conversion.fb_pixel_custom, fb_pixel_initiate_checkout,fb_pixel_purchase,<custom conversion fields> |
| website_purchases_value | Summed value of all offsite conversion fields, e.g. offsite_conversion.fb_pixel_custom, fb_pixel_initiate_checkout,fb_pixel_purchase,<custom conversion fields> |

*Note* The `<table_prefix>ad_summary_by_day` will have an addition field, `date` that represents the day the statistic is pulled for.
