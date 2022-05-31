---
slug: 06-db-query
id: yl5kgs1or3ul
type: challenge
title: Database query with ObjectScript and SQL
teaser: Database query with ObjectScript and SQL
notes:
- type: text
  contents: |-
    Let’s perform a more complex query using SQL right in your ObjectScript code.

    Continue using IRIS Terminal
tabs:
- title: IRIS Terminal
  type: terminal
  hostname: iris
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/services
  port: 8080
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/UtilHome.csp?IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
- title: Terminal
  type: terminal
  hostname: vscode
difficulty: basic
timelimit: 500
---
Type in IRIS Terminal:

Sets a variable with a valid SQL SELECT statement
```
set sqlquery = "SELECT * FROM ICO.inventory ORDER BY vendor_id"
```

Executes the SELECT and stores a pointer to results in `rs`
```
set rs = ##class(%SQL.Statement).%ExecDirect(,sqlquery)
```

Iterates over `rs`, printing the `vendor_id` property
```
while rs.%Next() { Write !, rs.%Get("vendor_id") }
```