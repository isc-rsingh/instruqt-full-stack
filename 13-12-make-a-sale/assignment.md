---
slug: 12-make-a-sale
id: upshsecwfgt4
type: challenge
title: Make a sale
teaser: A short description of the challenge.
notes:
- type: text
  contents: |-
    Our final service, `SellProduct`, records coffee sales. It takes as input the product ID and the quantity of bags being sold.

    This is extremely simplified, as we won’t do any error checking or special payment handling or shipping. We’ll just decrement the catalog’s quantity of coffee bags, assuming everything else is taken care of on the front end. We also will assume if the customer bought multiple products, the client will send a SellProduct request for each.
tabs:
- title: Terminal
  type: terminal
  hostname: vscode
difficulty: basic
timelimit: 300
---
Look at the `SellProduct` ClassMethod.

Just like we did in the `GetRawBeans` method, we’ll take advantage of ObjectScript’s convenience methods for querying records when you know their ID: `%ExistsId`, `%OpenId`, and `%Save`. Since this method is so similar to `GetRawBeans`, there’s nothing new to explain.

### Try out the services
Query for fresh products:
```
curl http://iris:52773/api/coffeeco/catalog/getproducts | jq
```

Query for stale:
```
curl http://iris:52773/api/coffeeco/catalog/getproducts/0 | jq
```

Try selling products:
```
curl -X POST http://iris:52773/api/coffeeco/catalog/sellproduct/1/2 | jq
```

The response should look similar to this.
```
{
  "catalog_id": 1,
  "product_code": "BRAZILDARK",
  "quantity": 38,
  "price": 13.99,
  "time_roasted": "2021-02-03T09:00:00Z",
  "roasting_notes": "Full bodied and low acidity. Thick, creamy, nutty and semi-sweet.",
  "img": "brazil_dark.jpg"
}
```