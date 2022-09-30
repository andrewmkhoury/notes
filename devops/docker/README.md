# Docker
## docker run
* Port (-p)
```
docker run -p 80:80 ...
```
* Port 1 : exposed from docker from your host machine that docker is running on.
* Port 2 : is the port to forward from within the container (the port your application uses).

## Command to open docker shell
docker exec -it `docker ps | tail -1 | awk '{ print $1 }'` /bin/sh
