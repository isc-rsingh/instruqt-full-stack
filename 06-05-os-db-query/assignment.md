---
slug: 05-os-db-query
id: cs0hpvve8izh
type: challenge
title: ObjectScript database query
teaser: Edit an object with ObjectScript
notes:
- type: text
  contents: |-
    A well-designed system never allows business applications to operate
    directly on the database. Instead, we provide access via services so that we
    can control and monitor the actions taken.
    In the next steps, we build out
    the suite of RESTful web services needed for the business to function.
- type: text
  contents: |-
    With most databases, you have no choice but to use a middleware framework — for example, Java Spring, Python Flask, or Node.js Express, — and talk to the data layer via SQL. You can certainly do that with InterSystems IRIS as well, but you also have another easier and higher performance option:
    * Code in ObjectScript: Get the performance of stored procedures, and the flexibility, power and ease-of-use of a real programming language.
    * No middleware required: The web server and middleware layer are built-in!
- type: text
  contents: Now let’s see how easy it is with ObjectScript, especially when you want
    to get a record using its primary key.
tabs:
- title: IRIS Terminal
  type: terminal
  hostname: iris
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/setup
  port: 8080
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/exp/%25CSP.UI.Portal.SQL.Home.zen?$NAMESPACE=USER&IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
- title: Terminal
  type: terminal
  hostname: vscode
difficulty: basic
timelimit: 500
---
Open IRIS Terminal

Type the following commands to get the ICO.inventory record having a primary key of 1.

Fetches record 1 from the database
```
set item = ##class(ICO.inventory).%OpenId(1)
```

Prints the record’s data to the screen
```
zwrite item
```

Changes a property’s value
```
set item.quantitykg = 300
```

Prints again to verify the change
```
zwrite item
```

Writes changed data to the database
```
do item.%Save()
```