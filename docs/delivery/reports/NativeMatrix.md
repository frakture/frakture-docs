## Definitions - data sources

### Static Files
Excel files, CSV files, FTP files all fall under the Static File data class.  Static files will typically contain lists of people or transactions, are pulled only periodically (once a day is common).  They may have campaign or source code information in them, but that depends on the provider.

### Limited API
*Limited* APIs provide a small set of highly specific data, but are often quite limited.  Examples of Limited APIs would be "Pulling people data, but without filtering by date modified", "Pulling some transaction data, but not source codes", Pulling some messaging data.  Each limited platform has different restrictions on their API - if it exists at all.  Contact Frakture to determine which class of data access your system has.

### Standard API
A Standard API allows retrieval of people, messaging, and transaction data with high limits, at reasonable costs, filtered by last modified date.  Most modern payment processors, social media tools (Facebook/Google/etc), and many CRMs provide standard API interfaces.  Unfortunately some systems that would otherwise qualify as a Standard API provide strict volume caps, or charge heavily for data access, and thus fall under a Limited API.  Most platforms that use webhooks would qualify as a Standard API, particularly if those webhooks can be backdated.

### Full, Bulk API
Full APIs allow querying of every element of data in the system, with high enough limits for heavy use.  Direct SQL access, or bulk APIs (such as the Salesforce Bulk API) fall under this category.  Even with a Full API, some systems do not track every interaction, so there is still some limits depending on the platform.  As a rule, though, try to ensure that any platform you choose has Full Bulk API access -- it's your data, you should be able to get to it.

## Definitions - Source Coding
Much of the value of reports comes down to how well the data has been coded coming in.  While you can derive some insights from untreated data, you can develop much better insights when you source code your data.  See [Conversion methods](enrichment/conversions "Conversion overview") for more information on source coding.

### No source coding
Very limited coding has been done in signup or transaction links.  Reporting tends to be limited to aggregate numbers, and is difficult to break out by source channel, or source campaign.  Origin performance -- performance about the first interaction of a person -- is basically nonexistent.

### Legacy/Limited Source coding
Source coding has been happening consistently, however the structure of the source code isn't well defined.  This can happen from poor source code design, or where there are numerous legacy source codes.  In this situation, you can report on where and when people originally came from, and have a limited ability to attribute performance to source messages and channels, but cannot slice performance by campaign or any deeper.

### Extended Source Coding
Source codes are extensive and high quality.  There are elements in the source code for 3-10 different pieces of data, and almost every person or transaction that comes in has a code.  This is the best situation for quality reporting, and leads to highly detailed, informative reports that can be sliced by channel, by campaign, by source -- any number of different ways.  The complexity of the source code defines how deep you can go, but generally if you have high source coding parsing rates you get the best reports.


## General class of available reports
|   	|Static Files   	| Limited API  	| Standard API  	|  Full, Bulk API	|
|---	|---	|---	|---	|---	|
|No coding   	| Top line People and Fundraising  	|  Total People, Transactions, Messaging 	|  Total People, Transactions, Messaging over time 	|  All People, Transactions, Messaging,Interactions 	|
|Legacy/Limited Source coding   	|  + Origin performance 	|  + Origin performance 	|  + Origin performance 	|  + Origin performance 	|
|Extended Source Coding   	|  + Performance by channel/campaign 	|  + Performance by channel/campaign 	|  + Performance by channel/campaign 	|  + Performance by channel/campaign 	|
