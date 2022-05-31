---
slug: 01-create-db
id: rc49n14ohxmg
type: challenge
title: Databases and SQL
teaser: Database creation with raw SQL
notes:
- type: text
  contents: |-
    <table style="border: 0px solid;">
      <tr>
        <td style="border: 0px solid;width:67%;vertical-align:top;">
          <p>In this tutorial, we’re going to create the basic information management infrastructure for a small manufacturing company. In this case, our company will be roasting, packaging and selling delicious, freshly roasted coffee beans.</p>
          <p>Along the way, you’ll learn how the InterSystems IRIS data platform can serve as the backbone of your IT architecture.</p>
        </td>
        <td style="border: 0px solid;text-align:right;vertical-align:top;">
          <i>always click<br/>this arrow<br/>to continue</i>
        </td>
      </tr>
    </table>
- type: text
  contents: |-
    <table style="border: 0px solid;">
      <tr>
        <td style="border: 0px solid;width:67%;vertical-align:top;">
          <p>You will work through a series of "challenges" that walk you through the process of creating databases, programming RESTful services that interact with those databases, and building a web app UI -- all with a single product -- InterSystems IRIS data platform.</p>
          <p>In the first challenge, we'll create the data tables our coffee company will use.</p>
        </td>
        <td style="border: 0px solid;text-align:right;vertical-align:top;">
          <img src="https://gettingstarted.intersystems.com/wp-content/uploads/2021/03/IrisCoffee-Sketch-part-1.png" width="240">
        </td>
      </tr>
    </table>
- type: text
  contents: |-
    <table style="border: 0px solid;">
      <tr>
        <td style="border: 0px solid;width:67%;vertical-align:top;">
          IRIS Coffee Company has three major divisions in the company:
          <ul>
            <li>the <b>warehouse</b> stores the raw coffee bean inventory. Its data will be in the table <code>ICO.inventory</code></li>
            <li>the <b>roastery</b> roasts the beans, and doesn’t need to store data</li>
            <li>the <b>storefront</b>, where the company sells the roasted coffee. Its data will be in the table <code>ICO.catalog</code></li>
          </ul>
          Let's use the SQL client built into the InterSystems IRIS Terminal to create those two tables using <code>SQL CREATE</code> statements.
        </td>
        <td style="border: 0px solid;text-align:right;vertical-align:top;">
          &nbsp;
        </td>
      </tr>
    </table>
tabs:
- title: IRIS
  type: service
  hostname: iris
  path: /csp/sys/exp/%25CSP.UI.Portal.SQL.Home.zen?$NAMESPACE=USER&IRISUsername=_SYSTEM&IRISPassword=SYS
  port: 52773
difficulty: basic
timelimit: 900
---
Copy and Paste the following SQL CREATE statement in the SQL "Execute Query" box on the left (below the "Execute" button) to create the <code>ICO.inventory</code> table.

Then press the "Execute" button to run the query.

```SQL
CREATE TABLE ICO.inventory
(
  vendor_id VARCHAR(128),
  vendor_product_code VARCHAR(128),
  quantity_kg DECIMAL(10,2),
  date_arrival DATE
)
```

Delete that statement, then copy and paste the following to create the <code>ICO.catalog table</code>.

Press the "Execute" button to run the query.

```SQL
CREATE TABLE ICO.catalog
(
  catalog_id BIGINT IDENTITY,
  product_code VARCHAR(128),
  quantity INTEGER,
  price DECIMAL(10,2),
  time_roasted DATETIME,
  roasting_notes VARCHAR(2048),
  img VARCHAR(2048)
)
```