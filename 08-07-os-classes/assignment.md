---
slug: 07-os-classes
id: txkl7pug7nsz
type: challenge
title: ObjectScript Classes
teaser: Writing ObjectScript Classes
notes:
- type: text
  contents: |-
    That wasn’t very pretty because we put a lot of code on a single line.

    Now let’s put our ObjectScript code in a file.
tabs:
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/services
  port: 8080
- title: IRIS Terminal
  type: terminal
  hostname: iris
difficulty: basic
timelimit: 500
---
* Expand src, then ICO.
* Right-click on the ICO folder and select “New File”.
* Name it `Test.cls`.
* In that file, type:

```
Class ICO.Test
{
  ClassMethod QueryDB() As %Status
  {
    set sqlquery = "SELECT * FROM ICO.inventory"
    set rs = ##class(%SQL.Statement).%ExecDirect(,sqlquery)
    while rs.%Next() {
      Write !, rs.%Get("vendor_id")
    }
  }
}
```
* Save the file
* Switch to the "IRIS Terminal" tab and run this command:

```
do ##class(ICO.Test).QueryDB()
```