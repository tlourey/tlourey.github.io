---
title: PostgreSQL Tips
description: "Please lower your expections of this page. "
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-23T02:07:07.345Z
lastmod: 2025-04-23T02:17:39.691Z
tags:
    - Azure_Databases
    - Databases
    - PostgreSQL
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Using Require SSL on Older PSQL versions](#using-require-ssl-on-older-psql-versions)
<!--- cSpell:enable --->

## Using Require SSL on Older PSQL versions

`psql` below 9.2 does not accept the URL like syntax like psql `"postgresql://localhost:2345/postgres?sslmode=require"`\

You can use `psql "sslmode=require host=localhost dbname=test"` or similar. You can also use environment variables like [PGSSLMODE](https://www.postgresql.org/docs/8.4/libpq-connect.html#LIBPQ-CONNECT-SSLMODE)

From <https://stackoverflow.com/a/14022480> - also has other great answers on the page.

REF: <https://www.postgresql.org/docs/8.4/app-psql.html>

<!-- cSpell:ignore toolname -->
<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
