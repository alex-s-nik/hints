1. Load data from .sql-file to postgres db which is in docker container
```
docker cp ./localfile.sql containername:/container/path/file.sql
docker exec -u postgresuser containername psql dbname postgresuser -f /container/path/file.sql
```
