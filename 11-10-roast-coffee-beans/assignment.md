---
slug: 10-roast-coffee-beans
id: wvrajhott0ux
type: challenge
title: Roast coffee beans
teaser: A short description of the challenge.
notes:
- type: text
  contents: |-
    Now that you can get a response from a simple URL request, we know the services are working.

    Let’s operate the coffee business now. First up is to simulate moving raw coffee beans out of inventory and roasting them.

    We’ll use the `/api/coffeeco/inventory/getbeans` API to do this.
tabs:
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/services
  port: 8080
- title: Terminal
  type: terminal
  hostname: vscode
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/UtilHome.csp?IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
- title: IRIS Terminal
  type: terminal
  hostname: iris
difficulty: basic
timelimit: 300
---
In Handler.cls, look at the <Routes> XData section at the end of the file.
See that the Url path `/inventory/getbeans/:id/:quantity` calls the ClassMethod GetRawBeans.
Notice the URL substitution technique to pass values in the URL.

Find the *GetRawBeans* ClassMethod in the file. Since we know the primary key of the bean record (it was passed as the `:id` in the URL),
we can use ObjectScript’s easy way to query the database with the *%OpenId()*. The rest of the method:
* Checks that enough quantity exists
* Decrements the quantity requested from inventory
* Returns the new inventory quantity to the requestor

Let’s run an actual request to get beans out of inventory for roasting.

This request can’t be tested by pasting the URL into a browser because you can’t send POST requests that way, so let’s use curl.

Click on the "Terminal" tab, and type:
```
curl -X POST http://iris:52773/api/coffeeco/inventory/getbeans/1/2.4
```

To get prettier output, pipe the response through [jq](https://stedolan.github.io/jq/):
```
curl -X POST http://iris:52773/api/coffeeco/inventory/getbeans/1/2.4 | jq
```