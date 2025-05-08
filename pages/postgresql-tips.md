---
title: PostgreSQL Tips
description: "Please lower your expections of this page. "
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-04-23T02:07:07.345Z
lastmod: 2025-04-23T03:41:14.594Z
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
* [PSQL](#psql)
  * [PSQL Command Line](#psql-command-line)
  * [PSQL Commands](#psql-commands)
  * [Admin Info Queries](#admin-info-queries)
  * [Using Require SSL on Older PSQL versions](#using-require-ssl-on-older-psql-versions)
<!--- cSpell:enable --->

## PSQL

### PSQL Command Line

`psql -e`: ("echo queries")

### PSQL Commands

`\c [STRING]`: \c[onnect] {[DBNAME|- USER|- HOST|- PORT|-] | conninfo}: connect to new database\
`\conninfo`: display information about current connection\
`\l[+]   [PATTERN]`: list databases. If database name is provided, will give stats including size.\
`\d[S+]`: List or describe table,view or sequence. See Informational keys below\
`\dt`: List Tables Only\
`\du[S+] [PATTERN]`: list roles\
`\dn[S+] [PATTERN]`: list schemas\
`\det[+] [PATTERN]`: list foreign tables\
`\dE[+]  [PATTERN]`: list foreign tables but with owner

```text
Informational
  (options: S = show system objects, + = additional detail)
  \d[S+]                 list tables, views, and sequences
  \d[S+]  NAME           describe table, view, sequence, or index
  \da[S]  [PATTERN]      list aggregates
  \dA[+]  [PATTERN]      list access methods
  \db[+]  [PATTERN]      list tablespaces
  \dc[S+] [PATTERN]      list conversions
  \dC[+]  [PATTERN]      list casts
  \dd[S]  [PATTERN]      show object descriptions not displayed elsewhere
  \dD[S+] [PATTERN]      list domains
  \ddp    [PATTERN]      list default privileges
  \dE[S+] [PATTERN]      list foreign tables
  \det[+] [PATTERN]      list foreign tables
  \des[+] [PATTERN]      list foreign servers
  \deu[+] [PATTERN]      list user mappings
  \dew[+] [PATTERN]      list foreign-data wrappers
  \df[antw][S+] [PATRN]  list [only agg/normal/trigger/window] functions
  \dF[+]  [PATTERN]      list text search configurations
  \dFd[+] [PATTERN]      list text search dictionaries
  \dFp[+] [PATTERN]      list text search parsers
  \dFt[+] [PATTERN]      list text search templates
  \dg[S+] [PATTERN]      list roles
  \di[S+] [PATTERN]      list indexes
  \dl                    list large objects, same as \lo_list
  \dL[S+] [PATTERN]      list procedural languages
  \dm[S+] [PATTERN]      list materialized views
  \dn[S+] [PATTERN]      list schemas
  \do[S+] [PATTERN]      list operators
  \dO[S+] [PATTERN]      list collations
  \dp     [PATTERN]      list table, view, and sequence access privileges
  \drds [PATRN1 [PATRN2]] list per-database role settings
  \dRp[+] [PATTERN]      list replication publications
  \dRs[+] [PATTERN]      list replication subscriptions
  \ds[S+] [PATTERN]      list sequences
  \dt[S+] [PATTERN]      list tables
  \dT[S+] [PATTERN]      list data types
  \du[S+] [PATTERN]      list roles
  \dv[S+] [PATTERN]      list views
  \dx[+]  [PATTERN]      list extensions
  \dy[+]  [PATTERN]      list event triggers
  \l[+]   [PATTERN]      list databases
  \sf[+]  FUNCNAME       show a function's definition
  \sv[+]  VIEWNAME       show a view's definition
  \z      [PATTERN]      same as \dp
```

### Admin Info Queries

Database Size: `SELECT pg_size_pretty(pg_database_size('your_database_name'));`. Also see `\l` note in [PSQL Commands](#psql-commands)

Current User: `SELECT current_user`. Also see `\conninfo` note in [PSQL Commands](#psql-commands)

Diskspace used by all databases:

```SQL
SELECT pg_size_pretty(pg_database_size(pg_database.datname)) AS size_in_mb,
pg_database.datname as database_name
FROM pg_database ORDER BY pg_database_size(pg_database.datname) DESC;
```

Foreign tables when in a different schema (not public):\
`\det schema_name.` - dot at the end is required
`\dE schema_name.` - shows owner info unlike above. Dot at the end is required.

### Using Require SSL on Older PSQL versions

`psql` below 9.2 does not accept the URL like syntax like psql `"postgresql://localhost:2345/postgres?sslmode=require"`\

You can use `psql "sslmode=require host=localhost dbname=test"` or similar. You can also use environment variables like [PGSSLMODE](https://www.postgresql.org/docs/8.4/libpq-connect.html#LIBPQ-CONNECT-SSLMODE)

From <https://stackoverflow.com/a/14022480> - also has other great answers on the page.

REF: <https://www.postgresql.org/docs/8.4/app-psql.html>
