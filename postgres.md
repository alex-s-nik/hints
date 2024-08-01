1. Load data from .sql-file to postgres db which is in docker container
```bash
docker cp ./localfile.sql containername:/container/path/file.sql
docker exec -u postgresuser containername psql dbname postgresuser -f /container/path/file.sql
```
2. Create database over psql shell
```bash
psql -U <username> -c "CREATE DATABASE <db_name>"
psql -U postgres -c "CREATE DATABASE one_more_db"
```
3. Change timezone with console working
```bash
=# set timezone to 'Europe/Moscow'
```
4. Dynamic SQL statements can also be safely constructed using the format function. For example:
```sql
EXECUTE format('UPDATE tbl SET %I = %L '
   'WHERE key = %L', colname, newvalue, keyvalue);
```
%I is equivalent to quote_ident, and %L is equivalent to quote_nullable. The format function can be used in conjunction with the USING clause:
```sql
EXECUTE format('UPDATE tbl SET %I = $1 WHERE key = $2', colname)
   USING newvalue, keyvalue;
```
This form is better because the variables are handled in their native data type format, rather than unconditionally converting them to text and quoting them via %L. It is also more efficient.

[source](https://www.postgresql.org/docs/15/plpgsql-statements.html)

5. Set default value in PostgreSQL table column to a value from a query
Create a function to get the id from the table users with email as an arg. 

```sql
CREATE OR REPLACE FUNCTION id_in_users(iemail varchar) 
RETURNS int LANGUAGE SQL AS $$
   SELECT id FROM users WHERE email = iemail;
$$;
```
And alter the table
```sql
ALTER TABLE runs ADD COLUMN userId bigint NOT NULL DEFAULT     
id_in_users('admin@example.com');
```
[source](https://stackoverflow.com/questions/25378806/set-default-value-in-postgresql-table-column-to-a-value-from-a-query)
