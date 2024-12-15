---
layout: post
title: PostgreSQL
tags: rails postgresql
---

### PostgreSQL Server Applications

- `postgres`: PostgreSQL database server.
  - The postgres server application itself.
- `pg_ctl`:  initialize, start, stop, or control a PostgreSQL server.
  - pg_ctl is a utility for initializing a PostgreSQL database cluster, starting, stopping, or restarting the PostgreSQL database server (postgres), or displaying the status of a running server.
- `initdb`: create a new  PostgreSQL database cluster.
  - A database cluster is a collection of databases that is stored at a common file system location (the “data area”). More than one postgres instance can run on a system at one time, so long as they use different data areas and different communication ports. When postgres starts it needs to know the location of the data area. The location must be specified by the -D option or the PGDATA environment variable; there is no default.

**Environment**

- PGDATA: Default data directory location.
- PGPORT: Default port number.

### PostgreSQL Client Applications

- `psql`: PostgreSQL interactive terminal.

**General Commands**

- `\?`: show general help.
- `\l`: list databases.
- `\d`: list tables, views, and sequences.

**SQL Commands**

- `\h`: show sql commands.


### Why


watching this tutorial: https://www.youtube.com/watch?v=qw--VYLpxG4

run command in postgres docker container: https://www.commandprompt.com/education/how-to-useexecute-postgresql-query-in-docker-container/#:~:text=To%20use%2Fexecute%20PostgreSQL%20Query%20in%20Docker%20container%2C%20first%2C,postgres”%20command.


PostgreSQL uses a client/server model. Once the server is running, The PostgreSQL server can handle multiple concurrent connections from clients.

TBD

### What



### How

- We should ask locally running psql server to handle all in-development client. Rather than create psql server for each client.

### Where


### When



**References**:

- psql tutorial: https://www.postgresql.org/docs/current/tutorial.html

- [PostgreSQL Server Applications](https://www.postgresql.org/docs/current/reference-server.html)
- [PostgreSQL Data Types](https://www.postgresql.org/docs/17/datatype.html)
- [Mockagroo](https://www.mockaroo.com)