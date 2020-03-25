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
- Create a file called domain.properties within the folder with the following content:
username=weblogic
password=welcome1

- Run command "docker run -d -p 7001:7001 -p 9002:9002 --name=wlsadmin --hostname wlsadmin -v D:\\1_dockershare\\docker-run:/u01/oracle/properties -e ADMINISTRATION_PORT_ENABLED=true mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startWebLogic.sh"

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
