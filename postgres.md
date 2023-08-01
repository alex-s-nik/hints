1. Load data from .sql-file to postgres db which is in docker container
```
docker cp ./localfile.sql containername:/container/path/file.sql
docker exec -u postgresuser containername psql dbname postgresuser -f /container/path/file.sql
```
2. Create database over psql shell
```
psql -U <username> -c "CREATE DATABASE <db_name>"
psql -U postgres -c "CREATE DATABASE one_more_db"
```
