
# One to Many and Many to Many Joins
<img src='Database-Schema.png' width=550>


```python
import sqlite3
import pandas as pd
```


```python
conn = sqlite3.connect('data.sqlite')
cur = conn.cursor()
```

# Write a one to one join


```python
#Answers will vary
cur.execute("""select * from customers
                        join employees
                        on (customers.salesRepEmployeeNumber = employeeNumber);""")
df = pd.DataFrame(cur.fetchall())
print('Number of results', len(df))
df.head()
```

    Number of results 100





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
      <th>16</th>
      <th>17</th>
      <th>18</th>
      <th>19</th>
      <th>20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>103</td>
      <td>Atelier graphique</td>
      <td>Schmitt</td>
      <td>Carine</td>
      <td>40.32.2555</td>
      <td>54, rue Royale</td>
      <td></td>
      <td>Nantes</td>
      <td></td>
      <td>44000</td>
      <td>...</td>
      <td>1370</td>
      <td>21000.00</td>
      <td>1370</td>
      <td>Hernandez</td>
      <td>Gerard</td>
      <td>x2028</td>
      <td>ghernande@classicmodelcars.com</td>
      <td>4</td>
      <td>1102</td>
      <td>Sales Rep</td>
    </tr>
    <tr>
      <th>1</th>
      <td>112</td>
      <td>Signal Gift Stores</td>
      <td>King</td>
      <td>Jean</td>
      <td>7025551838</td>
      <td>8489 Strong St.</td>
      <td></td>
      <td>Las Vegas</td>
      <td>NV</td>
      <td>83030</td>
      <td>...</td>
      <td>1166</td>
      <td>71800.00</td>
      <td>1166</td>
      <td>Thompson</td>
      <td>Leslie</td>
      <td>x4065</td>
      <td>lthompson@classicmodelcars.com</td>
      <td>1</td>
      <td>1143</td>
      <td>Sales Rep</td>
    </tr>
    <tr>
      <th>2</th>
      <td>114</td>
      <td>Australian Collectors, Co.</td>
      <td>Ferguson</td>
      <td>Peter</td>
      <td>03 9520 4555</td>
      <td>636 St Kilda Road</td>
      <td>Level 3</td>
      <td>Melbourne</td>
      <td>Victoria</td>
      <td>3004</td>
      <td>...</td>
      <td>1611</td>
      <td>117300.00</td>
      <td>1611</td>
      <td>Fixter</td>
      <td>Andy</td>
      <td>x101</td>
      <td>afixter@classicmodelcars.com</td>
      <td>6</td>
      <td>1088</td>
      <td>Sales Rep</td>
    </tr>
    <tr>
      <th>3</th>
      <td>119</td>
      <td>La Rochelle Gifts</td>
      <td>Labrune</td>
      <td>Janine</td>
      <td>40.67.8555</td>
      <td>67, rue des Cinquante Otages</td>
      <td></td>
      <td>Nantes</td>
      <td></td>
      <td>44000</td>
      <td>...</td>
      <td>1370</td>
      <td>118200.00</td>
      <td>1370</td>
      <td>Hernandez</td>
      <td>Gerard</td>
      <td>x2028</td>
      <td>ghernande@classicmodelcars.com</td>
      <td>4</td>
      <td>1102</td>
      <td>Sales Rep</td>
    </tr>
    <tr>
      <th>4</th>
      <td>121</td>
      <td>Baane Mini Imports</td>
      <td>Bergulfsen</td>
      <td>Jonas</td>
      <td>07-98 9555</td>
      <td>Erling Skakkes gate 78</td>
      <td></td>
      <td>Stavern</td>
      <td></td>
      <td>4110</td>
      <td>...</td>
      <td>1504</td>
      <td>81700.00</td>
      <td>1504</td>
      <td>Jones</td>
      <td>Barry</td>
      <td>x102</td>
      <td>bjones@classicmodelcars.com</td>
      <td>7</td>
      <td>1102</td>
      <td>Sales Rep</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>



# Write a one to many join


```python
#Answers will vary
cur.execute("""select * from payments
                        join customers
                        using(customerNumber);""")
df = pd.DataFrame(cur.fetchall())
print('Number of results', len(df))
df.head()
```

    Number of results 273





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>103</td>
      <td>HQ336336</td>
      <td>2004-10-19</td>
      <td>6066.78</td>
      <td>Atelier graphique</td>
      <td>Schmitt</td>
      <td>Carine</td>
      <td>40.32.2555</td>
      <td>54, rue Royale</td>
      <td></td>
      <td>Nantes</td>
      <td></td>
      <td>44000</td>
      <td>France</td>
      <td>1370</td>
      <td>21000.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>103</td>
      <td>JM555205</td>
      <td>2003-06-05</td>
      <td>14571.44</td>
      <td>Atelier graphique</td>
      <td>Schmitt</td>
      <td>Carine</td>
      <td>40.32.2555</td>
      <td>54, rue Royale</td>
      <td></td>
      <td>Nantes</td>
      <td></td>
      <td>44000</td>
      <td>France</td>
      <td>1370</td>
      <td>21000.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>103</td>
      <td>OM314933</td>
      <td>2004-12-18</td>
      <td>1676.14</td>
      <td>Atelier graphique</td>
      <td>Schmitt</td>
      <td>Carine</td>
      <td>40.32.2555</td>
      <td>54, rue Royale</td>
      <td></td>
      <td>Nantes</td>
      <td></td>
      <td>44000</td>
      <td>France</td>
      <td>1370</td>
      <td>21000.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>112</td>
      <td>BO864823</td>
      <td>2004-12-17</td>
      <td>14191.12</td>
      <td>Signal Gift Stores</td>
      <td>King</td>
      <td>Jean</td>
      <td>7025551838</td>
      <td>8489 Strong St.</td>
      <td></td>
      <td>Las Vegas</td>
      <td>NV</td>
      <td>83030</td>
      <td>USA</td>
      <td>1166</td>
      <td>71800.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>112</td>
      <td>HQ55022</td>
      <td>2003-06-06</td>
      <td>32641.98</td>
      <td>Signal Gift Stores</td>
      <td>King</td>
      <td>Jean</td>
      <td>7025551838</td>
      <td>8489 Strong St.</td>
      <td></td>
      <td>Las Vegas</td>
      <td>NV</td>
      <td>83030</td>
      <td>USA</td>
      <td>1166</td>
      <td>71800.00</td>
    </tr>
  </tbody>
</table>
</div>



# Write a many to many join


```python
#Answers will vary
cur.execute("""select * from orders
                        join payments
                        on (orders.orderDate = payments.paymentDate);""")
df = pd.DataFrame(cur.fetchall())
print('Number of results', len(df))
df.head()
```

    Number of results 118





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10116</td>
      <td>2003-04-11</td>
      <td>2003-04-19</td>
      <td>2003-04-13</td>
      <td>Shipped</td>
      <td></td>
      <td>381</td>
      <td>124</td>
      <td>CQ287967</td>
      <td>2003-04-11</td>
      <td>11044.30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10117</td>
      <td>2003-04-16</td>
      <td>2003-04-24</td>
      <td>2003-04-17</td>
      <td>Shipped</td>
      <td></td>
      <td>148</td>
      <td>424</td>
      <td>LM271923</td>
      <td>2003-04-16</td>
      <td>21665.98</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10123</td>
      <td>2003-05-20</td>
      <td>2003-05-29</td>
      <td>2003-05-22</td>
      <td>Shipped</td>
      <td></td>
      <td>103</td>
      <td>114</td>
      <td>GG31455</td>
      <td>2003-05-20</td>
      <td>45864.03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10124</td>
      <td>2003-05-21</td>
      <td>2003-05-29</td>
      <td>2003-05-25</td>
      <td>Shipped</td>
      <td>Customer very concerned about the exact color ...</td>
      <td>112</td>
      <td>353</td>
      <td>GT878649</td>
      <td>2003-05-21</td>
      <td>16700.47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10125</td>
      <td>2003-05-21</td>
      <td>2003-05-27</td>
      <td>2003-05-24</td>
      <td>Shipped</td>
      <td></td>
      <td>114</td>
      <td>353</td>
      <td>GT878649</td>
      <td>2003-05-21</td>
      <td>16700.47</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
