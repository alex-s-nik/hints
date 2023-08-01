1. Run postgres in Docker on computer
```
docker run --name <container_name> -e POSTGRES_PASSWORD=<postgres_password> -d -p 5432:5432 postgres
docker run --name pg-db -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 postgres
```
