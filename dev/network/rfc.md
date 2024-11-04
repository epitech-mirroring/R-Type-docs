Internet Engineering Task Force (IETF)                              R-Type Team

Request for Comments: N/A                                             November 2024

Category: Experimental


Network Communication Protocol for R-Type Game
================================================


Status of This Memo:
-------------------
This document specifies an experimental protocol for the R-Type game project. It
details the binary communication format used between the game server and clients,
which relies on UDP for transmitting game state and TCP for managing client
connections and disconnections.


Abstract:
---------
This memo describes a network protocol designed for a multiplayer network game
similar to R-Type. The protocol uses UDP for high-speed transmission of real-time
game data and TCP for reliable handling of client connections and disconnections.
This protocol supports multiple clients connected to a central server, which manages
their interactions.


Table of Contents:
------------------
1. Introduction
2. Protocol Overview
3. Connection Management (TCP)
4. Game Data Transmission (UDP)
    - Packet Format
5. Error Handling and Reconnection
6. Detailed Protocol Behavior
    - Server-Side
    - Client-Side
7. Example Scenario
    - Client Connection
    - Game Data Transmission
8. DTO and TCP Communication
9. Future Considerations
10. Security Considerations
11. Conclusion


1. Introduction
---------------
The R-Type network game requires efficient and real-time data transmission between
a server and multiple clients. The protocol described in this RFC outlines how the
server and clients interact using two different transport-layer protocols (TCP and
UDP) to balance reliability with performance.


2. Protocol Overview
---------------------
The network communication is based on binary communication using the following:
- **TCP** is used for connection management: when clients connect or disconnect
  from the server.
- **UDP** is used for high-frequency game state transmission (e.g., movement and
  game actions).


3. Connection Management (TCP)
-------------------------------
Clients connect to the server using TCP for reliable connection setup. The steps are:
1. The client sends a connection request to the server on the specified TCP port.
2. The server assigns a unique client ID and sends it to the client.
3. The client then initializes a UDP connection for game data transmission.
4. Disconnection is handled via TCP by sending a termination message (e.g., EXIT)
   to the server.


4. Game Data Transmission (UDP)
-------------------------------
Once the client has connected using TCP, all further communication for game data
(e.g., player movements, actions, game updates) occurs over UDP. The client sends
binary-encoded packets to the server at regular intervals, and the server responds
with game state updates.

### Packet Format:
All packets exchanged via UDP have the following binary format:

```
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Client ID (32 bits)                     |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Action Data (variable size)             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- **Client ID**: The unique ID assigned to the client by the server.
- **Action Data**: Encoded game data (e.g., position, movement, actions).


5. Error Handling and Reconnection
----------------------------------
In the event of packet loss (since UDP is used), no retransmission mechanism is
in place. The game compensates for lost packets by relying on frequent updates
and approximating missing data based on the last known state.

In case of disconnection, the client must reconnect using the TCP protocol to
request a new session.


6. Detailed Protocol Behavior
-----------------------------

### Server-Side
- **TCP Initialization**: The server accepts incoming TCP connections from clients
  on a specified port. Once connected, a client is assigned a unique identifier.
- **UDP Communication**: After establishing the TCP connection, the client initiates
  UDP communication by sending its endpoint information to the server.
- **Client Handling**: The server maintains a map of clients, each associated with
  its TCP socket and UDP endpoint. Messages from the client are parsed and either
  added to internal processing queues or dispatched for immediate responses.

### Client-Side
- **TCP Connection**: The client resolves the server's IP and port, connects over
  TCP, and receives its unique identifier from the server.
- **UDP Setup**: The client then sends its local UDP endpoint to the server for
  high-frequency game state exchange.
- **Queue Mechanisms**: Clients have send and receive queues for both TCP and UDP
  messages, allowing decoupled message production and consumption to minimize
  latency during gameplay.


7. Example Scenario
-------------------
### Client Connection:
1. The client connects to the server via TCP at port defined by the server (like 4444).
2. The server assigns a client ID (e.g., 5) and sends it to the client for identification.
3. The client switches to UDP to transmit game data at port defined by the server (like 5555).
4. The client sends its UDP endpoint to the server, allowing the server to direct
   game data packets to the appropriate destination.

### Game Data Transmission:
- The client sends binary-encoded packets to the server over UDP every 15 ms,
  containing movement and action data.


8. DTO and TCP Communication
----------------------------
In the R-Type network protocol, Data Transfer Objects (DTOs) are used to manage internal communication over TCP. These DTOs are serialized into binary form and packaged within a fixed-size packet of 1024 bytes. The first 8 bytes of each packet are reserved for indicating the size of the data to be read, allowing the receiving side to properly handle variable-sized messages.

The use of DTOs provides several benefits for TCP communication:

- **Efficiency**: By packaging the DTOs in a standard binary format, the protocol ensures efficient data transfer, reducing overhead compared to using higher-level abstractions.
- **Internal Communication**: DTOs play a crucial role in managing session states, client authentication, and other control messages that are necessary for maintaining stable connections but are not part of the game logic itself.
- **Standardized Messaging**: The use of a fixed packet size and a consistent format for encoding data makes it easier to implement message handling, minimizing errors and ensuring compatibility between different client and server versions.

Examples of DTOs used for internal TCP communication include:
- **TCPSendIdDTO**: Used to transmit the unique client ID assigned by the server to the client after a successful connection.
- **TCPCreateUDPEndpointDTO**: Manages the creation of a UDP endpoint via the reliable TCP channel, allowing the transition to high-speed UDP data transmission.

These DTOs are essential for managing the non-gameplay aspects of communication, such as connection setup, maintenance, and graceful disconnection, ensuring the stability and reliability of the multiplayer experience.


9. Future Considerations
------------------------
- The protocol could be enhanced with a lightweight reliability layer on top of
  UDP to improve robustness in poor network conditions.
- Compression could be applied to reduce packet sizes for higher efficiency.


10. Security Considerations
--------------------------
The protocol currently has no encryption. Future implementations may consider
adding encryption to both TCP and UDP data streams to prevent packet tampering.
For example, using SSL/TLS for TCP connections and custom encryption for UDP.


11. Conclusion
--------------
This document describes a simple yet effective binary protocol for handling
multiplayer game communication in the R-Type project. While the current
implementation focuses on performance, future iterations may incorporate
additional features like reliability improvements and security enhancements.

