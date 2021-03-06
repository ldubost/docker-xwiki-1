## Introduction

The goal of this project is to provide a customized tomcat8 container for Xwiki (KMDB) in Docker containers

[![](https://images.microbadger.com/badges/version/zwindler/xwiki-tomcat.svg)](http://microbadger.com/images/zwindler/xwiki-tomcat) [![](https://images.microbadger.com/badges/image/zwindler/xwiki-tomcat.svg)](http://microbadger.com/images/zwindler/xwiki-tomcat)


## Prerequisite 

### Build dependancies

This project uses Docker, containers, XWiki war file and JDBC pilot (all available from the Internet). This XWiki setup is preconfigured to use a PostgreSQL database, preferably from a docker container as well.

### Run dependancies

N/A

## Deploy

### Installation

To install, you have two solutions

#### Using Docker only

  * docker build -t zwindler/xwiki-tomcat:latest . #If you get it fron the source
  * docker run --net=xwiki-nw -itd --name xwiki-postgres -e POSTGRES_DB=xwiki -e POSTGRES_USER=xwiki -e POSTGRES_PASSWORD=xwiki postgres
  * docker run --net=xwiki-nw -itd --name xwiki-tomcat -p 8080:8080 -e POSTGRES_INSTANCE=xwiki-postgres zwindler/xwiki-tomcat
				
#### Using Docker-Compose
						
  * docker-compose up -d
	
## Test

URL : http://[serveur]:[port]/xwiki

Example : <http://localhost:8080/xwiki>
