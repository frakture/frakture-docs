# Google Ads

Google Ads are loaded into Frakture using the Message framework - they are separated into Ad Definitions, 
Ad lifetime statistics and Ad by day statistics.

All fields are pulled from Googles Reporting API.

## Ad Definitions and stats

The following **Ad Definition** Fields can be found in both the `<table_prefix>ad_summary` and 
`<table_prefix>ad_summary_by_day` views:

| Frakture Field | Source |
| --- | --- |
| message_id | The Frakture Assigned ID for this Google Ad |
| remote_id | Calculated as: `<Ad id>-<Ad Group Id>-<Campaign Id>` |
| label | Will be the Ad Name, Headline, or Image Name for the Ad |
| publish_date | Will be the date that stats are first available for this Ad |
| ad_type | Will be the type of Ad |

The following *Ad Statistics** Fields can be found in both the `<table_prefix>ad_summary` and 
`<table_prefix>ad_summary_by_day` views:

| Frakture Field | Source |
| --- | --- |
| spend | Google calculated cost |
| conversions | Ad Conversions |
| revenue | Ad Conversion Value |
| conversion_value | Ad Conversion Value |
| impressions | Ad Impressions |
| clicks | Ad Clicks |
| engagements | Ad Engagements |
| interactions | Interactions |

*Note* The `<table_prefix>ad_summary_by_day` will have an addition field, `date` that represents the day the statistic is pulled for.
