## Docker image for Liferay v6.x bundeled with Jboss and PostgreSQL 9.3

The project will build a docker image with up and running Liferay 6.x distribution. The image include :

* PostgreSQL 9.3 database

* JDK installation from provided tar.gz  

* Liferay installation from provided Liferay-portal-jboss-6.x bundle zip archive

**Note :** The docker image should not be used in production environment.

## Required Customization

Before running the docker builder, you need to provide following packages in ./assets/packages/ folder :

* Oracle JDK archive : jdk-7uXX-linux-x64.tar.gz

* Official Liferay Poratal 6.x jboss bundle .zip archive : liferay-portal-jboss-6.x<...>.zip

* Liferay license .xml file : license<...>.xml

Added to those packages, you may need to create a "/opt/liferay/docker" folder to be able to link a host deploy folder to the one in the container (used in the docker run command below)

## Build & Run & Start

From project root folder :

    docker build -t postgre-liferay-6.x.x .
    JOB=$(docker run -d -v /opt/liferay/docker:/opt/liferay/deploy -p 40022:22 -p 45432:5432 -p 48080:8080 -p 48787:8787 --name postgre-liferay-6.x.x postgre-liferay-6.x.x)
    docker start $JOB

Note :

    Arbitrary image and container name : postgre-liferay-6.x.x
    Arbitrary port mapping :
        port 22 is mapped to 40022
        port 5432 is mapped to 45432
        port 8080 is mapped to 48080
        port 8787 is mapped to 48787   

## Accounts :

System account : 

    user : root
    pwd : admin

Database accounts :

    PostgreSQL administration :
        user : docker
        pwd : docker
        
    Liferay Database : lportal
        user : lportal
        pwd : lportal

## Access to Liferay Portal :

Open **http://localhost:48080** in the browser of your choice and finish portal initialization.

**Note :** Please note that the first Liferay startup can take up to few minutes.