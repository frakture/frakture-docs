# Using the Warehouse
Enterprise Frakture clients have direct access to a SQL warehouse with all your data.  Typically this is hosted by Frakture (default); however you can also elect to self-host your warehouse.

For each scenario there's a few things you'll want to check.

## Access

### Self-Hosted
FraktureBots need to be able to push data into your warehouse, and adjust and modify the schemas.  Typically this requires the following:
	* Username, password, public domain or IP address, port, database engine (e.g. MySQL, SQLServer) and IP access through any firewalls coming from address 54.83.193.14
	* Create/drop tables, views, and indexes -- Frakture frequently uses intermediate temporary tables for optimized data loads
	* CRUD (create, read, update, delete) for all created table
	* Create and execute stored procedure -- For SQLServer we have a number of scripts to clone tables, and other utilities that we execute as scripts on the server side

It is usually easiest to give administrator rights to a single 'frakture' database on the instance. If you're in a multi-client environment, we recommend one database per client.

#### Self Hosted Performance and Optimization
Storage requirements depend very heavily on the size of the client. A good starting point for configuring new instances is 100GB of storage per client.

Frakture tries to play well with others, and not consume too many resources on the database side.  While most of our queries are optimized, some large data loads can take up to two hours to complete.


### Frakture Hosted
Frakture hosts a separate database per client, and gives access to enterprise users via a username, password, and domain (typically warehouse.frakture.com:3306).


#### Frakture Hosted query optimization
Frakture optimizes the standard queries we use to be very high performance across common use cases.

If you are writing your own queries, or hitting core tables deeper in the warehouse, you will occasionally compose some queries that don't perform well.  Typically this is resolvable with the creation of an extra index or two.  Let our support team know the queries that aren't performing as expected and we'll see if we can help out.

For the benefit of all our customers, Frakture will occasionally kill long running queries (> 1 hour).  If you are attempting some extensive data operations, let our team know -- typically it can be broken down into a custom data flow, or leverage date windowing, to performs better.

> NOTE: Frakture only guarantees the performance of queries that we build.  We can assist with improving third-party queries, or queries generated by third-party reporting tools (e.g. Tableau or Google Data Studio), but often we will recommend pulling data from another table or view.  Being able to write extensive custom SQL queries gives you a lot of rope -- but sometimes just enough to hang yourself.