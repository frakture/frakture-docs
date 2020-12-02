# Warehouse Access

Most Frakture users won't need to worry about warehouse access, as Frakture will set up and host your data warehouse as part of our service contract.

If you're hosting your own data warehouse, however, you'll need to set up a user with a broad grant of permissions.

* Create/drop tables, views, and indexes
* CRUD (create, read, update, delete) for all created tables
* For SQL Server databases, we'll also need to be able to create and execute stored procedures

We'll use this Frakture user to pipe all our data processes into your warehouse. The bots will only operate only on Frakture's tables.) Frakture can serve most widely used databases such as MySQL, SQL Server, Oracle, and Postgres.

Once you have a user set up, you'll need to give us this information:

* Hostname (either a URI or an IP address)
* Port
* Database Name
* The username you've given us
* Its associate password

Please do not send this sensitive login information in plaintext email; we recommend using a service such as [One Time Secret](https://onetimesecret.com) or [Saltify](https://saltify.io) to generate a secure, password-protected link and share that with your Frakture contact. Be sure to whitelist the Frakture bots' IP address (54.83.193.14) in any firewalls that govern access to the database in question.

For deeper detail on self-hosting, see [here](delivery/warehouse/ "Warehouse") or reach out to us at _support (at) frakture.com_.
