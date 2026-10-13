## 1. What is the OSI model?

OSI stands for Open Systems Interconnection.

The OSI model is a conceptual, seven-layer reference model developed by the International Organization for Standardization (ISO). It explains how data can travel from an application on one computer to an application on another computer through a network.

Each layer has specific responsibilities and interacts with the layers above and below it.

### All seven layers — from bottom to top

TOP — Closest to the user and applications

# 7

Application

Network services for applications

# 6

Presentation

Data format, encryption, compression

# 5

Session

Session establishment and management

# 4

Transport

End-to-end delivery, ports, reliability

# 3

Network

IP addressing and routing

# 2

Data Link

Frames, MAC addresses, local-link delivery

# 1

Physical

Bits, signals and transmission media

BOTTOM — Closest to the physical network connection

### Mnemonics to remember the order

From Layer 1 → Layer 7:

P D N T S P A

Please Do Not Throw Sausage Pizza Away.

|Layer|Name|One-word memory clue|
|---|---|---|
|7|Application|Services|
|6|Presentation|Format|
|5|Session|Conversation|
|4|Transport|Delivery|
|3|Network|Routing|
|2|Data Link|Frames|
|1|Physical|Signals|

From Layer 7 → Layer 1, remember:

A P S T N D P

All People Seem To Need Data Processing.

Exam trap: Application is Layer 7, not Layer 1. Physical is Layer 1, not Layer 7.

# 2. Layer 1 — Physical Layer

The Physical layer transmits raw bits (`0` and `1`) across a physical medium or wireless channel.

It is concerned with how bits are represented and transmitted, rather than what the bits mean.

### Main functions

- Transmits and receives raw bits.
    
- Defines electrical, optical or radio signal characteristics.
    
- Defines physical connectors and interfaces.
    
- Specifies signalling, bit timing and data transmission characteristics.
    
- Defines aspects of transmission media and link speed.
    
- Handles physical synchronization and line coding as specified by the technology.
    

### Examples of technologies and components

- Copper and fibre-optic transmission media.
    
- Ethernet physical-layer signalling.
    
- Repeaters and traditional hubs.
    
- Physical interfaces, connectors and transceivers.
    
- Radio transmission for Wi-Fi.
    

### Data unit (PDU)

Bits

### OSI layer and device examples

|Item|Example|
|---|---|
|PDU|Bits|
|Devices|Repeater, traditional hub|
|Media|Twisted pair, coaxial, fibre optic, radio|
|Main question it answers|How are bits physically transmitted?|

### Example

Suppose you send the character `A`. Its representation may be encoded as a sequence of bits. The Physical layer helps turn those bits into electrical, optical or radio signals that can travel through the chosen medium.

The receiver interprets the incoming signals as bits.

### Exam traps

- Physical layer deals with bits and signals.
    
- It does not use MAC addresses for forwarding or IP addresses for routing.
    
- A traditional hub operates at the Physical layer.
    
- Fibre-optic cables carry optical signals; copper cables carry electrical signals.
    

# 3. Layer 2 — Data Link Layer

The Data Link layer transfers data between devices over a local link and organizes the data into units called frames.

It makes use of link-layer addressing, error detection and medium-access rules as provided by the particular technology.

### Main functions

- Framing: organizes incoming data into frames.
    
- Link-layer addressing: uses MAC addresses in Ethernet and Wi-Fi.
    
- Error detection: detects errors using mechanisms such as a frame check sequence (FCS).
    
- Media access control: coordinates access to a shared communication medium where necessary.
    
- Link-level flow control or error recovery in technologies that support those features.
    

### Sublayers

In the traditional IEEE 802 description, the Data Link layer is divided into two sublayers:

|Sublayer|Main responsibility|
|---|---|
|LLC — Logical Link Control|Logical link functions, including identification of upper-layer protocols in the classic model|
|MAC — Media Access Control|MAC addressing and access to the transmission medium|

### Data unit (PDU)

Frame

### Addressing

The commonly tested address at this layer is the MAC address.

Example:

`00:1A:2B:3C:4D:5E`

This is an example of a 48-bit MAC address written in hexadecimal notation.

### Devices and technologies

- Traditional Layer 2 switches.
    
- Ethernet.
    
- Wi-Fi link-layer mechanisms.
    
- Bridges.
    
- Point-to-Point Protocol (PPP).
    
- High-Level Data Link Control (HDLC).
    

### Example

If two computers are communicating on the same Ethernet LAN, Ethernet frames carry their data across the local link. A switch can use the destination MAC address to decide which port should receive a known unicast frame.

### Exam traps

- Data Link layer → Frames.
    
- Traditional Layer 2 switch → MAC address table.
    
- MAC addresses are used for link-layer delivery, while IP addresses are used for network-layer addressing.
    
- Error detection does not necessarily mean that the Data Link layer automatically corrects every error or retransmits every lost frame.
    

# 4. Layer 3 — Network Layer

The Network layer handles logical addressing and forwarding packets between different networks.

Its main purpose is to help data travel from its source network toward its destination network, potentially through multiple routers.

### Main functions

- Logical addressing using IP addresses.
    
- Routing: determining suitable paths through interconnected networks.
    
- Packet forwarding between networks.
    
- Fragmentation and reassembly where supported by the network protocol; for IPv4, fragmentation may occur under specified conditions.
    
- Handling certain network-level error and diagnostic messages through supporting protocols.
    

### Data unit (PDU)

Packet — more precisely, an IP packet or IP datagram.

### Addressing

The Network layer primarily uses IP addresses.

Examples:

- IPv4: `192.168.1.10`
    
- IPv6: `2001:db8::10` (illustrative documentation address)
    

### Devices and protocols

|Item|Example|
|---|---|
|Device|Router|
|Layer 3 switch|A switch capable of routing IP packets|
|Main protocol|IP|
|Diagnostic protocol|ICMP|
|Common routing protocols|OSPF, BGP|

Routing protocols help routers exchange routing information; they are not all forwarding protocols themselves.

### Example

Imagine a computer in Delhi sends a request to a server in another country.

1. The computer creates an IP packet addressed to the destination IP.
    
2. The local router receives the packet.
    
3. Routers forward it across networks according to routing information.
    
4. The packet eventually reaches the destination network.
    

### Exam traps

- Network layer → Packets and IP addressing.
    
- Router → traditionally associated with Layer 3.
    
- IP is a best-effort protocol; it does not itself guarantee packet delivery or ordering.
    
- An IP address is not the same as a MAC address.
    

# 5. Layer 4 — Transport Layer

The Transport layer provides communication between processes running on different hosts.

It can divide application data into transport units, use port numbers to identify applications or services, and provide reliability or flow control depending on the protocol.

### Main functions

- Process-to-process delivery.
    
- Segmentation and reassembly when required.
    
- Port addressing.
    
- Multiplexing data from multiple applications.
    
- Reliability and retransmission with protocols such as TCP.
    
- Flow control and congestion control with TCP.
    
- Connection-oriented or connectionless transport, depending on the protocol.
    

### Data unit (PDU)

- TCP: Segment.
    
- UDP: Datagram.
    

In general exam questions, the answer is often segment for the Transport layer. Technically, UDP units are more specifically called datagrams.

### Port numbers

Port numbers help a host deliver received transport data to the appropriate application or socket.

Some standard examples:

|Service|Common port|
|---|---|
|HTTP|TCP 80|
|HTTPS|TCP 443; HTTP/3 uses QUIC over UDP 443 by default|
|FTP control|TCP 21|
|DNS|UDP or TCP 53, depending on use|
|SMTP|TCP 25 for server-to-server relay|

Ports identify transport endpoints, not the physical computer itself. Real applications may use different ports when configured to do so.

### TCP versus UDP

|Feature|TCP|UDP|
|---|---|---|
|Connection model|Connection-oriented|Connectionless|
|Built-in reliable, ordered byte stream|Yes|No|
|Delivery and ordering guarantees|Provided by TCP's mechanisms|Not guaranteed by UDP|
|Built-in congestion control|Yes|No|
|Common applications|Web traffic over HTTP/1.1 or HTTP/2, email, file transfer|DNS queries, real-time media, gaming, QUIC transport|

These applications are examples, not strict limitations. For example, DNS can use TCP as well as UDP.

### Example: Opening a website

Your browser may use a transport connection to exchange data with the web server. The transport layer uses port numbers to identify the relevant endpoints; when TCP is used, it provides reliable, ordered delivery of a byte stream.

### Exam traps

- Transport layer → Ports, TCP and UDP.
    
- TCP provides reliable and ordered delivery to the receiving application.
    
- UDP has lower protocol overhead but does not guarantee delivery or ordering.
    
- IP addresses identify network endpoints; port numbers distinguish transport endpoints or services.
    

# 6. Layer 5 — Session Layer

The Session layer manages the establishment, maintenance and termination of communication sessions between applications.

A session is an organized conversation between communicating systems.

### Main functions

- Establishing sessions.
    
- Maintaining and coordinating dialogues.
    
- Terminating sessions.
    
- Synchronization and checkpoints in systems that support those functions.
    
- Supporting recovery or resumption from a checkpoint where the relevant protocol provides it.
    

### Data unit (PDU)

Data

### Example

Imagine two applications conducting a long exchange of information. Session-related functionality may help manage the conversation, coordinate dialogue and support checkpoints so work can resume after an interruption.

In modern networking, these responsibilities are often implemented inside application protocols, libraries or other layers rather than a clearly separate Session-layer protocol.

### Commonly cited examples

- NetBIOS session services.
    
- Remote Procedure Call (RPC) mechanisms, depending on the implementation.
    
- Session-management functions within applications.
    

These examples illustrate session-related functionality; the exact OSI layer assigned to a real-world protocol can depend on how it is used and how the model is being applied.

### Exam traps

- Session layer → Establishes, manages and terminates sessions.
    
- Session synchronization and checkpoints are classic textbook functions.
    
- Do not confuse a session with a TCP connection: one application session may use multiple connections, and a connection may carry multiple application exchanges.
    

# 7. Layer 6 — Presentation Layer

The Presentation layer is concerned with the representation and transformation of data so that the receiving application can interpret it.

Think of it as the layer concerned with the form in which data is represented.

### Main functions

- Data format translation.
    
- Character encoding and representation.
    
- Serialization and deserialization concepts.
    
- Data compression and decompression.
    
- Encryption and decryption in the traditional textbook model.
    

### Data unit (PDU)

Data

### Examples

- Character encoding: ASCII and Unicode encodings such as UTF-8.
    
- Data formats: JPEG and PNG for images; MPEG formats for media.
    
- Data compression: compression formats and algorithms.
    
- Encryption: cryptographic transformations that secure data.
    

These are examples of relevant representation or transformation concepts, rather than a claim that every associated standard is exclusively an OSI Layer 6 protocol.

### Example

Suppose one system produces information in a particular character encoding and another system expects a different representation. Presentation-related functionality can ensure that the data is encoded, decoded or transformed appropriately.

Encryption may also be applied so that the receiving side can decrypt data before its intended processing.

### Exam traps

- Presentation layer → Translation, encryption and compression.
    
- Character representation and data formats are commonly associated with Layer 6 in exam questions.
    
- In modern Internet protocols, encryption such as TLS is not always neatly confined to a single OSI layer. Textbooks often associate it with Presentation-layer functionality for learning purposes.
    

# 8. Layer 7 — Application Layer

The Application layer provides network services and interfaces used by applications. It is the highest layer of the OSI model, closest to the application software.

It does not simply mean every program installed on a computer. It refers to the networking functions and protocols that applications use.

### Main functions

- Provides network services to application software.
    
- Defines application-level requests and responses.
    
- Supports web access, file transfer, email, name resolution and network management.
    
- Identifies the meaning and structure of application messages.
    

### Data unit (PDU)

Data or message.

### Important Application-layer protocols

|Protocol|Main function|
|---|---|
|HTTP|Web request and response|
|HTTPS|Secure HTTP communication using TLS|
|FTP|File transfer|
|SMTP|Sending and relaying email|
|POP3|Email retrieval|
|IMAP|Accessing and synchronizing email|
|DNS|Resolving domain names and other DNS records|
|DHCP|Providing IP configuration to clients|
|SNMP|Network monitoring and management|

### Example: Visiting a website

When you enter a website address in your browser, application-layer protocols define the request and response format. HTTP tells the browser and server how to exchange web content, while DNS may resolve the domain name to an IP address.

Other layers handle transport, routing, framing and signalling.

### Exam traps

- Application layer → HTTP, FTP, SMTP, DNS, DHCP.
    
- It is closest to the end-user's network applications.
    
- HTTP is an application-layer protocol; it is not a Transport-layer protocol.
    
- HTTPS uses TLS for security; HTTP still defines the web request/response semantics.
    

# 9. Complete OSI revision table

This is the table to revise before a DSSSB mock test. Try to memorize the PDU, addressing, examples and primary function for every layer.

|Layer|Name|PDU|Addressing / identifier|Typical examples|
|---|---|---|---|---|
|7|Application|Data|Application-level names and fields|HTTP, FTP, SMTP, DNS, DHCP|
|6|Presentation|Data|Data format / encoding|Character encoding, compression, encryption|
|5|Session|Data|Session identifiers or dialogue state, where applicable|Session management, checkpoints|
|4|Transport|Segment / Datagram|Port numbers|TCP, UDP|
|3|Network|Packet|IP address|IP, ICMP; routers|
|2|Data Link|Frame|MAC address (Ethernet/Wi-Fi)|Ethernet, PPP; Layer 2 switches|
|1|Physical|Bits|No MAC/IP addressing at this layer|Signals, cables, hubs, repeaters|

Important clarification: The PDU and device columns are the conventional exam-level classification. In actual implementations, functions can span OSI layers, and devices such as modern switches, NICs and wireless routers may perform more than one layer's functions.

## 10. Encapsulation and decapsulation

This is a very common question in networking examinations.

### What is encapsulation?

Encapsulation is the process in which each lower layer adds its own control information, typically in a header and sometimes a trailer, as data moves from the Application layer toward the Physical layer.

### Encapsulation — Sender

Application data

TCP header

Application data

Transport segment

IP header

Segment

Network packet

Ethernet header

Packet

FCS

Ethernet frame

Bits and physical signals

Simplified illustration for TCP over IP over Ethernet. FCS is an Ethernet frame check sequence; exact headers and trailers depend on the protocols in use.

### What is decapsulation?

At the receiving end, each layer processes and removes the control information relevant to it, then passes the remaining data upward.

- Physical layer receives the signal and recovers bits.
    
- Data Link layer processes the frame.
    
- Network layer processes the IP packet.
    
- Transport layer processes the segment or datagram and delivers data to the correct endpoint.
    
- Upper layers process the application data.
    

Exam trap: Encapsulation moves down the layer stack at the sender. Decapsulation moves up the layer stack at the receiver.

## 11. Following one web request through the OSI model

Suppose you use a browser to visit a website.

7 · Application

Browser creates an HTTP request.

6 · Presentation

Data representation and security transformations may be applied.

5 · Session

Communication-session functions may be managed by the application or relevant libraries.

4 · Transport

TCP or a transport such as QUIC carries application data using ports.

3 · Network

IP addresses and routing move packets toward the server.

2 · Data Link

Ethernet or Wi-Fi frames carry data across the local link.

1 · Physical

Electrical, optical or radio signals transmit bits.

At the destination, the data is processed in the reverse direction so the server application can interpret the request.

Technical nuance: The OSI model is a reference framework. Real Internet protocols do not always map one-to-one onto seven independent implementations. For example, TLS is often considered between the application and transport layers in simplified TCP/IP diagrams, even though encryption is taught as a Presentation-layer function in many OSI exam notes. HTTP/3 uses QUIC over UDP rather than TCP.

# 12. OSI model vs TCP/IP model

Both models describe network communication, but they organize the functions differently.

|OSI model|Common four-layer TCP/IP model|
|---|---|
|Application (7)|Application|
|Presentation (6)|Application|
|Session (5)|Application|
|Transport (4)|Transport|
|Network (3)|Internet|
|Data Link (2)|Network Access / Link|
|Physical (1)|Network Access / Link|

The TCP/IP model is commonly presented with four layers, although some textbooks use a five-layer model by separating Physical and Data Link.

### Key differences

- OSI has seven layers.
    
- The common four-layer TCP/IP model has four layers.
    
- OSI is a general reference model.
    
- TCP/IP describes the protocol suite used by the Internet.
    
- In the common mapping, OSI Application, Presentation and Session functions are grouped into the TCP/IP Application layer.
    
- OSI Network corresponds approximately to the TCP/IP Internet layer.
    
- OSI Physical and Data Link functions are commonly grouped into the TCP/IP Link or Network Access layer.
    

Exam trap: Do not answer that TCP/IP always has exactly four layers irrespective of the question. Use the model your question specifies: four-layer or five-layer TCP/IP.

# 13. High-yield OSI exam traps

|Question clue|Correct answer|
|---|---|
|How many OSI layers?|7|
|Lowest layer|Physical|
|Highest layer|Application|
|Raw bits and signals|Layer 1 — Physical|
|Frames and MAC addresses|Layer 2 — Data Link|
|Packets and IP addresses|Layer 3 — Network|
|Segments, datagrams and ports|Layer 4 — Transport|
|Session establishment and checkpoints|Layer 5 — Session|
|Encryption, compression and data formats in the textbook model|Layer 6 — Presentation|
|HTTP, FTP, SMTP and DNS|Layer 7 — Application|
|Traditional hub|Layer 1|
|Traditional Layer 2 switch|Layer 2|
|Router|Layer 3|
|TCP|Layer 4|
|Encapsulation|Sender: upper layers toward lower layers|
|Decapsulation|Receiver: lower layers toward upper layers|

Three addresses to remember:

- MAC address: Layer 2 — local-link delivery.
    
- IP address: Layer 3 — logical network addressing and routing.
    
- Port number: Layer 4 — transport endpoint identification.

7 Application — 6 Presentation — 5 Session — 4 Transport — 3 Network — 2 Data Link — 1 Physical.

Remember the central distinctions: bits → frames → packets → segments when moving upward from Layer 1 to Layer 4 conceptually, and the reverse encapsulation direction when data is sent from an application down to the network. More precisely, outgoing application data becomes a transport segment or datagram, then a network packet, then a link-layer frame, and finally a sequence of bits and signals.

Next, study the TCP/IP model, IP addressing (IPv4 and IPv6), MAC vs IP addresses, and TCP vs UDP. These topics connect directly to the OSI model and are useful for comparison-based exam questions.