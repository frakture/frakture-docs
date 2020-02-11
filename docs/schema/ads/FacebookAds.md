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
| website_purchases | The number of website purchases attributed to this ad |
| website_purchases_value | The total monetary value of the web_purchases attributed this ad |

*Note* The `<table_prefix>ad_summary_by_day` will have an addition field, `date` that represents the day the statistic is pulled for.
