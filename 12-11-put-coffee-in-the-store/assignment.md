---
slug: 11-put-coffee-in-the-store
id: qnoswekskxvk
type: challenge
title: Put coffee in the store
teaser: A short description of the challenge.
notes:
- type: text
  contents: Now let's stock our online store with freshly roasted coffee!
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
In this simple example, the quantity requested doesn’t get recorded anywhere.
We will count on the application making the request to take care of roasting coffee, bagging it and putting it in the store for sale.

Let’s do that now. In the services/samples directory, you’ll find 2 scripts:

* `createproducts.sh`: Creates 5 sample coffee products ready for sale.The first 3 were roasted today,
and the last 2 were roasted 6 days ago. This gives us some relatively stale inventory to discount in the store.
* `loadproducts.sh`: Runs a curl command that iterates through every JSON file in the directory and uses the web
service you just wrote to load the data into ICO.catalog.

Click on the "Terminal" tab, and type:

```
cd /opt/intersystems/src/services/samples
sh createproducts.sh
sh loadproducts.sh
```

If you’re not comfortable running a script you didn’t write yourself (which is smart from a security perspective),
you can manually run your own curl commands to load the data. Here’s an example:

```
curl -X POST -d "@product_brazil_dark.json" \
 -H "Content-Type: application/json" \
 http://iris:52773/api/coffeeco/catalog/catalogproduct
```