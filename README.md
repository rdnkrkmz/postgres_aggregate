# PostgreSQL Custom Aggregate
This is a custom aggregate extension for PostgreSQL

### 
The aggregate function returns a text formatted like: max -> min for an integer column, where min and max are minimum and maximum values of that column.

### Installation
```
git clone https://github.com/rdnkrkmz/postgres_aggregate.git
cd postgres_aggregate
make installcheck
```


### Supported data types
```
numeric, integer, float
char, varchar, text
date, time, timestamp
```

### Examples
-- 1. case: task's required case, without explicitly telling delimiter
```
select max_to_min(val) from (values(5),(3),(6),(7),(9),(10),(7)) t(val);
```
-- 1.1. case: task's required case, wit explicitly telling delimiter
```
select max_to_min(val, ' =8> ') from (values(5),(3),(6),(7),(9),(10),(7)) t(val);
```
-- 2. case: numeric, integer, float types together and some rows are null
```
select max_to_min(val, ' => ') from (values(5.0),(-6.9),(6),(7),(99.9),(11), (null),(7)) t(val);
```


-- 3. case: char, varchar, text
```
select max_to_min(val, ' => ') from (values('a'),('b'),('c'),('d'),('e'),('f'), (null),('g')) t(val);

-- 4. case: timestamp with time zone
select max_to_min(val, ' => ') from (
    values
	(to_timestamp('2023-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone),
    (to_timestamp('2022-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone),
    (to_timestamp('2021-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone),
    (to_timestamp('2020-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone),
    (to_timestamp('2019-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone),
    (to_timestamp('2018-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone),
    (null),
    (to_timestamp('2017-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp with time zone)
) t(val);


-- 5. case: timestamp without time zone
select max_to_min(val, ' => ') from (
    values
	(to_timestamp('2023-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone),
    (to_timestamp('2022-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone),
    (to_timestamp('2021-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone),
    (to_timestamp('2020-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone),
    (to_timestamp('2019-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone),
    (to_timestamp('2018-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone),
    (null),
    (to_timestamp('2017-10-20 10:11:00', 'yyyy-mm-dd hh24:mi:ss')::timestamp without time zone)
) t(val);


-- 6. case: date
select max_to_min(val, ' => ') from (
    values
	(to_timestamp('2023-10-20', 'yyyy-mm-dd')),
    (to_timestamp('2022-10-20', 'yyyy-mm-dd')),
    (to_timestamp('2021-10-20', 'yyyy-mm-dd')),
    (to_timestamp('2020-10-20', 'yyyy-mm-dd')),
    (to_timestamp('2019-10-20', 'yyyy-mm-dd')),
    (to_timestamp('2018-10-20', 'yyyy-mm-dd')),
    (null),
    (to_timestamp('2017-10-20', 'yyyy-mm-dd'))
) t(val);
```
