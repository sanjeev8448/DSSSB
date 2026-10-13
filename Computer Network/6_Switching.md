## 1. What is switching in computer networks?

Switching is the process of transferring data from a source to a destination through intermediate network devices or nodes.

When multiple devices communicate over a network, switching determines how communication resources are used and how data is forwarded toward its destination.

For example, when a computer sends data to a server in another city, intermediate network devices forward the data through available links.

The three traditional switching techniques differ mainly in how the communication path is established and how the data is transferred.

# 2. Circuit switching

Circuit switching establishes a dedicated logical communication path between the sender and receiver before data transmission begins.

The path's resources are reserved for that communication for the duration of the connection, according to the system's design.

A traditional telephone call is the classic example of circuit switching.

## How does circuit switching work?

Circuit switching generally has three phases.

### Phase 1: Connection establishment

The network establishes a route and reserves the required resources.

### Phase 2: Data transfer

Data flows over the established path while the connection remains active.

### Phase 3: Connection release

The connection is terminated and its reserved resources are released.

### Example

Imagine a traditional telephone call between Person A and Person B. Once the connection is established, the network maintains the circuit for the call. The reserved capacity remains associated with the connection even during pauses in conversation.

### Advantages

- Predictable transmission performance after the circuit is established.
    
- Resources are reserved, so capacity is available to the connection.
    
- Data can flow continuously without each piece needing an individual routing decision.
    
- Suitable for traditional continuous voice communication.
    

### Disadvantages

- A setup phase is required before communication.
    
- Reserved capacity may be wasted during silence or idle periods.
    
- Establishing a circuit can fail when resources are unavailable.
    
- A circuit failure may interrupt the connection.
    

### Important exam points

- Dedicated logical path: Yes.
    
- Connection setup: Required.
    
- Resource reservation: Typically yes.
    
- Classic example: Traditional telephone networks.
    
- Main disadvantage: Inefficient use of reserved capacity when no data is being sent.
    

Exam trap: A dedicated circuit does not necessarily mean that the communication has its own separate physical cable. A circuit can be created using reserved time slots or other logical resources in shared infrastructure.

# 3. Packet switching

Packet switching divides a message into smaller units called packets. The network forwards the packets through intermediate nodes toward the destination.

Unlike traditional circuit switching, packet switching generally shares link capacity among multiple communications rather than reserving a dedicated end-to-end circuit for each message.

The Internet is the best-known example of a packet-switched network.

## How does packet switching work?

1. The sender divides data into packets when required by the protocol.
    
2. Each packet carries control information, such as addressing and other header fields.
    
3. Intermediate network devices forward packets toward the destination.
    
4. The destination processes the received packets and reassembles the original data when appropriate.
    

### Packet Switching

Sender

Message divided into packets

P1

P2

P3

Network routers

Forward packets

Destination

Packets may experience different delays; in datagram networks, they may travel by different routes.

### Important characteristics

- Data is divided into packets.
    
- Network capacity can be shared by many users.
    
- A packet may be stored briefly at a forwarding device before being forwarded.
    
- Packets may experience different delays.
    
- In connectionless datagram networks, different packets can take different routes and may arrive out of order.
    

### Two types of packet switching

A. Datagram packet switching

Each packet is handled independently and carries destination information. A network does not establish a dedicated end-to-end circuit before sending each datagram flow.

Example: IP forwarding on the Internet.

B. Virtual-circuit packet switching

A logical path is established before packets are transferred. Packets follow the established virtual path, although network capacity is still shared rather than necessarily reserved as in classic circuit switching.

This is a packet-switching technique, not the same thing as traditional circuit switching.

### Advantages

- Uses network capacity efficiently through statistical multiplexing.
    
- Supports many simultaneous communications.
    
- Can route around some link failures when alternate routes exist.
    
- Works well for bursty traffic, such as web browsing and file transfer.
    
- Does not generally require a dedicated circuit for the entire communication.
    

### Disadvantages

- Packet delay may vary because of congestion and queuing.
    
- Packets may be lost, duplicated or reordered, depending on the network and protocol.
    
- Protocol headers add overhead.
    
- Real-time traffic may need additional mechanisms to control delay and jitter.
    

### Important exam points

- Classic example: Internet Protocol (IP) networks.
    
- Data unit: Packet.
    
- Capacity usage: Shared.
    
- Delay: Can vary.
    
- Resource allocation: Typically statistical sharing rather than a dedicated reserved circuit.
    

Exam trap: Packet switching does not guarantee that packets will always follow different routes. Packets can take the same route too. Different routes are possible, especially in connectionless datagram networks.

# 4. Message switching

Message switching transfers an entire message as one unit from one intermediate node to the next.

A node receives and stores the complete message before forwarding it. This is known as store-and-forward switching.

Unlike traditional circuit switching, message switching does not require a dedicated end-to-end circuit to remain reserved for the communication.

## How does message switching work?

1. The sender transmits a complete message.
    
2. An intermediate node receives and stores the whole message.
    
3. The node selects the next hop and forwards the message.
    
4. The process continues until the message reaches its destination.
    

### Message Switching

Sender

Node 1

Stores entire message

Node 2

Stores entire message

Destination

Each intermediate node stores the whole message before forwarding it to the next node.

### Example

Suppose a 10 MB message must pass through two intermediate nodes. In classic message switching, each intermediate node needs enough storage to receive the entire message before forwarding it.

It does not divide that message into independently forwarded smaller packets as packet switching does.

### Advantages

- No dedicated end-to-end circuit is required.
    
- Network links can be shared among multiple messages.
    
- Intermediate nodes can store messages and forward them when the next link becomes available.
    
- Messages can be routed based on network availability and destination information.
    

### Disadvantages

- Requires substantial storage for large messages at intermediate nodes.
    
- Can introduce high and variable delay.
    
- Unsuitable for many real-time applications requiring low latency.
    
- A large message may need to be received completely before it can proceed to the next hop.
    

### Important exam points

- Data unit: Entire message.
    
- Forwarding method: Store and forward the complete message.
    
- Dedicated circuit: Not required.
    
- Intermediate storage: Potentially large.
    
- Main disadvantage: High delay and storage requirements.
    

Exam trap: Message switching and packet switching can both use store-and-forward. The crucial difference is what gets stored and forwarded: the entire message in message switching versus individual packets in packet switching.

# 5. Circuit vs Packet vs Message Switching

This is the most important comparison table for exam revision.

|Feature|Circuit switching|Packet switching|Message switching|
|---|---|---|---|
|Data handling|Continuous data stream over an established circuit|Data divided into packets|Entire message handled as a unit|
|Dedicated end-to-end path|Yes, with resources reserved for the circuit|Usually no; virtual circuits are an exception to the no-setup part|No|
|Connection setup|Required|Not required for datagram switching; required for virtual-circuit switching|Usually no dedicated connection setup|
|Intermediate storage|Not the defining feature|Packets may be buffered|Whole message must be stored at each intermediate node|
|Resource allocation|Reserved for the circuit|Shared, generally statistically multiplexed|Shared between messages|
|Delay|Setup delay, then comparatively predictable transfer|Variable delay due to queuing and routing|Often high because each node stores the complete message|
|Bandwidth efficiency|May be low during idle periods|Generally efficient for bursty traffic|Shared-link use is possible, but full-message storage adds cost and delay|
|Example|Traditional telephone circuit|Internet packet delivery|Classic store-and-forward message network|
|Main limitation|Dedicated capacity can be wasted|Congestion, loss or variable delay|High storage needs and delay|

### Quick memory table

Circuit switching = Dedicated circuit

Reserve resources, establish a path, communicate, then release.

Packet switching = Small packets

Divide data into packets and forward them through a shared network.

Message switching = Whole message

Store the full message at each intermediate node before forwarding it.

## 6. Numerical concept: transmission and delay

Consider a message of size \(M\) bits sent over a link with rate \(R\) bits per second.

The basic transmission time is:

\[ \boxed{T_{\text{tx}}=\frac{M}{R}} \]

For example, if a 12-million-bit message is sent over a 3 Mbps link:

\[ T_{\text{tx}}=\frac{12\times10^6}{3\times10^6} =\boxed{4\text{ seconds}} \]

This calculation gives transmission time on one link, ignoring overhead. It is not necessarily the total end-to-end delay.

### Why can message switching have high delay?

Suppose the 12-million-bit message must pass through two store-and-forward links, each operating at 3 Mbps. If both links are available and propagation delay and queuing are ignored, the whole message needs approximately 4 seconds to be transmitted over the first link and another 4 seconds over the second.

Total transmission time for the two serial links:

\[ T = 4+4=\boxed{8\text{ seconds}} \]

This illustrates why storing and forwarding the entire message can create high delay.

With packet switching, packets may be forwarded while later packets are still being received, allowing pipelining. The actual end-to-end time depends on packet size, link rate, propagation delay, queuing, routing and overhead.

Exam trap: Do not confuse transmission delay with propagation delay.

- Transmission delay: Time to put all the bits onto the link.
    
- Propagation delay: Time for the signal to travel across the physical distance of the link.
    
- Queuing delay: Time waiting in a queue at a network device.
    
- Processing delay: Time a device spends examining and handling the data.
    

## 7. High-yield exam traps

1. Dedicated, reserved path → Circuit switching.
    
2. Whole message stored at each intermediate node → Message switching.
    
3. Data divided into smaller packets → Packet switching.
    
4. Store-and-forward is not exclusive to message switching. Packet-switched networks also commonly store and forward packets.
    
5. Packet switching does not always require connection setup. Datagram switching is connectionless; virtual-circuit packet switching uses a setup phase.
    
6. Circuit switching can waste reserved capacity when the connection is idle.
    
7. Message switching generally has high delay because intermediate nodes receive the complete message before forwarding it.
    
8. The Internet primarily uses packet switching, although modern networking technologies can provide reservation and quality-of-service mechanisms.
### Final revision

Circuit = dedicated path. Packet = smaller packets. Message = whole message stored and forwarded.

Next in Computer Networks, study simplex, half-duplex and full-duplex transmission modes, then the OSI model and TCP/IP model.