# SQL Basics

This file contains fundamentals of SQL

---


---

### SELECT FROM

```SQL
SELECT *
FROM table_name
```

Use `SELECT DISTINCT` to show unique rows

```SQL
SELECT DISTINCT col_name
FROM table_name
```

### LIMIT

### ORDER BY

### WHERE

### LIKE
```SQL
SELECT *
FROM company_table
WHERE company_name LIKE '%google%'
```

### IN
```SQL
SELECT *
FROM company_table
WHERE company_name IN ('Apple', 'Banana', 'Carrot')
```

### NOT
```SQL
SELECT *
FROM company_table
WHERE company_name NOT IN ('Apple', 'Banana', 'Carrot')
```

### AND
```SQL
SELECT *
FROM orders_table
WHERE order_date >= '2020-01-01' AND order_date <= '2020-12-31'
ORDER BY order_date
```

### BETWEEN
```SQL
SELECT *
FROM orders_table
WHERE order_date BETWEEN '2020-01-01' AND '2020-12-31'
ORDER BY order_date
```
Notes: BETWEEN includes both endpoints

### OR
```SQL
SELECT *
FROM orders_table
WHERE criteria_1 = 0 OR criteria_2 = 0
```

Notes: Use parentheses to group

```SQL
SELECT *
FROM orders_table
WHERE (criteria_1 = 0 OR criteria_2 = 0) AND order_date >= '2020-01-01'
```

### JOIN (Inner Join)
```SQL
SELECT *
FROM orders_table
JOIN accounts_table
ON orders_table.account_id = accounts_table.id
```

Notes: Use `table_name`.`column_name` to specify columns to select

```SQL
SELECT orders_table.order_date, orders_table.transaction_total, accounts_table.customer_email
FROM orders_table
JOIN accounts_table
ON orders_table.account_id = accounts_table.id
```

Notes: multiple tables to join

```SQL
SELECT orders_table.order_date, orders_table.transaction_total, accounts_table.customer_email
FROM orders_table
JOIN accounts_table
ON orders_table.account_id = accounts_table.id
JOIN transaction_table
ON accounts_table.id = transaction_table.account_id
```

### Join (Left Join & Right Join)

After a left join, all data from the left_table will be present in the resulting table.

```SQL
SELECT *
FROM left_table
LEFT JOIN right_table
ON left_table.PK = right_table.FK
```

After a right join, all data from the right_table will be present in the resulting table.

```SQL
SELECT *
FROM left_table
RIGHT JOIN right_table
ON left_table.PK = right_table.FK
```

### Alias

Notes: in the `FROM` or `JOIN` clauses

```SQL
SELECT o.*,
       a.*
FROM orders_table o
JOIN accounts_table a
ON o.account_id = a.id
```

Use `AS`

```SQL
SELECT o.*,
       a.*
FROM orders_table AS o
JOIN accounts_table AS a
ON o.account_id = a.id
```

Give alias to selected columns

```SQL
SELECT o.order_date o_date,
       a.name a_name
FROM orders_table o
JOIN accounts_table a
ON o.account_id = a.id
```

### HAVING

HAVING is used to filter aggregated column

```sql
SELECT a,
       SUM(b)
FROM table
GROUP BY a
HAVING sum(b) >= 1000
```


### DATE_TRUNC

Use `DATE_TRUNC` to truncate detailed time information so that we can use `GROUP BY` to group same days, months, or years.

```sql
SELECT DATE_TRUNC('day', timestamp) AS date,
       SUM(qty) AS sum_qty
FROM table
GROUP BY DATE_TRUNC('day', timestamp)
ORDER BY DATE_TRUNC('day', timestamp)
```

Other parameters: `second`, `day`, `month`, `year`


### DATE_PART

DATE_PART pulls out the specific part of the date

`dow`: day of the week, returning values from 0 (Sunday) to 6 (Saturday)


```sql
SELECT DATE_PART('dow', timestamp)
FROM table
```


### CASE

`CASE WHEN xxx THEN yyy ELSE zzz END`

```sql
SELECT *
       CASE WHEN name = 'GitHub' THEN 'yes' ELSE 'no' END AS is_github
FROM table
```

For multiple conditions

```sql
SELECT *
       CASE WHEN score > 90 THEN 'A'
            WHEN score > 80 THEN 'B'
            WHEN score > 70 THEN 'C'
            WHEN score > 60 THEN 'D'
            ELSE 'F'
            END
            AS grade
FROM table
```

The example below classified the scores into a letter grade, and counts the number of students with that grade

```sql
SELECT CASE WHEN score > 90 THEN 'A'
            WHEN score > 80 THEN 'B'
            WHEN score > 70 THEN 'C'
            WHEN score > 60 THEN 'D'
            ELSE 'F'
            END
            AS grade,
       COUNT(*) AS num_of_students
FROM table
GROUP BY 1
```

### WITH

```sql
WITH supp_table AS (
                    SELECT id, 
                           DATE_TRUNC('year', timestamp)
                    FROM main_table
                    )

SELECT *
FROM main_table
JOIN supp_table
ON main_table.id = supp_table.id

```

### LEFT/RIGHT

To collect a certain of numbers from the left or right side of a string

```sql
SELECT LEFT(phone_number, 3) AS area_code,
       RIGHT(phone_number, 4) AS phone_last_4_digit
FROM table
```

### LENGTH/LOWER/UPPER

Calculate the length of the string/ make the string lower cases or upper cases.

### POSITION/STRPOS

`POSITION('@' IN column_name)` finds the index of `'@'` in the column = column_name

This is the same as calling `STRPOS(column_name, '@')`


### CONCAT/||

Use `CONCAT` or `||` to concatenate string

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM table
```

This is equivalent to 

```sql
SELECT first_name || ' ' || last_name AS full_name
FROM table
```

### Window functions

Running sum of `order_qry` along the entire axis of `order_time`:

```sql
SELECT order_qty,
       SUM(order_qty) OVER (ORDER BY order_time) AS running_total
FROM table
```

Group the `order_time` by months first, and then calcualte the running sum of `order_qry` along the months:


```sql
SELECT order_qty,
       DATE_TRUNC('month', order_time) AS month,
       SUM(order_qty) OVER (PARTITION BY DATE_TRUNC('month', order_time) ORDER BY order_time) AS running_total
FROM table
```

```sql
SELECT id,
       account_id,
       order_time,
       ROW_NUMBER() OVER (ORDER BY order_time) AS row_number
FROM table
```

```sql
SELECT id,
       account_id,
       order_time,
       ROW_NUMBER() OVER (PARTITION BY account_id ORDER BY order_time) AS row_number
FROM table
```

```sql
SELECT id,
       account_id,
       DATE_TRUNC('month', order_time),
       RANK() OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time)) AS row_number
FROM table
```


`DENSE_RANK` doesn't skip rank numbers.
```sql
SELECT id,
       account_id,
       DATE_TRUNC('month', order_time),
       DENSE_RANK() OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time)) AS row_number
FROM table
```

Running counts, runnning average, running minimum, running maximum
```sql
SELECT id,
       account_id,
       DATE_TRUNC('month', order_time),
       COUNT(order_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time)) AS running_counts,
       AVG(order_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time)) AS running_avg,
       MIN(order_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time)) AS running_min,
       MAX(order_qty) OVER (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time)) AS running_max
FROM table
```

Create alias to make the code cleaner
```sql
SELECT id,
       account_id,
       DATE_TRUNC('month', order_time),
       COUNT(order_qty) OVER main_window AS running_counts,
       AVG(order_qty) OVER main_window AS running_avg,
       MIN(order_qty) OVER main_window AS running_min,
       MAX(order_qty) OVER main_window AS running_max
FROM table
WINDOW main_window AS (PARTITION BY account_id ORDER BY DATE_TRUNC('month', order_time))
```

Compare rows to their preceding/following rows.

`lag` pulls previous rows.

`lead` pulls the following rows.
```sql
SELECT account_id,
       order_sum,
       LAG(order_sum) OVER (ORDER BY order_sum) AS lag,
       LEAD(order_sum) OVER (ORDER BY order_sum) AS lead,
       order_sum - LAG(order_sum) OVER (ORDER BY order_sum) AS lag_diff,
       LEAD(order_sum) OVER (ORDER BY order_sum) - order_sum AS lead_diff

FROM (
       SELECT account_id,
              SUM(order_qty) AS order_sum
       FROM orders_table
       GROUP BY 1
       ) sub
```

Percentiles

```sql
SELECT id,
       account_id,
       order_time,
       order_qty,
       NTILE(4) OVER (ORDER BY order_qty) AS quartile,
       NTILE(100) OVER (ORDER BY order_qty) AS percentile
FROM table
ORDER BY order_qty DESC

```
