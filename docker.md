1. Run postgres in Docker on computer
```
docker run --name <container_name> -e POSTGRES_PASSWORD=<postgres_password> -d -p 5432:5432 postgres
docker run --name pg-db -e POSTGRES_PASSWORD=postgres -d -p 5432:5432 postgres
```
2. Delete all containers and images
```
sudo docker stop $(sudo docker ps -a -q)
sudo docker container prune # or sudo docker rm $(sudo docker ps -a -q)
sudo docker image rm $(sudo docker image ls -a -q)
```
3. Run shell into docker container started from Windows Git Bash (this requires a double slash at the bash path)
```
docker run -it <container_name_or_ID> //bin/bash
```
