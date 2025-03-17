---
title: "Setting Up Turso with Next.js and Prisma"
date: "2024-08-21"
categories: 
  - "tutorial"
coverImage: "nextprisma-thumbnail-1.png"
---

There are two ways which you can use Turso, locally and through a connection

Locally:

```

datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}
```

Once you run, npx prisma generate, your dev.db file should be created and you're ready for local development.

### Through a connection (Turso's db)

In order to do it through a connection we need to install the Turso CLI. Installing the CLI, should be a simple process, with [the official instructions](https://docs.turso.tech/cli/introduction).

#### Understanding the limitations.

"Since libSQL uses HTTP to connect to the remote database, this makes it incompatible with Prisma Migrate. However, you can use [`prisma migrate diff`](https://www.prisma.io/docs/orm/reference/prisma-cli-reference#migrate-diff) to create a schema migration and then apply the changes to your database using [Turso's CLI](https://docs.turso.tech/reference/turso-cli).

"

This messes up the Developer Experience but with most of the work being focused on Drizzle lets be glad that we have workarounds to use Prisma.

We wrote down the migration script which can be found in the [official video](https://youtu.be/YX30LmRip6M?si=YbBULRYV8a6DqBle&t=113) on using Prisma with Turso.

```
npx prisma migrate diff --from-empty --to-schema-datamodel prisma/schema.prisma --script > baseline.sql
```

The above command will create a .sql file called baseline.sql.

Then, we run this command:

```
turso db shell your-database < baseline.sql
```

## Connecting with libraries

The two libraries we need can be downloaded with this command:

```
npm install @libsql/client @prisma/adapter-libsql
```

To push the db, run:

```
npx prisma db push 
```

After all of this your Turso with Next.js and Prisma app should work fine.

## Errors:

"Error: failed to execute SQL:  
error code 401: Not authorized to execute query: DDL statements not permitted on namespace f16a969f-77b1-4020-9701-b595ea037277"

Fix: Be careful so that your are operating db schema, not the db which is a "child db". Again, operate on the schema level db.

## To Conclude,

I would not recommend using Turso with Prisma, it is much better to use Turso with Drizzle.
