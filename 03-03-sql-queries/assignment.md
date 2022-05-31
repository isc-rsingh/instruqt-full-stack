---
slug: 03-sql-queries
id: iuhf83icltd0
type: challenge
title: SQL database queries
teaser: Let’s make sure the data was inserted
notes:
- type: text
  contents: Let’s check out what we now have in inventory with some SQL queries!
tabs:
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/exp/%25CSP.UI.Portal.SQL.Home.zen?$NAMESPACE=USER&IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
difficulty: basic
timelimit: 900
---
Execute SQL Query
```
select * from ICO.inventory
```
You should see five rows of raw coffee beans in inventory.

Try a couple queries to play with our inventory in more detail. See all large deliveries — over 100 kilograms. You might want to start roasting these first.
```SQL
SELECT * FROM ICO.inventory WHERE quantity_kg > 100
```

Or you may need to see all inventory from a particular vendor.
```SQL
SELECT * FROM ICO.inventory WHERE vendor_id LIKE 'DKE'
```