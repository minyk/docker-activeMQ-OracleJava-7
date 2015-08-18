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

This activemq image can be loaded into Mesos. 

Load this json file as a Docker image:
```
{
    "container": {
        "docker": {
            "image": "granthbr/docker-activemq-oraclejava-7"
        },
        "type": "DOCKER",
        "volumes":[]
    },
    "cpus": "0.5",
    "id": "amq",
    "instances": "1",
    "mem": "512",
    "name": "mq",
    "ports": [
        61616,
        8161
    ],
    "uris": []
} 
```
To load into Mesos via Marathon. First check that Marthon is running:
ps aux|grep -i marathon

Should display something like this:
\root      6952  0.0  0.1  64952  2116 pts/1    S    16:30   0:00 sudo nohup /opt/marathon-0.7.0/bin/start --master zk://localhost:2181/mesos --zk_hosts localhost:2181

Next, load the image into Mesos via a POST to Marathon:
curl -X POST -H "Content-Type: application/json" localhost:8080/v2/apps -d@activemq.json

It should return something like this:
```javascript
{
    "args": null,
    "backoffFactor": 1.15,
    "backoffSeconds": 1,
    "cmd": null,
    "constraints": [],
    "container": {
        "docker": {
            "image": "granthbr/docker-activemq-oraclejava-7"
        },
        "type": "DOCKER",
        "volumes": []
    },
    "cpus": 0.5,
    "dependencies": [],
    "disk": 0.0,
    "env": {},
    "executor": "",
    "healthChecks": [],
    "id": "/amq",
    "instances": 1,
    "mem": 512.0,
    "ports": [
        61616,
        8161
    ],
    "requirePorts": false,
    "storeUrls": [],
    "upgradeStrategy": {
        "minimumHealthCapacity": 1.0
    },
    "uris": [],
    "user": null,
    "version": "2014-10-01T17:39:12.134Z"
}
```


