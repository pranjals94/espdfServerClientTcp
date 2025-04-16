this example uses wi fi, also enc28j60 ethernet module can be used

# TCP/IP and TCP Client-Server Coding

Socket programming and TCP are related but distinct concepts. Socket programming is the process of building applications that use sockets to communicate over a network, and TCP is a specific protocol that can be used with sockets. While a socket is a generic concept for an endpoint in a communication channel, TCP is a specific protocol that provides reliable, connection-oriented communication. Sockets can also utilize other protocols, such as UDP, but TCP is the most common.

Types of Network Sockets:

Stream Sockets:
These sockets provide a reliable, sequenced, and unduplicated flow of data, like a stream, using the TCP protocol. They are connection-oriented, meaning a connection must be established before data transfer begins.

Datagram Sockets:
These sockets use the UDP protocol for connectionless communication, where packets are sent independently without guaranteed order or reliability.

Raw Sockets:
Raw sockets offer access to the underlying network layer, allowing for sending and receiving IP packets directly without adhering to higher-level protocol formats.

Sequenced Packet Sockets:
These sockets are less common and provide connection-oriented communication similar to stream sockets but with features related to packet sequencing.

## Overview of TCP/IP

TCP/IP (Transmission Control Protocol/Internet Protocol) is a Low-level transport protocol used to interconnect network devices. It provides end-to-end communication, specifying how data should be packetized, addressed, transmitted, routed, and received. Other higher protocols like http, mqttp, https etc are build on top of tcp.

### Key Features of TCP/IP:

- **Reliability**: Ensures data delivery through error checking and retransmission.
- **Connection-Oriented**: Establishes a connection before data transfer.
- **Standardized Protocols**: Enables interoperability between different devices and networks.

## TCP Client-Server Model

The TCP client-server model is a communication framework where:

- The **server** listens for incoming connections on a specific port.
- The **client** initiates the connection to the server.

### Steps in TCP Communication:

1. **Server Setup**:

   - Create a socket.
   - Bind it to an IP address and port.
   - Listen for incoming connections.
   - Accept client connections.

2. **Client Setup**:

   - Create a socket.
   - Connect to the server using its IP address and port.

3. **Data Exchange**:

   - Use `send()` and `recv()` (or equivalent) to transmit and receive data.

4. **Connection Termination**:
   - Close the socket on both client and server sides.

AF_INET
Meaning: AF_INET stands for "Address Family - Internet". It is used to specify that the socket will use IPv4 addresses (e.g., 192.168.1.1).

SOCK_STREAM
Meaning: SOCK_STREAM specifies that the socket will use a stream-oriented protocol, typically TCP (Transmission Control Protocol).
Purpose: It ensures reliable, ordered, and error-checked delivery of data between applications.
Example: When creating a TCP socket, you combine AF_INET with SOCK_STREAM:

Blocking and non blocking modes.

In TCP networking, blocking functions refer to socket operations (like connect(), accept(), recv(), and send()) that pause the execution of the calling program until the operation completes, or until an error occurs. This means the program is essentially waiting for something to happen on the network connection before continuing.
Here's a more detailed explanation:
Blocking Mode:
Sockets in their default state are typically in blocking mode. This means that when you call a blocking function, the program will pause and wait until the operation completes, such as receiving data, establishing a connection, or sending data.
Example:
If you call recv() (read from the socket) in blocking mode, the program will halt until at least one byte of data is received from the remote end, or until an error occurs.
Non-Blocking Mode:
You can switch a socket to non-blocking mode. In this mode, blocking functions return immediately, regardless of whether the operation has completed. Instead of waiting, the program can continue executing other tasks while monitoring the socket's status.
Why use blocking sockets:
Blocking sockets are simple to use and understand, making them suitable for beginners and straightforward network applications.
Why use non-blocking sockets:
Non-blocking sockets are essential for creating efficient applications that can handle multiple connections concurrently or need to handle situations where a connection might time out.
Non blocking modes may not be supported by esp32 wifi as settings like "setsockopt(sock, SOL_SOCKET, SO_RCVTIMEO, &recvTimeout, sizeof(int)); // set receive time out for 5 seconds " did not seem to work. also this info was found somewhere in google. use poll(), select(), fnclt(), functions related to file descriptors to make a function non blocking.
