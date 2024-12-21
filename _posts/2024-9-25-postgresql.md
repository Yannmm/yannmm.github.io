---
layout: post
title: PostgreSQL
tags: rails postgresql
---

> Learn PostgresSQL knowledge bit by bit according to this [roadmap](https://roadmap.sh/postgresql-dba).


# Introcution

**What are Relational Databases?**

> A relational database organizes data into rows and columns, which collectively from a table where the data points are related to each other.

> Data is typically structured across multiple tables, which can be joined together via a primary key or a foreign key. These unique identifiers demonstrate the differrent relationships which exist between tables, and these relationships are usually illustrated through differernt types of data models.

**RDBMS Benefits and Limitations**

> RDBMS offer serveral benefits, including robust data integrity through ACID compliance, powerful querying capabilities, and strong support for data relationship via foreign keys and joins. They are highly scalable vertically(add more power to a machine) and can handle complex transactions reliably. However, RDBMS also have limitations such as difficulties in horizontal scaling (add more machines), which hinders performance in highly distributed systems. They are also less flexible with schema schanges, often requiring significant effort to modify existing structures, and may not be the best fit for unstructured data aor lar-scale, high-velocity data environments typical of some NoSQL solutions.

# RDBMS Concepts

## Object Model in PostgreSQL

> object-oriented models

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

- SELECT
- ORDER BY
- WHERE

- LIMIT
- OFFSET: `SELECT * FROM person OFFSET 5 FETCH FIRST 5 ROW ONLY;`

- IN

- BETWEEN: `SELECT * FROM person WHERE date_of_birth BETWEEN DATE '2000-01-01' AND '2015-01-01';`

- LIKE: `SELECT * FROM person WHERE email LIKE '%___a@%';`

- GROUP BY: `SELECT country_of_birth, COUNT(country_of_birth) FROM person GROUP BY country_of_birth;`

- GROUP BY HAVING: `SELECT country_of_birth, COUNT(country_of_birth) FROM person GROUP BY country_of_birth HAVING COUNT(*) > 5 ORDER BY country_of_birth;`

- [Aggregate Functions](https://www.postgresql.org/docs/17/functions-aggregate.html): Aggregate functions compute a single result from a set of input values.


Sorry I go awry with Calibre, will focus on posgresql again.

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