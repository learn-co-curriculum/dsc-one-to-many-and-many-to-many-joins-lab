# One-to-Many and Many-to-Many Joins - Lab

## Introduction

In this lab, you'll practice your knowledge of one-to-many and many-to-many relationships!

## Objectives

You will be able to:
* Explain one-to-many and many-to-many joins as well as implications for the size of query results
* Query data using one-to-many and many-to-many joins

## One-to-Many and Many-to-Many Joins
<img src='images/Database-Schema.png' width="600">

## Connect to the Database

Include the relevant imports, then connect to the database located at `data.sqlite`.


```python
import sqlite3
import pandas as pd
```


```python
conn = sqlite3.connect('data.sqlite')
```

## Employees and Their Offices (a One-to-One Join)

Select all of the employees including their first name and last name along with the city and state of the office that they work out of (if they have one). Include all employees and order them by their first name, then their last name.


```python
q = """
SELECT firstName, lastName, city, state
FROM employees
JOIN offices
    USING(officeCode)
ORDER BY firstName, lastName
;
"""
df = pd.read_sql(q, conn)
print('Total number of results:', len(df))
df.head()
```

    Total number of results: 23





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
      <td>Andy</td>
      <td>Fixter</td>
      <td>Sydney</td>
      <td></td>
    </tr>
    <tr>
      <th>1</th>
      <td>Anthony</td>
      <td>Bow</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Barry</td>
      <td>Jones</td>
      <td>London</td>
      <td></td>
    </tr>
    <tr>
      <th>3</th>
      <td>Diane</td>
      <td>Murphy</td>
      <td>San Francisco</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Foon Yue</td>
      <td>Tseng</td>
      <td>NYC</td>
      <td>NY</td>
    </tr>
  </tbody>
</table>
</div>



## Customers and Their Orders (a One-to-Many Join)

Select all of the customer contacts (first and last names) along with details for each of the customers' order numbers, order dates, and statuses.


```python
q = """
SELECT
    contactFirstName,
    contactLastName,
    orderNumber,
    orderDate,
    status
FROM customers
JOIN orders
    USING(customerNumber)
;
"""
df = pd.read_sql(q, conn)
print('Total number of results:', len(df))
df.head()
```

    Total number of results: 326





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



## Customers and Their Payments (Another One-to-Many Join)

Select all of the customer contacts (first and last names) along with details for each of the customers' payment amounts and date of payment. Sort these results in descending order by the payment amount. 


```python
q = """
SELECT
    contactFirstName,
    contactLastName,
    amount,
    paymentDate
FROM customers
JOIN payments
    USING(customerNumber)
ORDER BY amount DESC
;
"""
df = pd.read_sql(q, conn)
print('Total number of results:', len(df))
df.head()
```

    Total number of results: 273





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
      <th>amount</th>
      <th>paymentDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Diego</td>
      <td>Freyre</td>
      <td>120166.58</td>
      <td>2005-03-18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Diego</td>
      <td>Freyre</td>
      <td>116208.40</td>
      <td>2004-12-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Susan</td>
      <td>Nelson</td>
      <td>111654.40</td>
      <td>2003-08-15</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Eric</td>
      <td>Natividad</td>
      <td>105743.00</td>
      <td>2003-12-26</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Susan</td>
      <td>Nelson</td>
      <td>101244.59</td>
      <td>2005-03-05</td>
    </tr>
  </tbody>
</table>
</div>



## Orders, Order Details, and Product Details (a Many-to-Many Join)

Select all of the customer contacts (first and last names) along with the product names, quantities, and date ordered for each of the customers and each of their orders. Sort these in descending order by the order date.

> Note: This will require joining 4 tables! This can be tricky! Give it a shot, and if you're still stuck, turn to the next section where you'll see how to write subqueries that can make complex queries such as this much simpler!


```python
q = """
SELECT
    contactFirstName,
    contactLastName,
    productName,
    quantityOrdered,
    orderDate
FROM customers
JOIN orders
    USING(customerNumber)
JOIN orderdetails
    USING(orderNumber)
JOIN products
    USING (productCode)
ORDER BY orderDate DESC
;"""
df = pd.read_sql(q, conn)
print('Total number of results:', len(df))
df.head()
```

    Total number of results: 2996





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
      <td>Janine</td>
      <td>Labrune</td>
      <td>1962 LanciaA Delta 16V</td>
      <td>38</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Janine</td>
      <td>Labrune</td>
      <td>1957 Chevy Pickup</td>
      <td>33</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Janine</td>
      <td>Labrune</td>
      <td>1998 Chrysler Plymouth Prowler</td>
      <td>28</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Janine</td>
      <td>Labrune</td>
      <td>1964 Mercedes Tour Bus</td>
      <td>38</td>
      <td>2005-05-31</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Janine</td>
      <td>Labrune</td>
      <td>1926 Ford Fire Engine</td>
      <td>19</td>
      <td>2005-05-31</td>
    </tr>
  </tbody>
</table>
</div>



## Summary

In this lab, you practiced your knowledge of one-to-many and many-to-many relationships!
