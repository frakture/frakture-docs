# Frakture Standard Source code metadata

Each source code can have arbitrary amounts of information embedded in it.  Frakture provides standard names for common elements of a source code, so

### Account ID (account_prefix)
An identifier for a specific client.

### Channel (source_code_channel)

Specific channel pulled out of the source code.  When pulling message out of a platform, Frakture also maintains information on that level, but the source_code_channel is channel information pulled completely from the source code.

### Source Code Date (source_code_date)

YYYYMMDD format of the source code date.  Sometimes different than the core message "publish date", as it relies completely on the parsing of the source code and no other information.

## Primary message hierarchy
Frakture recommends a 3-part campaign hierarchy - Campaign -> Message Set -> Message.  While other elements can also be used for hierarchies, maintaining these three helps with standard roll-up reporting.

### Campaign (campaign)

Name of the messaging campaign.  Typically the top level grouping of campaigns, often is cross-channel (email, ads, etc).

### Message Set (message_set)

Name of the set of messages within a campaign -- the Ad Set in online ads, testing sets for emails, etc.

### Variant (variant)

The Specific message variant in a message set.  The Ad in an AdSet for online ads

### Channel subtype (subchannel)

More details on the communication channel

### Media type (media)

Video, text, image, etc. aka MIME type

### Appeal (appeal)

A specific grouping of content, often used in direct mail.

### Fund (fund)

The fund or bank account this message is targeted to, C3/C4, operating fund, etc.

### Issue (issue)

Broad issue area -- advocacy

### Theme (theme)

Broad theme of the message

### Policy (policy)

Policy area, e.g. Federal/State/International policy

### Goal (goal)

Primary goal of the message.  In digital ads this is related to how you want to calculate conversions, etc.
e.g. Advocacy, Fundraising, Retention, Acquisition, Ticket sales

### Secondary Goal (goal_2)

Secondary Goal of the message e.g. signups, etc.

### Audience (audience)

Target audience -- for example, High donors, likeley customers, etc.

### Targeting Details (targeting)

More targeting details

### Author (author)

The human credited sender of the message - John Smith, Mary Jane

### Signer (signer)

The human at the bottom of the letter -- often a celebrity -- ‚'Prince','Gandhi','The Rolling Stones', etc.

### Agency (agency)

The responsible marketing agency

### Partner (partner)

Sending organization, used for list rentals, partnerships, etc

### Organization/Department (department)

Responsible department within the organization

### Geography (geo)

Target geography -- e.g. MA,MS,VA, or East Coast, etc

### Organic/Paid (organic)

Organic or paid message

### Recurring Campaign Type (recurtype)

If this is a recurring campaign effort, please select from the following options

### Additional (additional_info)

Additional info
