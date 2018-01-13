# Devices Tracking System - Performance Profiling
The Performance Profiling repository contains instructions for running the performance monitoring system, as well as it 
collects all performance tests for the whole infrastructure of Devices Tracking System.

## Monitoring dashboard
In order to run a performance monitoring dashboard, based on the Netflix Vector, in a Docker container, simply type:
```
docker run -p 9090:80 netflixoss/vector:latest
```
The dashboard is running on the `9090` port in your Docker web. This tool monitors performance of all hosts and 
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

