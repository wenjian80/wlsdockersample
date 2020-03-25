# Sample Wls Docker domain creation using wlst.

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
- Run command 
> docker build --file Dockerfile.create --force-rm=true -t mywls:v1 .
- Run command. You will see the docker image being created.
> docker images  

## Start the admin server

- Create a file called domain.properties. Refer to domain.properties
- In docker create a shared directory, Eg in window i place this domain.properties in D:\\1_dockershare\\docker-run
- Run command 
> docker run -d -p 7001:7001 -p 9002:9002 --name=wlsadmin --hostname wlsadmin -v D:\\1_dockershare\\docker-run:/u01/oracle/properties -e ADMINISTRATION_PORT_ENABLED=true mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startWebLogic.sh
- Run command to see if the it is running.
> docker ps -a 
- Access the console http://localhost:7001/console and logic via weblogic/welcome1 as defined in domain.properties
- Run command, example "docker exec -it 37dc159d29f7 bash" to go into the container. 
> docker exec -it [container id when you have run docker ps] bash
- You can make changes to the files system and do a commit to a different version. Example command 
> docker commit 37dc159d29f7 mywls:v2
- For example you can go into the console create a new cluster make changes and then commit. This is not recommended as the changes should be done in wlst.
- Stop the container 
> docker stop 37dc159d29f7
- See log of container 
> docker container logs 37dc159d29f7
- Remove container 
>docker container rm  37dc159d29f7


## Start the managed server
- Make sure your admin server is already up and running. Refer to previous steps.
- Create a file boot.properties. Refer to domain.properties
- In docker create a shared directory, Eg in window i place this boot.properties in D:\\1_dockershare\\docker-run
- Run command 
> docker run -d --name=managed-server1 --hostname managed-server1 --link wlsadmin:wlsadmin -p 8001:8001 -v D:\\1_dockershare\\docker-run\\ms1:/u01/oracle/user_projects/domains/sample-domain1/servers/managed-server1/security  mywls:v1 /u01/oracle/user_projects/domains/sample-domain1/bin/startManagedWebLogic.sh managed-server1 http://wlsadmin:7001
- Go to weblogic console. http://localhost:7001/console. You will see the managed server is up.
- Try accessing http://localhost:8001/opdemo/ to see the app

## References

Weblogic docker image
- https://hub.docker.com/_/oracle-weblogic-server-12c
- https://container-registry.oracle.com
- https://github.com/oracle/docker-images/tree/master/OracleWebLogic

Weblogic operator
- https://oracle.github.io/weblogic-kubernetes-operator/
- https://github.com/oracle/weblogic-kubernetes-operator

Monitoring exporter
- https://github.com/oracle/weblogic-monitoring-exporter

Logging exporter
- https://github.com/oracle/weblogic-logging-exporter

Weblogic WDT
- https://github.com/oracle/weblogic-deploy-tooling

Weblogic image tool, docker images
- https://github.com/oracle/weblogic-image-tool

White Paper steps
- https://www.oracle.com/a/ocom/docs/engineered-systems/oracle-webLogic-server-on-pca.pdf

Weblogic Tooling
- https://github.com/oracle/weblogic-image-tool
- https://github.com/oracle/weblogic-deploy-tooling

Operator
- https://oracle.github.io/weblogic-kubernetes-operator/userguide/introduction/
- https://github.com/oracle/weblogic-kubernetes-operator

Weblogic exporter for promethues
- https://github.com/oracle/weblogic-monitoring-exporter

Slack support
- oracle-weblogic.slack.com
- https://weblogic-slack-inviter.herokuapp.com/



