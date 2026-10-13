
## 1. What Is Switching?

Switching is the process of transferring data from a source to a destination through intermediate network devices or nodes.

Switching determines how communication resources are used and how data is forwarded toward its destination.

Example: When a computer sends data to a server in another city, intermediate network devices forward the data through available links.

The three traditional switching techniques are:

1. Circuit Switching
    
2. Packet Switching
    
3. Message Switching
    

---

## 2. Circuit Switching

Circuit switching establishes a dedicated logical communication path between the sender and receiver before data transmission begins.

Resources are reserved for that communication for the duration of the connection.

**Classic example:** Traditional telephone calls.

### Phases of Circuit Switching

1. **Connection Establishment:** The network establishes a route and reserves the required resources.
    
2. **Data Transfer:** Data flows over the established path while the connection remains active.
    
3. **Connection Release:** The connection terminates, and the reserved resources are released.
    

### Example

During a traditional telephone call, the network maintains the circuit for the duration of the call. The reserved capacity remains associated with the connection even during pauses in conversation.

### Advantages

- Predictable transmission performance after the circuit is established.
    
- Reserved resources provide capacity for the connection.
    
- Data can flow continuously without requiring an individual routing decision for every piece of data.
    
- Suitable for traditional continuous voice communication.
    

### Disadvantages

- A setup phase is required before communication.
    
- Reserved capacity may be wasted during silence or idle periods.
    
- Connection establishment can fail if resources are unavailable.
    
- A circuit failure may interrupt the connection.
    

### Important Exam Points

- Dedicated logical path: Yes.
    
- Connection setup: Required.
    
- Resource reservation: Typically yes.
    
- Example: Traditional telephone networks.
    
- Main disadvantage: Inefficient use of reserved capacity during idle periods.
    

**Exam trap:** A dedicated circuit does not necessarily mean a separate physical cable. A circuit can use reserved time slots or other logical resources within shared infrastructure.

---

## 3. Packet Switching

Packet switching divides a message into smaller units called **packets**. Intermediate network devices forward these packets toward the destination.

Network capacity is generally shared among multiple communications instead of reserving a dedicated end-to-end circuit for every message.

**Classic example:** The Internet.

### How Packet Switching Works

1. The sender divides data into packets when required by the protocol.
    
2. Each packet carries control information, such as addressing and other header fields.
    
3. Intermediate network devices forward packets toward the destination.
    
4. The destination processes the packets and reassembles the original data when appropriate.
    

### Important Characteristics

- Data is divided into packets.
    
- Network capacity is shared by multiple users.
    
- A packet may be stored briefly at a forwarding device before being forwarded.
    
- Packets may experience different delays.
    
- In connectionless datagram networks, packets may take different routes and arrive out of order.
    

### Types of Packet Switching

**A. Datagram Packet Switching**

Each packet is handled independently and carries destination information. A dedicated end-to-end circuit is not established before sending the datagrams.

Example: IP forwarding on the Internet.

**B. Virtual-Circuit Packet Switching**

A logical path is established before packets are transferred. Packets follow the established virtual path, while network capacity remains shared rather than necessarily reserved as in traditional circuit switching.

Important: Virtual-circuit switching is a packet-switching technique, not the same as traditional circuit switching.

### Advantages

- Uses network capacity efficiently through statistical multiplexing.
    
- Supports many simultaneous communications.
    
- Can route around certain link failures when alternate routes exist.
    
- Works well for bursty traffic, such as web browsing and file transfers.
    
- Generally does not require a dedicated circuit for the entire communication.
    

### Disadvantages

- Packet delay may vary because of congestion and queuing.
    
- Packets may be lost, duplicated or reordered, depending on the network and protocol.
    
- Protocol headers add overhead.
    
- Real-time traffic may require additional mechanisms to control delay and jitter.
    

### Important Exam Points

- Example: Internet Protocol (IP) networks.
    
- Data unit: Packet.
    
- Capacity usage: Shared.
    
- Delay: Variable.
    
- Resource allocation: Generally statistical sharing.
    

**Exam trap:** Packet switching does not mean that packets must always follow different routes. They can follow the same route, too.

---

## 4. Message Switching

Message switching transfers an entire message as one unit from one intermediate node to the next.

Each intermediate node receives and stores the **complete message** before forwarding it. This is called store-and-forward switching.

It does not require a dedicated end-to-end circuit to remain reserved for the communication.

### How Message Switching Works

1. The sender transmits the complete message.
    
2. An intermediate node receives and stores the entire message.
    
3. The node selects the next hop and forwards the message.
    
4. The process continues until the message reaches its destination.
    

### Example

Suppose a 10 MB message passes through two intermediate nodes. In classic message switching, each intermediate node needs enough storage to receive the entire message before forwarding it.

Unlike packet switching, the message is not divided into independently forwarded smaller packets by the switching technique itself.

### Advantages

- No dedicated end-to-end circuit is required.
    
- Network links can be shared among multiple messages.
    
- Intermediate nodes can store messages and forward them when the next link becomes available.
    
- Messages can be routed according to destination information and network availability.
    

### Disadvantages

- Large messages require substantial intermediate storage.
    
- Delay can be high and variable.
    
- Unsuitable for many real-time applications requiring low latency.
    
- A complete message must generally be received before it can proceed to the next hop.
    

### Important Exam Points

- Data unit: Entire message.
    
- Forwarding method: Store and forward the complete message.
    
- Dedicated circuit: Not required.
    
- Intermediate storage: Potentially large.
    
- Main disadvantage: High delay and storage requirements.
    

**Exam trap:** Both packet switching and message switching can use store-and-forward. The difference is what is stored and forwarded:

- Message switching: The entire message.
    
- Packet switching: Individual packets.
    

---

## 5. Circuit vs Packet vs Message Switching

|Feature|Circuit Switching|Packet Switching|Message Switching|
|---|---|---|---|
|Data handling|Continuous data stream over an established circuit|Data divided into packets|Entire message handled as a unit|
|Dedicated end-to-end path|Yes, with resources reserved|Usually no; virtual circuits are an exception to connection setup|No|
|Connection setup|Required|Not required for datagram switching; required for virtual-circuit switching|Usually no dedicated connection setup|
|Intermediate storage|Not the defining feature|Packets may be buffered|Entire message stored at each intermediate node|
|Resource allocation|Reserved for the circuit|Shared, generally statistically multiplexed|Shared between messages|
|Delay|Setup delay, then comparatively predictable transfer|Variable because of queuing and routing|Often high because the complete message is stored at each node|
|Bandwidth efficiency|May be low during idle periods|Generally efficient for bursty traffic|Shared-link use is possible, but storage adds cost and delay|
|Example|Traditional telephone circuit|Internet packet delivery|Classic store-and-forward message network|
|Main limitation|Reserved capacity can be wasted|Congestion, loss or variable delay|High storage requirements and delay|

### Quick Memory Trick

- **Circuit switching = Dedicated circuit.** Establish the path, reserve resources, communicate, then release.
    
- **Packet switching = Small packets.** Divide data into packets and forward them through a shared network.
    
- **Message switching = Whole message.** Store the complete message at each intermediate node before forwarding it.
    

---

## 6. Numerical Concepts: Transmission and Delay

Consider a message of size M bits sent over a link with a rate of R bits per second.

### Transmission Time Formula

Transmission time is the time required to place all the bits onto a link.

T_tx = M / R

Where:

- M = Message size in bits.
    
- R = Link transmission rate in bits per second.
    
- T_tx = Transmission time in seconds.
    

### Example 1: Transmission Time

A 12-million-bit message is sent over a 3 Mbps link.

T_tx = (12 × 10⁶) / (3 × 10⁶)

T_tx = 4 seconds

This is the transmission time over one link, ignoring overhead. It is not necessarily the total end-to-end delay.

### Example 2: Message Switching Across Two Links

Suppose the same 12-million-bit message passes through two store-and-forward links, each operating at 3 Mbps.

Transmission time over the first link = 4 seconds.

Transmission time over the second link = 4 seconds.

Total transmission time = 4 + 4 = **8 seconds**.

Assumptions:

- Both links are available.
    
- Propagation delay is ignored.
    
- Queuing delay is ignored.
    
- Overhead is ignored.
    

This illustrates why storing and forwarding the entire message can introduce high delay.

With packet switching, later packets may be transmitted over the first link while earlier packets are being transmitted over the second link. This is called pipelining. The actual end-to-end delay depends on packet size, link rate, propagation delay, queuing, routing and overhead.

### Types of Network Delay

**1. Transmission Delay**

Time required to put all the bits onto a link.

Formula: Transmission delay = Message size / Transmission rate

**2. Propagation Delay**

Time taken by the signal to travel across the physical distance of the link.

**3. Queuing Delay**

Time spent waiting in a queue at a network device.

**4. Processing Delay**

Time a device spends examining and handling the data.

**Exam trap:** Transmission delay and propagation delay are different concepts.

---

## 7. High-Yield Exam Traps

1. Dedicated, reserved path → Circuit switching.
    
2. Entire message stored at each intermediate node → Message switching.
    
3. Data divided into smaller packets → Packet switching.
    
4. Store-and-forward is not exclusive to message switching. Packet-switched networks also commonly store and forward packets.
    
5. Datagram packet switching does not require connection setup; virtual-circuit packet switching does.
    
6. Circuit switching can waste reserved capacity when the connection is idle.
    
7. Message switching generally has high delay because each intermediate node receives the complete message before forwarding it.
    
8. The Internet primarily uses packet switching, although modern networking technologies can also provide resource reservation and quality-of-service mechanisms.
    

---

## 8. Final Revision

Circuit switching: Dedicated path and reserved resources.

Packet switching: Data divided into smaller packets and forwarded over a shared network.

Message switching: Complete message stored and forwarded at each intermediate node.

### Next Topics in Computer Networks

1. Transmission modes: Simplex, half-duplex and full-duplex.
    
2. OSI model.
    
3. TCP/IP model.