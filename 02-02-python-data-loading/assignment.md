---
slug: 02-python-data-loading
id: 101uev0fgbmq
type: challenge
title: Python data loading
teaser: Use SQL in a Python script for more flexibility
notes:
- type: text
  contents: |-
    <table style="border: 0px solid;">
      <tr>
        <td style="border: 0px solid;width:67%;vertical-align:top;">
          <p>In this challenge, we will populate the database with raw coffee bean orders, simulating shipments of raw beans from vendors around the world. Assume that all the shipments are consolidated in a single order manifest in JSON format.</p>
          <p>To load the data, we’ll use a Python program to parse the order manifest file and insert the deliveries into the database, also using SQL, but this time within Python.</p>
        </td>
        <td style="border: 0px solid;text-align:right;vertical-align:top;">
          &nbsp;
        </td>
      </tr>
    </table>
tabs:
- title: Terminal
  type: terminal
  hostname: vscode
- title: VSCode
  type: service
  hostname: vscode
  path: /?folder=/opt/intersystems/src/setup
  port: 8080
difficulty: basic
timelimit: 900
---
## Run the inventory import script

In the terminal on the left, run the following commands.

Setup odbc driver
```
sudo odbcinst -i -d -f pyodbc_wheel/odbcinst.ini
```

Execute python script
```
python3 manifest_importer.py
```

## Python script walkthrough

In you are interested in the details of how the script works, click on the VSCode tab and follow along. The <code>manifest_importer.py</code> file should be open for you.

Notice some of the key elements of this script. In the main function definition, we simply import the JSON order manifest file and validate it, checking for the structure needed for the inventory database.
```python
def main():
    with open('./order_manifest.json') as f:
    data = json.load(f)
    data, status, exp = validate_manifest(data)
```
The next thing we do in main() is read database credentials from the file, <code>connection.config</code>.
```python
connection_detail = get_connection_info("connection.config")
ip = connection_detail["ip"]
port = int(connection_detail["port"])
namespace = connection_detail["namespace"]
username = connection_detail["username"]
password = connection_detail["password"]
driver = "{InterSystems ODBC}"
```

Then we set up a connection to the database using an ODBC driver.
```python
connection_string = 'DRIVER={};SERVER={};PORT={};DATABASE={};UID={};PWD={}' \
.format(driver, ip, port, namespace, username, password)
connection = pyodbc.connect(connection_string)
```

If all goes well, we call load_manifest with the JSON data and the database connection object.
```python
msg = load_manifest(data, connection)
```

In load_manifest, we iterate through all the items in the JSON file, inserting each one into the ICO.inventory table we created previously using SQL INSERT statements. Here’s how that works: First, we define our base SQL INSERT statement:
```python
fieldnamesql = "INSERT INTO ICO.inventory (vendor_id, vendor_product_code, quantity_kg, date_arrival)"
```

On the next two lines, we create a new date string based on the current date, for example, ‘2020-06-18’. This will be the date the product arrived in the warehouse.
```python
today = date.today()
mydate = today.strftime("%Y-%m-%d")
```

Now, the code loops through each item object in the JSON file, and uses the data there to construct the VALUES part of our SQL INSERT statement. The result is a completed SQL INSERT statement that looks something like this:
```sql
INSERT INTO ICO.inventory (vendor_id, vendor_product_code, quantity_kg, date_arrival) VALUES (ETRADER, ETHIOPIA32, 200, ‘2020-06-18’)
```

Now the code runs the completed SQL statement. We defined our database cursor on the first line of the function, so now we can run execute on the cursor with the SQL statement as its input.
```python
cursor.execute(valsql)
```