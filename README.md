
## part 1 exercies 1-8
</br>
basic ones https://github.com/kapistelijaKrisu/docker-xmas-course/edit/master/part1.txt

## 1.8 further instructions

My fall node/react/postgres forum project deployment

##### step 1 create network  
``` docker network create --subnet 172.20.0.0/16 --ip-range 172.20.240.0/20 multi-host-network ```
--ip-range choose yourself. This app needs 2 last word is name of network
##### step 2 setting up postgres
```
docker pull postgres
docker run --rm --name pgw -e POSTGRES_PASSWORD=docker -d -p 5432:5432 --network multi-host-network -v $HOME/Desktop/volumes/postgres:/var/lib/postgresql/data postgres
docker exec -it c5df bash
root@someid:/# psql -U postgres
postgres-# CREATE DATABASE forum;
postgres-# \q
root@someid:/# exit
```
-e for expose, network must match, -v for persisting database, --rm remove when shut down

##### step 3 setting up application
pull image https://cloud.docker.com/repository/docker/kapistelijakrisu/forum-v1/general
build it with simpler tag ``` docker build . -t forum ```
run container ``` docker run --name le-forum -it -p 3003:3003 --network multi-host-network forum ```
network name must match
##### notes
db tables aren't initially set up
schema here https://github.com/kapistelijaKrisu/FullstackForum/blob/master/src/config/db_init.js
