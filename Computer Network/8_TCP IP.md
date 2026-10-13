## 1. What is the TCP/IP model?

TCP/IP stands for Transmission Control Protocol / Internet Protocol.

The TCP/IP model describes the layers and protocols used to communicate over interconnected networks, including the Internet.

The commonly taught four-layer TCP/IP model consists of:

1. Application
    
2. Transport
    
3. Internet
    
4. Network Access
    

Unlike the OSI model, which is a seven-layer reference model, TCP/IP is closely associated with the practical protocol suite used by the Internet.

## 2. All four layers at a glance

TOP — Application software and network services

# 4

Application

HTTP, DNS, SMTP, DHCP

# 3

Transport

TCP, UDP — ports and process delivery

# 2

Internet

IP addressing and routing

# 1

Network Access

Ethernet, Wi-Fi, physical transmission

BOTTOM — Network interface and transmission medium

### Memory trick

From top to bottom:

A T I N

Application → Transport → Internet → Network Access.

|Layer|Main responsibility|Key clue|
|---|---|---|
|Application|Network services used by applications|HTTP, DNS, SMTP|
|Transport|Communication between processes|TCP, UDP, port numbers|
|Internet|IP addressing and routing across networks|IP, packets, routers|
|Network Access|Local-link delivery and physical transmission|Ethernet, Wi-Fi, frames|

Exam trap: In the four-layer model, Network Access is the bottom layer, not the Internet layer.

# 3. Application layer

The Application layer provides network communication services directly to application software.

It combines the roles that are divided among the OSI Application, Presentation and Session layers in the seven-layer model.

### Main functions

- Provides network services to applications.
    
- Defines formats and rules for application-level requests and responses.
    
- Supports web browsing, email, file transfer and name resolution.
    
- Handles application-specific data representation and communication.
    
- May include session-management, encryption or data-format functions through protocols and libraries.
    

### Important protocols

|Protocol|Purpose|
|---|---|
|HTTP|Transfers web requests and responses|
|HTTPS|HTTP secured using TLS|
|FTP|File transfer|
|SMTP|Sending and relaying email|
|POP3|Retrieving email|
|IMAP|Accessing and synchronizing email|
|DNS|Resolving domain names and other DNS records|
|DHCP|Automatically provides network configuration|
|SNMP|Network monitoring and management|
|SSH|Secure remote login and command execution|

These are commonly classified as Application-layer protocols in the TCP/IP model.

### Example: Opening a website

When you enter a website address in a browser, HTTP defines the web request and response. DNS may resolve the domain name to an IP address. The application data is then passed to the lower layers for transport and delivery.

### PDU

Data or message.

### Exam traps

- HTTP, FTP, SMTP and DNS belong to the Application layer.
    
- HTTPS uses TLS to secure HTTP communication.
    
- DNS resolves domain names; DHCP supplies network configuration.
    
- In the four-layer TCP/IP model, Session and Presentation functions are generally grouped into Application.
    

# 4. Transport layer

The Transport layer provides communication between application processes running on different hosts.

It uses port numbers to identify transport endpoints and can provide services such as reliability, ordering, segmentation, flow control and congestion control, depending on the transport protocol.

### Main functions

- Process-to-process communication.
    
- Port addressing and multiplexing.
    
- Segmentation and reassembly when required.
    
- Reliable, ordered delivery with TCP.
    
- Flow and congestion control with TCP.
    
- Connection-oriented or connectionless communication, depending on the protocol.
    

### Major protocols

A. TCP — Transmission Control Protocol

TCP provides a reliable, ordered byte stream between endpoints. It uses acknowledgements and retransmission mechanisms and includes flow and congestion control.

Examples of applications commonly using TCP include HTTP/1.1, HTTP/2, email protocols and file-transfer applications.

B. UDP — User Datagram Protocol

UDP provides datagram-based transport with low protocol overhead. It does not itself guarantee delivery, ordering or retransmission.

Examples of uses include DNS queries, real-time communications and online gaming. Applications may implement their own reliability mechanisms where needed.

|Feature|TCP|UDP|
|---|---|---|
|Connection model|Connection-oriented|Connectionless|
|Built-in reliable, ordered byte stream|Yes|No|
|Built-in retransmission|Yes, when required|No|
|Built-in congestion control|Yes|No|
|Data unit commonly named|Segment|Datagram|
|Typical use|Web traffic using HTTP/1.1 or HTTP/2, email|DNS queries, real-time media, gaming|

Note: HTTP/3 uses QUIC over UDP. QUIC provides transport functions, including reliability for its streams and congestion control, above UDP's basic datagram service.

### Port numbers

Ports identify transport endpoints or services.

|Service|Common port|
|---|---|
|HTTP|TCP 80|
|HTTPS|TCP 443; also UDP 443 for HTTP/3 over QUIC by default|
|DNS|UDP/TCP 53, depending on use|
|SMTP relay|TCP 25|
|SSH|TCP 22|
|DHCP for IPv4|UDP 67 (server), UDP 68 (client)|

Port numbers are not IP addresses: an IP address identifies a network endpoint, while a port helps identify a particular transport endpoint on that host.

### PDU

- TCP: Segment
    
- UDP: Datagram
    

### Exam traps

- TCP and UDP belong to the Transport layer.
    
- TCP provides reliable, ordered delivery; UDP alone does not.
    
- Port numbers are a Transport-layer concept.
    
- Do not claim that all Internet application traffic uses TCP.
    

# 5. Internet layer

The Internet layer handles logical addressing and forwarding packets across interconnected networks.

Its primary protocol is IP (Internet Protocol). IP provides addressing and packet forwarding so data can travel from the source host toward the destination host through routers.

### Main functions

- Logical addressing using IP addresses.
    
- Routing packets between networks.
    
- Forwarding packets toward the destination.
    
- Supporting best-effort delivery.
    
- Supporting network-level diagnostic and control functions through related protocols.
    

### Important protocols

|Protocol|Function|
|---|---|
|IPv4|Internet Protocol version 4; 32-bit addresses|
|IPv6|Internet Protocol version 6; 128-bit addresses|
|ICMP|Network-layer diagnostic and error-reporting messages, such as those used by ping|
|IGMP|IPv4 multicast group membership management|
|IPsec|Security protocols for protecting IP traffic|

Routing protocols such as OSPF and BGP help exchange routing information. They support routing decisions but are not themselves the same thing as IP packet forwarding.

### IPv4 versus IPv6

|Feature|IPv4|IPv6|
|---|---|---|
|Address size|32 bits|128 bits|
|Example|`192.168.1.10`|`2001:db8::10`|
|Notation|Dotted decimal|Colon-separated hexadecimal|
|Address capacity|About 4.3 billion possible addresses|\(2^{128}\) possible addresses|

The IPv6 address shown is an illustrative documentation address.

### Role of a router

A router examines an IP packet's destination address, consults its routing information and selects a next hop. When forwarding over another link, it sends the IP packet inside a new link-layer frame appropriate for that link.

### PDU

Packet or IP datagram.

### Addressing

IP address — IPv4 or IPv6.

### Exam traps

- Internet layer → IP addresses, packets and routing.
    
- Router → typically performs Internet-layer forwarding.
    
- IP is best-effort: it does not itself guarantee delivery, ordering or retransmission.
    
- ICMP is used for network diagnostics; `ping` commonly uses ICMP Echo messages.
    
- IPv4 has 32-bit addresses; IPv6 has 128-bit addresses.
    

# 6. Network Access layer

The Network Access layer, also called the Link layer in many TCP/IP descriptions, handles communication over the local network link and the transmission of data over the physical medium.

In the four-layer TCP/IP model, it groups functions that the OSI model separates into the Data Link and Physical layers.

### Main functions

- Framing and local-link delivery.
    
- Link-layer addressing, such as MAC addresses in Ethernet and Wi-Fi.
    
- Media access rules.
    
- Link-level error detection, where provided.
    
- Transmission and reception of bits through copper, fibre or wireless signals.
    
- Interaction with the network interface and underlying medium.
    

### Technologies and protocols

|Technology / protocol|Purpose|
|---|---|
|Ethernet|Common wired LAN technology|
|Wi-Fi (IEEE 802.11)|Wireless LAN technology|
|PPP|Point-to-Point Protocol|
|Ethernet MAC|Link-layer addressing and frame-delivery rules|
|Physical Ethernet standards|Define the signalling and media characteristics of wired Ethernet|

### Devices

- Network interface cards (NICs).
    
- Wi-Fi adapters.
    
- Traditional hubs and repeaters, for the physical part.
    
- Layer 2 switches and bridges, for the data-link part.
    

A modern device may perform functions from multiple layers, so the device list is illustrative rather than exclusive.

### MAC address versus IP address

|MAC address|IP address|
|---|---|
|Used for local-link delivery|Used for logical addressing and routing|
|Associated with the Network Access / Data Link functions|Used at the Internet layer|
|Example: `00:1A:2B:3C:4D:5E`|Example: `192.168.1.10`|

### PDU

The specific unit depends on the function:

- Frame at the data-link portion.
    
- Bits at the physical-transmission portion.
    

### Example

A laptop sends data to its local router over Wi-Fi. The IP packet is carried inside a Wi-Fi frame, and the frame is transmitted as radio signals. The router can then forward the IP packet toward the next network.

### Exam traps

- Network Access → Ethernet, Wi-Fi, frames and physical transmission.
    
- This layer combines OSI Layers 1 and 2 in the common four-layer TCP/IP model.
    
- MAC addresses are associated with link-layer delivery; IP addresses are associated with Internet-layer delivery.
    
- The Network Access layer does not replace IP routing.
    

# 7. TCP/IP versus OSI model

This comparison is very important for DSSSB multiple-choice questions.

|Four-layer TCP/IP model|OSI model|Main function|
|---|---|---|
|Application|Application (7)|Network services for applications|
|Application|Presentation (6)|Data representation, compression and encryption functions|
|Application|Session (5)|Session and dialogue functions|
|Transport|Transport (4)|End-to-end process communication|
|Internet|Network (3)|Logical addressing and routing|
|Network Access|Data Link (2)|Frames and local-link delivery|
|Network Access|Physical (1)|Signals and transmission of bits|

### Key differences

|Feature|OSI model|TCP/IP model|
|---|---|---|
|Common layer count|7|4|
|Nature|General reference model|Model associated with the Internet protocol suite|
|Application-related layers|Three separate layers|Combined into one Application layer|
|Network and link functions|Network, Data Link and Physical are separate|Internet and Network Access|
|Protocol association|Describes layered functions|Closely associated with Internet protocols such as IP, TCP and UDP|

Some textbooks use a five-layer Internet model, separating Data Link and Physical rather than grouping them in Network Access. For this topic, use the four-layer TCP/IP structure in your syllabus.

# 8. Encapsulation in the TCP/IP model

Encapsulation is the process of adding protocol control information as data moves down the layers from the sender's Application layer toward Network Access.

Consider sending an HTTP request using TCP over IPv4 and Ethernet:

### TCP/IP Encapsulation

Application layer

HTTP data

Transport layer

TCP header

HTTP data

TCP segment

Internet layer

IP header

TCP segment

IP packet

Network Access layer

Ethernet header

IP packet

FCS

Ethernet frame

Signals and bits over the medium

Simplified example using TCP/IP over Ethernet. Actual headers and trailers depend on the protocols and network technology in use.

### PDU sequence to memorize

|TCP/IP layer|Data unit|
|---|---|
|Application|Data / message|
|Transport|Segment (TCP) or datagram (UDP)|
|Internet|IP packet / IP datagram|
|Network Access|Frame, then bits and signals|

At the receiver, decapsulation happens in reverse: each layer processes its own control information and passes the remaining data to the next layer above it.

Exam trap: Encapsulation proceeds downward at the sender. Decapsulation proceeds upward at the receiver.

# 9. Quick revision and common MCQ traps

|Exam question clue|Correct answer|
|---|---|
|TCP/IP has how many layers in the common model used here?|4|
|Which layer contains HTTP and DNS?|Application|
|Which layer contains TCP and UDP?|Transport|
|Which layer contains IP?|Internet|
|Which layer contains Ethernet and Wi-Fi link functions?|Network Access|
|Which layer uses port numbers?|Transport|
|Which layer uses IP addresses?|Internet|
|Which layer uses MAC addresses for local-link delivery?|Network Access|
|Which TCP/IP layer combines OSI Layers 5, 6 and 7?|Application|
|Which TCP/IP layer combines OSI Layers 1 and 2?|Network Access|
|Which TCP/IP protocol provides reliable, ordered byte-stream delivery?|TCP|
|Which protocol does not guarantee delivery or ordering by itself?|UDP|

Memory trick: Application = services, Transport = ports, Internet = IP, Network Access = local link.

### Final revision

Memorize this order:

Application → Transport → Internet → Network Access

Then associate each layer with its main clue:

Protocols → Ports → IP → MAC / Frames / Signals

Next, study IPv4 addressing, classes and subnet masks, private vs public IP addresses, IPv6, and MAC vs IP addressing. These topics build directly on the Internet and Network Access layers.