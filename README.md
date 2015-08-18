docker-activeMQ-OracleJava-7 -- Contains JSON for Mesos Docker task creation
============================

MQ info:
console login: <containerIPAddress>:8161/admin/ 
username:admin
password:admin

Good Docker container with Apache Active MQ installed. Oracle Java 7 installed. 

To run the image and connect to it:
docker run -d --name amq granthbr/docker-activemq-oraclejava-7 

run with static ports and an external config file
docker run -d --name amq -p 8161:8161 -p 61616:61616 -p 61613:61613 -p 61617:61617 granthbr/docker-activemq-oraclejava-7 

Ports that needs to be open are listed in the Docker file.
The start command with parameters is the last line of the Dockerfile.