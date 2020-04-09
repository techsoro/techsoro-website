---
layout: post
title: Permission denied!
subtitle: Postgres users and their permission issue.
tags: [Rails, Postgres]
author: Shekhar Patil
---

Have you ever faced the following issue while fetching records from Postgres in the rails?

**`ActiveRecord::StatementInvalid: PG::InsufficientPrivilege: ERROR:  permission denied for relation`**

I had following configuration in my database.yml file

```
development:
  <<: *default
  database: dev_db_name

staging:
  <<: *default
  database: staging_db_name
  username: staging_db_username
  password: password

test:
  <<: *default
  database: test_db_name
  username: test_db_username
  password: password
```
So while fetching Postgres record from rails console I was getting above mentioned error

Another issue was the rails were not providing the username for which permission error was occurring and I was not sure about the username used while fetching the Postgres record.

To check which user is getting permission error we can check Postgres log file:
If you are using ubuntu the please open following file:

`/var/log/postgresql/postgresql-10-main.log` (log file name can be different as per your Postgres version)

In the log file you will get line similar to the following:

```
2020-04-09 17:24:01.874 IST [25904] root@dev_db_name ERROR:  permission denied for relation
```
Here we can get the username `root@dev_db_name` so `root` user is getting permission denied for the table.

To solve this issue use the following steps:

* Open your Postgres console with the following command:

  `sudo su - postgres` followed by `psql`

* Now use `\du` command to check users and their permissions.

```
postgres=# \du
                                      List of roles
   Role name    |                         Attributes                         | Member of
----------------+------------------------------------------------------------+-----------
 postgres       | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
 root           |                                                            | {}
 shekhar        | Superuser, Create DB, Bypass RLS                           | {}
```
Here we can see root user don't have any permission

Now grant the following permissions to the `root` user.

```
GRANT ALL PRIVILEGES ON DATABASE dev_db_name to root;
postgres=# ALTER USER root WITH SUPERUSER CREATEDB BYPASSRLS;
```
you can read more about the Privileges in PostgreSQL [Here](https://www.digitalocean.com/docs/databases/postgresql/how-to/modify-user-privileges/).

I hope it will solve your problem.
If you still have a problem please feel free to contact me on [email](patilshekhar900@gmail.com) or [twitter](https://twitter.com/Shekharpatil95).
