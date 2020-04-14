# Frakture Documentation

Frakture delivers an army of digital Bots designed to help organizations gather and use their data, regardless of the platform that data lives on.  Frakture focuses heavily on marketing and sales operations, including People/Contacts, monetary Transactions, and Messaging (social media, email, direct mail, etc).


## [Extract Transform Load (aka ETL)](etl/ "Extract, Transform, Load")

Frakture's core features start with ETL.  Every night, our Bots connect to hundreds of different platforms (such as CRMs, email platforms, social media, etc), execute tens of thousands of jobs, and Extract tens of millions of records using the best mechanism available for any given platform.  They then Transform that data into the common Frakture schema, standardizing field names, parsing out messaging information, converting timestamps, etc.  Once completed, they Load that data into the client's data warehouse (if self-hosting), or into Frakture's warehouse (if Frakture hosted).

[Read More](etl/ "Extract, Transform, Load")

## [Enrichment](enrichment/ "Data enrichment")

In order to make the information more useful for reporting and analysis, Frakture enriches the data pulled from platforms,  adding data to support deduplication and identity, conversion tracking, attribution models, and more.

Frakture also creates convenient views of the data to make the large amounts of data more accessible to reporting suites and engineers -- to minimize the amount of work needed to access the data.

[Read More](enrichment/ "Data enrichment")

## [Delivery](delivery/ "Delivery Options")

Frakture delivers the data using multiple mechanisms:

* Database teams can access the raw data directly, and append their own data or processes on top.
* 3rd party reporting suites (such as Google Data Studio or Tableau) can connect directly into the warehouse, to build charts and graphs customized to the client.
* Frakture also provides a standard suite of reports suitable for non-technical people to use
* Frakture can push people and transaction data into other platforms, which can accommodate many integration needs
* Frakture can automatically push cross-channel targeting groups into ad platforms such as Google and Facebook


[Read More](delivery/ "Delivery Options")
