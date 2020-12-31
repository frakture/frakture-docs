# Frakture Standard Source code metadata

Each source code can encode a great deal of additional information about the solicitation that carried it: to whom was the solicitation targeted, for what purpose was it sent. Frakture provides standard names for common elements that might further describe a source code; our [Level 2](level2/level2_intro) service provides the ability to automate recognition of elements declared by your organization's source code syntax(es) with human visibility and manual overrides.

Apart from the date all source metadata is open-ended text that you're free to use according to your own taxonomies. Suggested entries below are merely that -- suggestions: unless specifically noted there is no menu of preferred or expected choices that are needed to optimize other components of the Frakture infrastructure. If you're best served not by terms like "Holiday Fundraiser" but by shorthand abbreviations or numerical keys, use whatever suits you. The most important thing is to be consistent with these terms across different codes, because reports will break out counts and sums along the axes defined here.

### Account (account_prefix)

An identifier for a specific client; intended for use by agencies and consultants who might service many distinct clients.

### Agency (agency)

The responsible marketing entity. The converse of "Account": it's intended for use when the client has multiple vendors responsible for different projects, such as an ads shop and an email shop.

### Channel (source_code_channel)

Channel for message delivery, such as SMS, Bing Ads, or Direct Mail.

### Source Code Date (source_code_date)

YYYYMMDD format of the source code date. Sometimes different from the core message "publish date", and usually obtained by automatically parsing the source code.

## Primary message hierarchy

Frakture recommends a three-part campaign hierarchy -- Campaign -> Message Set -> Message.  While other elements can also be used for hierarchies, maintaining these three helps with standard roll-up reporting.

### Campaign (campaign)

Name of the messaging campaign. Typically the top-level clustering of many related codes, often deployed over many different channels.

### Message Set (message_set)

Name of the set of messages within a campaign -- the Ad Set in online ads, testing sets for emails, etc.

### Variant (variant)

The specific message variant in a message set.  The exact individual Ad in an AdSet for online ads.

### Channel subtype (subchannel)

More details on the communication channel.

### Media type (media)

Video, text, image, etc. aka MIME type.

### Appeal (appeal)

A specific grouping of content, often used in direct mail.

### Fund (fund)

The funds category this source code feeds, such as Operating Fund, the name of a specific project, differentiating 501(c)3 and 501(c)4, or any other bucket.

### Issue (issue)

Broad issue area.

### Theme (theme)

Broad theme of the message.

### Policy (policy)

Policy area, e.g. Federal/State/International policy.

### Goal (goal)

The descriptive (not numerical) goal of the message, e.g. Advocacy, Fundraising, Retention, Acquisition, or Ticket sales. Commonly used for differentiating conversion performance among different types of digital ads.

### Secondary Goal (goal_2)

Secondary Goal of the message e.g. signups.

### Audience (audience)

Target audience -- for example, Lapsed Donors, or Prospects.

### Targeting Details (targeting)

Any additional targeting details.

### Author (author)

The human credited sender on the from line of an email.

### Signer (signer)

The hopefully-credible person over whose actual or notional "signature" the message appears at the bottom of the letter. Perhaps a member of the organization's senior staff, or perhaps a celebrity endorser, an everyday person with a powerful firsthand experience of the organization's work, or any other voice being tested for messaging impact.

### Partner (partner)

Sending organization, used for list rentals, partnerships, etc

### Organization/Department (department)

Responsible department within the organization.

### Geography (geo)

For use if the message is targeted to a specific locale, a common parameter for digital ads -- e.g. Richmond, or VA, or East Coast.

### Organic/Paid (organic)

Organic or paid message.

### Recurring Campaign Type (recurtype)

Whether this is a recurring campaign effort.

### Additional (additional_info)

Additional info.
