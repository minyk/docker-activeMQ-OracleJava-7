docker-activeMQ-OpenJDK-8
============================

MQ info:
console login: <containerIPAddress>:8161/admin/
username:admin
password:admin

Good Docker container with Apache Active MQ installed. Open Java 8 update 131 installed.

To run the image and connect to it:

docker run -d --name amq minyk/docker-activemq-openjdk-8:5.14.5

Run with static ports and an external config file

`docker run -d --name amq -p 8161:8161 -p 61616:61616 -p 61613:61613 -p 61617:61617 -v $PWD/conf:/opt/activemq/conf minyk/docker-activemq-openjdk-8`


The start command with parameters is the last line of the Dockerfile.
