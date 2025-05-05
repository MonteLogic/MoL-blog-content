---
title: "Work Notes: Run MySQL 8 for UserLAnd for Prisma/Next.js projects"
date: "2023-09-07"
---

i am getting the error

E: Package 'mysql-server' has no installation candidate

Note, I am using Debian instance from UserLAnd.

...

Apparently,

mysql has been replaced by mariadb in Debian10.

So, I ran

i I am getting this error message:

"

ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/run/mysqld/mysqld.sock' (2) debian "mariadb" "UserLAnd"

""

And there's no answer so I'm just going to give up and use SQLite.

Running MySQL and connecting it via connection is just too cumbersome on user land.

so I guess I got to figure out how to use a double run of SQLite and MySQL.

I guess if I had internet I can still like do it good but if I don't have internet I'm going to need to use SQLite.

I couldn't get MySQL 8 to run so I'm going to run SQLite. It would be dope if I could use Bun for this as there as native support for SQLite within Bun.
