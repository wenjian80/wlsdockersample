# Sample Wls Docker

## Build simple app
- mvn clean package

## Pull weblogic docker image
- Login to docker hub
- Search for weblogic
- Agree to the agreement and test if you could pull down the docker image
- docker pull store/oracle/weblogic:12.2.1.4-191221

## Docker create
- Look at the contents of Dockerfile.create.
- It is pulling the image, copy the war file and running a wlst script to create a domain
- Examine the contents of model.py wlst
- Run command "docker build --file Dockerfile.create --force-rm=true -t mywls:v1 ."
- Run command "docker images". You will see the docker image being created.

## Start the admin server

- Create a file called domain.properties. Refer to domain.properties
- In docker create a shared directory, Eg in window i place this domain.properties in D:\\1_dockershare\\docker-run
- Run command "docker run -d -p 7001:7001 -p 9002:9002 --name=wlsadmin --hostname wlsadmin -v D:\\1_dockershare\\docker-run:/u01/oracle/properties -e ADMINISTRATION_PORT_ENABLED=true mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startWebLogic.sh"
- Run command "docker ps" to see if the it is running.
- You will see the below
C:\Users\bjlim\Desktop\Kube_Lab\wlsdockersample>docker run -d -p 7001:7001 -p 9002:9002 --name=wlsadmin --hostname wlsadmin -v D:\\1_dockershare\\docker-run:/u01/oracle/properties -e ADMINISTRATION_PORT_ENABLED=true mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startWebLogic.sh
37dc159d29f7c7e9a1657517cd15cc147858ff14ac7de91ef9fb01509ebe8e7a

C:\Users\bjlim\Desktop\Kube_Lab\wlsdockersample>docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
37dc159d29f7        mywls:v1            "/u01/oracle/user_pr…"   9 seconds ago       Up 8 seconds        0.0.0.0:7001->7001/tcp, 0.0.0.0:9002->9002/tcp   wlsadmin

1. [mvn clean package]

2. [Simplified tutorial used during Oracle Open World 2019 as HOL5213](tutorials/domain.home.in.image_oow.md)
(a.k.a. *Domain-home-in-image* version using WebLogic Operator 2.x)
  - Install WebLogic Operator
  - Deploy WebLogic domain on Kubernetes
  - Scale WebLogic Cluster

3. [Simplified tutorial used during Oracle Open World 2019 as HOL5213](tutorials/domain.home.in.image_oow.md)
(a.k.a. *Domain-home-in-image* version using WebLogic Operator 2.x)
  - Install WebLogic Operator
  - Deploy WebLogic domain on Kubernetes
  - Scale WebLogic Cluster



### License ###
Copyright (c) 2019 Oracle and/or its affiliates
The Universal Permissive License (UPL), Version 1.0
