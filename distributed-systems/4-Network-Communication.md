# Introduction

## Multi-threading vs Distributed System
In multi-threaded env, threads can communicate with each other through shared memory. Locks are used for protection against race conditions and semaphores / condition variables are used for signaling.

![DS!](images/ds1.png)

In distributed systems, we don't have a shared memory. Only way for nodes to communicate with each other is through network.
![DS!](images/ds2.png)

## TCP-IP Network Model
It is based on a layered architecture. Higher layer depends on lower layer abstractions.

Higher the abstraction layer, closer it is to us, a software developers / users. Lower the abstraction layer is, closer it is to physical layer / hardware.
![DS!](images/ds3.png)

### Layer 1 - Data Link
1. Physical delivery of data between 2 points over a single link
2. In charge of
- Encapsulation of data
- Flow control
- Error detection
- Error correction, etc..
![DS!](images/ds4.png)

The commonly used protocol in this layer is Ethernet protocol. This protocol wraps our data into frames and uses devices MAC addresses  to deliver those packages from one device to other.
![DS!](images/ds5.png)

### Layer 2 - Internet
It typically uses Internet Protocol (IP). Each device in the network is assigned an IP address. This allows packets to travel from source host to destination host.

![DS!](images/ds6.png)

The internet layer is responsible to deliver the packet from one computer to another. It doesn't know to what specific application process on a destination host the packet is intended for. Nor does it know what application process on source host sent it. For that purpose, we have a transport layer

### Layer 3 - Transport
This abstraction layer takes care of delivering message end-to-end - from process on one machine to a process on another machine. In transport layer, each endpoint / socket identifies itself by 16bit port number. 
![DS!](images/ds7.png)

In transport layer, there are 2 primary protocols;
1. **User Datagram Protocol (UDP)**
- Connection less
- Best Effort based delivery - unreliable
- Messages can be lost, duplicated or reordered
- Based on unit called Datagram which is limited in size
- **UDP is preferred when the speed and simplicity is more important than reliability**
- **UDP allows broadcasting** - you can broadcast a message in network without knowing what all other computers are out there in the network - this decouples sender from receiver(s)

- **Use cases**
Sending debug information to a distributed logging service. If some log messages get lost, its not a big deal as long as those are not financial data
![DS!](images/ds8.png)

Real time data stream service such as video or audio
![DS!](images/ds9.png)

Online Gaming
![DS!](images/ds10.png)


2. **Transmission Control Protocol (TCP)**
- Reliable - guarantees data delivery as sent, without any losses, duplications or reordering.
- Connection between 2 points - no broadcasting like UDP
- The connection between 2 points needs to be established before data is sent and in the end, has to be shutdown gracefully.
- Works as stream of bytes unlike UDP (individual packets)
- More popular in distributed systems because of the reliability
![DS!](images/ds11.png)

Since TCP works on stream of bytes, it is difficult to know where the message starts and where it ends. That's where application layer helps.
![DS!](images/ds12.png)

### Layer 4 - Application
This is the layer we, software developers, typically work with to build distributed system communications.

Protocols
- FTP (File Transfer Protocol)- Transferring files through web
- SMTP (Simple Mail Transfer Protocol) - Sending and receiving emails
- DNS (Domain Name System) - Translating host names into IP addresses
- HTTP (HyperText Transfer Protocol) - transmitting hypermedia documents, video, sound, images

