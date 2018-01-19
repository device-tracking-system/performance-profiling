# Devices Tracking System - Performance Profiling
The Performance Profiling repository contains instructions for running the performance monitoring system, as well as it 
collects all performance tests for the whole infrastructure of Devices Tracking System.

## Monitoring dashboard
In order to run a performance monitoring dashboard, based on the Netflix Vector, in a Docker container, simply type:
```
docker run -p 9090:80 netflixoss/vector:latest
```
The dashboard is running on the `9090` port in your Docker network. This tool monitors performance of all hosts and 
containers running the Performance Co-Pilot (PCP) program by collecting necessary metrics in high resolution. In order 
to install the PCP for monitoring given microservice, please refer to an appropriate repository.  
  
In order to check whether the monitoring services are running properly, open the container's bash by typing:
```
docker exec -it [CONTAINER ID] bash
```
and type:
```
netstat -anp | grep ':44321'
```
then type:
```
netstat -anp | grep ':44323'
```
The commands above should return an output similar to:
```
tcp        0      0 0.0.0.0:44321           0.0.0.0:*               LISTEN      -

tcp        0      0 0.0.0.0:44323           0.0.0.0:*               LISTEN      -
tcp6       0      0 :::44323                :::*                    LISTEN      -
```

## Time Tracing
For two HTTP-utilizing microservices: [UI Service](https://github.com/device-tracking-system/ui-service) and 
[Edge Server](https://github.com/device-tracking-system/edge-server) the Spring Cloud Sleuth is used. This library is
responsible for tagging HTTP requests so that they may be recognized and visualised by the Zipking tracing service.
The dashboard illustrating recorded attributes is presented on the `9091` port when the 
[Tracing Service](https://github.com/device-tracking-system/tracing-service) is ran.

## AMQP Monitoring
If the RabbitMQ broker instance is installed along with the [Management Plugin](https://www.rabbitmq.com/management.html),
the monitoring dashboard presenting attributes of a messaging system (including exchanges, queues, bindings and metrics)
is located on the `15672` port. Default credentials (user/password) for the management dashboard are: `guest/guest`.

## MongoDB Monitoring
In order to run a [MongoDB Client](https://www.nosqlclient.com/) application, which offers many utilities as well as 
provides some performance monitoring, please run a Docker container by typing:
```
docker run -p 9092:3000 -e MONGO_URL=[MONGODB SERVER URI] mongoclient/mongoclient
``` 
where the `[MONGODB SERVER URI]` in it's simplest form is given by `mongodb://[MONGODB HOST]:[MONGODB PORT]`. The client
web application is running on the `9092` port in your Docker network. Once the application is opened, it is necessary to
connect to the desired database by clicking the "Connect" button in the upper right corner and providing some necessary
information such as: connection URL (i.e. the `MONGODB HOST]`), server port (i.e. the `[MONGODB PORT]`) and name of the
database (e.g. `uiService` or `processingService`). After successful connection, the management panel for given database
is opened. 
