# Virtual Routing
------
Application Layer Virtual Routing

- [ ] A cartoon demostration application is good.

## Self-organized 
### RIP
Main Reference:[Route Information Protocol](https://en.wikipedia.org/wiki/Routing_Information_Protocol#RIPng)
#### Components:
+ DV routing:
    * Bellman-Ford algorithm
    * Ford-Fulkerson
+ RIP hop count metric
+ split horizon, route poisoning, holddown
+ RIP version 2: 224.0.0.9 is used to broadcast
+ UDP on port 520
+ Timers
    * Update
    * Invaild
    * Flush
    * Holddown
+ RIPv2 message
    * request
    * response

![RIPv2 message](https://github.com/Leo-xh/Virtual-Routing/blob/master/imgs/RIPv2-message.PNG)
4 threads:

+ listenUDPThread

    event driven

+ routerWatchThread

    determine whether to remove a router

+ updateThread
+ mainThread

1. How to send and receive data?
    check the buffer regularly.
2. Is it necessary to maintain the route table?

### OSPF
No explicit status

Package: Hello, LSU, broadcast, normal, traceRoute, echo

Broadcast: RPF

features:
1. multi-path
2. tackle with routing loops, using md5

Timers:
1. hello
2. dead

## Centralized

### Server
+ connect with routers 
+ receive the LS from routers
+ execute the Floyd algorithm
+ send the corresponding forwarding table to each router

How to connect the routers?
1. routers send connecting packet periodically
2. set a dead interval
How to store the map?
+ Just like that in OSPF

How to send the forwarding table?
+ Triggered update and periodically

Using Twisted!

### Client
+ connect with the server
+ send the LS to the server
+ receive the forwarding from the server

How to connect to the server?
+ periodically and at the beginning
