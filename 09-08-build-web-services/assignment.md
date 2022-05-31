---
slug: 08-build-web-services
id: 5shnvzylcwk2
type: challenge
title: Build Web Services
teaser: Build Web Services
notes:
- type: text
  contents: |-
    That was a gentle introduction to ObjectScript.
    Now let’s use what you’ve learned to build the web services needed to power our coffee roasting business. We will:

    * Copy and compile pre-written code to the database
    * JSON-enable the database tables
    * Examine how each RESTful API is built
    * Deploy and test the web services using curl and the browser
    * Use a web service to move coffee from inventory to the store
    * Record sales
- type: text
  contents: |-
    In part 1 we created database tables using standard SQL.
    What we didn’t mention is that behind the scenes, corresponding ObjectScript classes were created as well!
    This lets developers easily switch between SQL and code depending on which style makes sense for the task at hand.

    ![image](https://dev-start.intersystems.com/wp-content/uploads/2021/03/WebServices-image.png)
tabs:
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
- title: IRIS Terminal
  type: terminal
  hostname: iris
difficulty: basic
timelimit: 500
---
We need to make a few changes to the ObjectScript code that represents our database tables so that we can also output the data as JSON. But first let’s look at the code already in the database.

* In the "VSCode" tab, click on the InterSystems icon to view the ObjectScript Explorer.
This shows you the code that’s been loaded and compiled on the database server, rather than the local version of code you work on.
* Expand the folders `Classes` and `ICO` and you see two files with familiar names, `catalog` and `inventory` (with .cls extensions).
When we created database tables earlier using SQL statements, companion ObjectScript classes were also created at the same time.
* Click on `catalog.cls`. Note that columns are called Properties, but the data type and range restrictions should look familiar. Also look at `inventory.cls`
* Close any files you have opened.

### JSON-enable the Data Tables

We need to change these classes slightly to enable JSON output, and make that output look nice, so let’s do that now.

* Go back to the normal file explorer by clicking the documents icon at the top of the VSCode icon panel.
* Drag `catalog.cls` and `inventory.cls` from `src_Sample/ICO` folder to `src/ICO`.
* Right-click on each file and select "Import and Compile".
This uploads and compiles your new versions of these classes with the addition of %JSON.Adapter and %JSONFIELDNAME.

We did 2 things in these files:
* Extend `%JSON.Adapter` to enable automatic JSON output of this table’s data.
* Add `%JSONFIELDNAME` “property parameters” to selected Properties, to change its name when used in JSON output.