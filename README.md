
# One to Many and Many to Many Joins


## Introduction

In this lab, you'll practice your knowledge on one-to-many and many-to-many relationships!

## Objectives 

You will be able to:

* Query data using one-to-many and many-to-many joins
* Predict the resulting size of one-to-many and many-to-many joins


<img src='Database-Schema.png' width=550>

## Connect to the Database


```python
import sqlite3
import pandas as pd
```


```python
conn = sqlite3.connect('data.sqlite')
cur = conn.cursor()
```

## Employees and their Office (a One-to-One join)

Return a list of all of the employees with their first name, last name and the city and state of the office that they work out of (if they have one). Include all employees and order them by their first name, then their last name.


```python
# Your code here
cur.execute("""select firstName, lastName, city, state
                        from employees e
                        join offices o
                        using(officeCode);""")
df = pd.DataFrame(cur.fetchall())
df.columns = [x[0] for x in cur.description]
print('Number of results', len(df))
df.head()
```

    Number of results 23





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>firstName</th>
      <th>lastName</th>
      <th>city</th>
      <th>state</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Diane</td>
      <td>Murphy</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mary</td>
      <td>Patterson</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Jeff</td>
      <td>Firrelli</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>3</th>
      <td>William</td>
      <td>Patterson</td>
      <td>Sydney</td>
      <td></td>
    </tr>
    <tr>
      <th>4</th>
      <td>Gerard</td>
      <td>Bondur</td>
      <td>Paris</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>



## Customers and their Orders (a One-to-Many join)

Return a list of customers first and last names along with each of their order numbers, order dates and statuses.


```python
#Your code here
cur.execute("""select contactFirstName, contactLastName,
                      orderNumber, orderDate, status
                      from customers
                      join orders
                      using(customerNumber);""")
df = pd.DataFrame(cur.fetchall())
df.columns = [x[0] for x in cur.description]
print('Number of results', len(df))
df.head()
```

    Number of results 326





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>contactFirstName</th>
      <th>contactLastName</th>
      <th>orderNumber</th>
      <th>orderDate</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>10123</td>
      <td>2003-05-20</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>10298</td>
      <td>2004-09-27</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>10345</td>
      <td>2004-11-25</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Jean</td>
      <td>King</td>
      <td>10124</td>
      <td>2003-05-21</td>
      <td>Shipped</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Jean</td>
      <td>King</td>
      <td>10278</td>
      <td>2004-08-06</td>
      <td>Shipped</td>
    </tr>
  </tbody>
</table>
</div>



## Orders, Order details and Product Details (a Many-to-Many Join)

Return a list of customer first and last names, product names, quantities, and date ordered for each of the customers and each of their orders. 

Note: This will require joining 4 tables! This can be tricky! Give it a shot, and if you're still stuck, turn to the next section where you'll see how to write subqueries which can make complex queries such as this much simpler!


```python
#Your code here
cur.execute("""select contactFirstName, contactLastName,
                      productName, quantityOrdered, orderDate
                      from customers c
                      join orders o
                      using(customerNumber)
                      join orderdetails od
                      using(orderNumber)
                      join products p 
                      using (productCode);""")
df = pd.DataFrame(cur.fetchall())
df.columns = [x[0] for x in cur.description]
print('Number of results', len(df))
df.head()
```

    Number of results 2996





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>contactFirstName</th>
      <th>contactLastName</th>
      <th>productName</th>
      <th>quantityOrdered</th>
      <th>orderDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>1965 Aston Martin DB5</td>
      <td>26</td>
      <td>2003-05-20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>1999 Indy 500 Monte Carlo SS</td>
      <td>46</td>
      <td>2003-05-20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>1948 Porsche Type 356 Roadster</td>
      <td>34</td>
      <td>2003-05-20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>1966 Shelby Cobra 427 S/C</td>
      <td>50</td>
      <td>2003-05-20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Carine</td>
      <td>Schmitt</td>
      <td>1996 Moto Guzzi 1100i</td>
      <td>39</td>
      <td>2004-09-27</td>
    </tr>
  </tbody>
</table>
</div>



## Summary

In this lab, you practiced your knowledge on One-to-Many and Many-to-many relationships!
