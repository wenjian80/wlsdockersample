##[Optional] Build Sample app 
mvn clean package

## Build a docker file
docker build --file Dockerfile.create --force-rm=true -t mywls:v1 .

## Go into bash in weblogic
docker run -it mywls:v1 bash

yum install vim
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]


docker cp mywls:v1:/u01/oracle/user_projects/domains/sample-domain1/config .


docker image rm --force 

/u01/oracle/user_projects/domains/sample-domain1/config

https://github.com/oracle/docker-images/tree/master/OracleWebLogic



docker run -d -p 7001:7001 -p 9002:9002 --name=wlsadmin --hostname wlsadmin -v D:\\1_dockershare\\docker-run:/u01/oracle/properties -e ADMINISTRATION_PORT_ENABLED=true mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startWebLogic.sh
docker run -d --name=managed-server1 --hostname managed-server1 --link wlsadmin:wlsadmin -p 8001:8001 -v D:\\1_dockershare\\docker-run:/u01/oracle/user_projects/domains/sample-domain1/servers/managed-server1/security -v D:\\1_dockershare\\docker-run:/u01/oracle/properties  mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startManagedWebLogic.sh managed-server1 http://wlsadmin:7001 


--commit
C:\WINDOWS\system32>docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
ed37e9e3b9f2        mywls:v1            "/u01/oracle/user_pr…"   5 seconds ago       Up 3 seconds        0.0.0.0:7001->7001/tcp, 0.0.0.0:9002->9002/tcp   wlsadmin

docker exec -it ed37e9e3b9f2 bash
docker commit  ed37e9e3b9f2 mywls:v2

--remove image
docker images
docker rmi

--remove container
container list -a
docker

--run empty


docker ps -a -f status=exited



docker run -d --name=managed-server1 --link wlsadmin:wlsadmin -p 8001:8001 -v D:\\1_dockershare\\docker-run:/u01/oracle/properties -e MANAGED_SERV_NAME=managed-server1 mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startManagedWebLogic.sh


https://www.middlewareinventory.com/blog/weblogic-docker/

http://localhost:9001/console

docker container list -a
docker container rm 
docker container logs <name of the container>


      
