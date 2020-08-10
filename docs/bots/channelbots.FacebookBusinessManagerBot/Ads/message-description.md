A Frakture Submodule of type **message**. This will pull Ad definitions and by day statistics into your warehouse. Ads refers specifically to the paid advertising you manage through [Facebook Business Manager](https://business.facebook.com/).

The by-date combination of stats and message definition can be found in `<bot_id>_ad_summary_by_date`.

Stat fields that do not have values for any ad (for instance, if you don't have any comments attributed to your ads in the business manager) will _not_ be pulled into the warehouse.
