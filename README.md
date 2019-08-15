
# One-to-Many and Many-to-Many Joins - Lab

## Introduction

In this lab, you'll practice your knowledge on one-to-many and many-to-many relationships!

## Objectives

You will be able to:
- Query data using one-to-many and many-to-many joins
- Predict the resulting size of one-to-many and many-to-many joins

## One-to-Many and Many-to-Many Joins
<img src='images/Database-Schema.png' width="600">

## Connect to the Database


```python
#Your code here
```

## Employees and their Office (a One-to-One join)

Return a dataframe with all of the employees including their first name and last name along with the city and state of the office that they work out of (if they have one). Include all employees and order them by their first name, then their last name.


```python
#Your code here
```

## Customers and their Orders (a One-to-Many join)

Return a dataframe with all of the customers' first and last names along with details for each of their order numbers, order dates, and statuses.


```python
# Your code here
```

## Customers and their Payments (another One-to-Many join)

Return a dataframe with all of the customers' first and last names along with details about their payments' amount and date of payment. Sort these results in descending order by the payment amount.


```python
# Your code here
```

## Orders, Order details and Product Details (a Many-to-Many Join)

Return a dataframe with all of the customers' first and last names along with the product names, quantities, and date ordered for each of the customers and each of their orders. Sort these in descending order by the order date.

- Note: This will require joining 4 tables! This can be tricky! Give it a shot, and if you're still stuck, turn to the next section where you'll see how to write subqueries which can make complex queries such as this much simpler!


```python
# Your code here
```

## Summary

In this lab, you practiced your knowledge on one-to-many and many-to-many relationships!
