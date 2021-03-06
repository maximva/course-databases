# Inserting data

## Inserting a single complete row

When inserting a complete row into the table, all fields must be specified in the order in which they appear in the table definition. All columns must be specified. If no value is available for a particular column, the `NULL` value can be used \(If `NULL` is allowed by the table definition\).

Notice that the first value for the `cust_id` is `NULL`. This is possible by the `AUTO_INCREMENT` attribute that is defined for this field.

```sql
INSERT INTO customers
VALUES (
    NULL,
    'Pep E. LaPew',
    '100 Main Street', 
    'Los Angeles',
    'LA',
    '90046',
    'USA',
    NULL,
    NULL
);
```

No output is generated for these kind of queries. The client will tell the amount of affected rows. In this case it is only 1.

```text
Query OK, 1 row affected (0.01 sec)
```

This way of inserting rows is not recommended. A clear knowledge of the table structure is required.

## Inserting a single partial row

To insert a partial row, the column names must be stated explicitly. Columns that are not specified will get the _default_ value. The default value is specified in the table definition.

Notice that `cust_id` is not specified. It won't receive a `NULL` value, because the `AUTO_INCREMENT`attribute is set for this field. It will use an value that is 1 larger than the last used `cust_id`.

```sql
INSERT INTO customers (
    cust_name,
    cust_address,
    cust_city,
    cust_state,
    cust_zip,
    cust_country
)
VALUES (
    'Pep E. LaPew',
    '100 Main Street', 
    'Los Angeles',
    'LA',
    '90046',
    'USA'
);
```

This is a safer way to insert data into an table. It is more verbose, but not all structure of the table must be known to safely insert any data. It is possible to change the order of fields \(columns\) independently from the table structure.

```sql
INSERT INTO customers (
    cust_country,
    cust_state,
    cust_address,
    cust_name,
    cust_city,
    cust_zip
)
VALUES (
    'USA',
    'LA',
    '100 Main Street', 
    'Pep E. LaPew',
    'Los Angeles',
    '90046'
);
```

## Inserting multiple rows

Multiple columns can be inserted at once by adding sets of values, each enclosed within parentheses and separated by commas.

```sql
INSERT INTO customers (
    cust_name,
    cust_address,
    cust_city,
    cust_state,
    cust_zip,
    cust_country
)
VALUES (
    'Pep E. LaPew',
    '100 Main Street', 
    'Los Angeles',
    'LA',
    '90046',
    'USA'
),(
    'M. Martian',
    '42 Galaxy Way', 
    'New York',
    'NY',
    '11213',
    'USA'
);
```

This way of inserting multiple rows improves the performance of the database. It is more efficient than separate INSERT statements.

## Insert the result of a query

Instead of a `VALUES` clause, a `SELECT` clause can be used to insert data from existing data in other tables.

```sql
INSERT INTO customers (
    cust_name,
    cust_address,
    cust_city,
    cust_state,
    cust_zip,
    cust_country
)
SELECT 
    cust_name,
    cust_address,
    cust_city,
    cust_state,
    cust_zip,
    cust_country
FROM custnew;
```

