## 1. Protocols at a glance

A network protocol is a set of rules that governs communication between devices or applications.

|Protocol|Full form|Main purpose|TCP/IP layer|
|---|---|---|---|
|TCP|Transmission Control Protocol|Reliable, ordered transport|Transport|
|UDP|User Datagram Protocol|Lightweight datagram transport|Transport|
|IP|Internet Protocol|Logical addressing and packet forwarding|Internet|
|HTTP|Hypertext Transfer Protocol|Transfer web content|Application|
|HTTPS|HTTP Secure|Secure web communication using TLS|Application|
|FTP|File Transfer Protocol|File transfer|Application|
|SMTP|Simple Mail Transfer Protocol|Sending and relaying email|Application|
|POP / POP3|Post Office Protocol|Retrieving email|Application|
|DNS|Domain Name System|Resolves names and other DNS records|Application|
|DHCP|Dynamic Host Configuration Protocol|Automatically configures network settings|Application|
|ARP|Address Resolution Protocol|Resolves IPv4 addresses to link-layer addresses on a local network|Link / Network Access|

Memory grouping:

- Transport: TCP, UDP
    
- Internet: IP
    
- Application: HTTP, HTTPS, FTP, SMTP, POP3, DNS, DHCP
    
- Local-link address resolution: ARP
    

ARP is an important exception to memorize: it does not fit as neatly into the TCP/IP layers as the other protocols. In introductory networking, it is generally associated with the link layer or between the Internet and Network Access layers.

# 2. TCP — Transmission Control Protocol

TCP is a connection-oriented transport-layer protocol that provides a reliable, ordered stream of bytes between two endpoints.

It is used when applications need the receiving end to obtain data reliably and in the same order in which it was sent.

### Main functions

- Establishes a connection before ordinary data transfer.
    
- Provides reliable delivery using acknowledgements and retransmissions.
    
- Preserves the order of bytes delivered to the application.
    
- Uses sequence numbers and acknowledgements.
    
- Provides flow control so a fast sender does not overwhelm a receiver.
    
- Uses congestion control to respond to network congestion.
    
- Uses port numbers to identify transport endpoints.
    

### How TCP connection establishment works

A standard TCP connection begins with the three-way handshake.

### TCP Three-Way Handshake

Client

Server

1

SYN

Client requests connection establishment.

2

SYN-ACK

Server acknowledges and responds.

3

ACK

Client acknowledges the server's response; the connection is established.

### TCP header concepts

|Field|Purpose|
|---|---|
|Source port|Identifies the sender's transport endpoint|
|Destination port|Identifies the receiving transport endpoint|
|Sequence number|Tracks byte positions in the stream|
|Acknowledgement number|Indicates the next byte expected in the usual cumulative acknowledgement model|
|Flags|Include SYN, ACK, FIN and RST|
|Window size|Supports receiver flow control|
|Checksum|Detects errors in the TCP segment and associated pseudo-header information|

### TCP characteristics

- Layer: Transport
    
- PDU: Segment
    
- Addressing: Port numbers, alongside IP addressing at the Internet layer
    
- Connection model: Connection-oriented
    
- Reliability: Yes, with acknowledgements and retransmission mechanisms
    
- Ordering: Yes, for data delivered to the application
    

Common examples include web traffic over HTTP/1.1 and HTTP/2, email transmission and file transfers.

### Exam traps

- TCP is not the same as IP: TCP provides transport reliability; IP provides network addressing and forwarding.
    
- TCP delivers a byte stream, not individual application message boundaries.
    
- A TCP acknowledgement does not mean that the receiving application has finished processing the data.
    
- TCP does not guarantee that the network can never lose packets; its mechanisms handle many loss cases through retransmission.
    

# 3. UDP — User Datagram Protocol

UDP is a connectionless transport-layer protocol. It sends independent datagrams without TCP-style connection establishment or built-in guarantees of delivery and ordering.

UDP has a simpler header and lower protocol overhead than TCP.

### Main functions

- Sends datagrams from one transport endpoint to another.
    
- Uses source and destination port numbers.
    
- Includes a checksum mechanism for error detection, with details varying by IP version and context.
    
- Allows applications to define their own recovery or reliability behaviour if needed.
    

### Characteristics

|Feature|UDP|
|---|---|
|Layer|Transport|
|PDU|Datagram|
|Connection setup|No TCP-style handshake|
|Delivery guarantee|No|
|Ordering guarantee|No|
|Retransmission built in|No|
|Header size|8 bytes|
|Typical uses|DNS queries, real-time media, gaming, QUIC transport|

### Example

A live voice or video application may prefer low delay rather than waiting for a retransmission of stale data. UDP allows the application to decide how to handle missing or late data.

However, UDP is not inherently faster in every situation. Performance depends on the application, network conditions and additional mechanisms used above UDP.

### TCP vs UDP

|Feature|TCP|UDP|
|---|---|---|
|Connection-oriented?|Yes|No|
|Reliable ordered byte stream?|Yes|No|
|Data unit|Segment|Datagram|
|Header size|Minimum 20 bytes without options|8 bytes|
|Built-in retransmission|Yes|No|
|Built-in flow and congestion control|Yes|No|
|Typical use|Reliable web and file transfer|Low-overhead datagrams, DNS and real-time applications|

### Exam traps

- UDP is not the same as unreliable hardware: it is a protocol that simply makes fewer delivery guarantees.
    
- UDP does not establish a TCP-style connection.
    
- UDP header = 8 bytes is a useful fact to memorize.
    
- TCP header minimum = 20 bytes, excluding options.
    
- QUIC uses UDP as its underlying transport, but QUIC itself provides additional transport functions, including reliability for its streams and congestion control.
    

# 4. IP — Internet Protocol

IP stands for Internet Protocol. It operates at the Internet layer of the TCP/IP model and the Network layer of the OSI model.

IP provides logical addressing and carries packets from a source toward a destination across interconnected networks.

### Main functions

- Provides IPv4 or IPv6 addressing.
    
- Places data into IP packets.
    
- Enables routing and forwarding between networks.
    
- Supports best-effort delivery.
    
- Allows routers to forward packets based on destination IP addresses.
    

### IPv4 and IPv6

|Feature|IPv4|IPv6|
|---|---|---|
|Address length|32 bits|128 bits|
|Example|`192.168.1.10`|`2001:db8::10`|
|Notation|Dotted decimal|Colon-separated hexadecimal|
|Packet delivery|Best effort|Best effort|
|Header checksum|Present in IPv4 header|No header checksum in the IPv6 base header|

The addresses shown are examples; `2001:db8::10` is from the IPv6 documentation range.

### What does best-effort delivery mean?

IP tries to forward packets toward their destinations, but IP by itself does not guarantee:

- Delivery.
    
- In-order arrival.
    
- Exactly-once delivery.
    
- Retransmission of lost packets.
    

Applications or transport protocols may provide additional mechanisms. For example, TCP retransmits data when required.

### IP versus TCP

|IP|TCP|
|---|---|
|Internet / Network layer|Transport layer|
|Uses IP addresses|Uses port numbers along with the IP addressing provided below|
|Routes and forwards packets|Provides a reliable, ordered byte stream|
|Does not guarantee delivery|Uses acknowledgements and retransmissions|
|PDU: packet / datagram|PDU: segment|

Exam trap: IP and TCP work together but have different responsibilities. IP gets packets across networks; TCP provides reliable, ordered data delivery between endpoints.

# 5. HTTP — Hypertext Transfer Protocol

HTTP is an application-layer protocol used to transfer web resources between clients and servers.

A web browser usually acts as an HTTP client, while a web server processes requests and returns responses.

### How HTTP works

1. The client sends an HTTP request.
    
2. The server processes the request.
    
3. The server sends an HTTP response containing a status code, headers and, where applicable, a body.
    

Example request:

```
GET /index.html HTTP/1.1
Host: example.com
```

Example response:

```
HTTP/1.1 200 OK
Content-Type: text/html
```

The response may also contain the HTML page in its body.

### Important HTTP methods

|Method|Common purpose|
|---|---|
|GET|Retrieve a resource|
|POST|Submit data or request processing|
|PUT|Create or replace a resource at a specified URI, according to the API's semantics|
|PATCH|Partially modify a resource|
|DELETE|Request deletion of a resource|
|HEAD|Retrieve response headers without the usual response body|

### Common HTTP status codes

|Code|Meaning|
|---|---|
|200|OK — request succeeded|
|201|Created|
|301|Moved Permanently|
|400|Bad Request|
|401|Unauthorized; authentication is needed or has failed|
|403|Forbidden|
|404|Not Found|
|500|Internal Server Error|
|503|Service Unavailable|

### HTTP characteristics

- Layer: Application
    
- Default port: TCP 80 for conventional HTTP
    
- Communication model: Request-response
    
- State: HTTP's core semantics are stateless, although applications can maintain state using cookies, tokens and server-side sessions.
    
- Security: Plain HTTP does not encrypt traffic by itself.
    

### Exam traps

- HTTP is not a Transport-layer protocol.
    
- HTTP is conventionally associated with TCP port 80.
    
- HTTP is stateless at its core; cookies can be used to maintain application state.
    
- HTTP request methods and status codes serve different purposes: methods describe requested operations, while status codes describe the response outcome.
    

# 6. HTTPS — HTTP Secure

HTTPS is HTTP communication protected by TLS (Transport Layer Security).

TLS can provide encryption, integrity protection and server authentication, helping protect web traffic against eavesdropping and tampering.

### How HTTPS works

1. The browser connects to the web server.
    
2. The client and server establish TLS security parameters and authenticate the server using its certificate.
    
3. They establish cryptographic keys.
    
4. HTTP messages are sent through the protected connection.
    

For HTTPS using HTTP/1.1 or HTTP/2, TCP with TLS is commonly used. HTTP/3 uses QUIC over UDP, with TLS 1.3 integrated into QUIC's handshake.

### HTTP vs HTTPS

|Feature|HTTP|HTTPS|
|---|---|---|
|Security|No encryption by itself|Uses TLS protection|
|Integrity protection|Not provided by HTTP alone|Provided by TLS|
|Server authentication|Not provided by HTTP alone|Commonly uses certificates|
|Conventional port|TCP 80|TCP 443; HTTP/3 commonly uses UDP 443|
|Layer|Application|Application|
|Main purpose|Web communication|Protected web communication|

### Why is HTTPS important?

HTTPS helps protect passwords, payment details, private messages and other web data in transit. Certificate validation can help the browser confirm that it is communicating with the intended server.

HTTPS does not guarantee that a website is trustworthy or free from malware. It secures the connection, not the honesty of the website itself.

### Exam traps

- HTTPS means HTTP secured using TLS, not a different replacement for the HTTP request/response model.
    
- The conventional HTTPS port is 443.
    
- HTTPS provides encryption and integrity protection in transit.
    
- HTTP/3 uses QUIC over UDP, so do not assume every HTTPS connection uses TCP.
    

# 7. FTP — File Transfer Protocol

FTP is an application-layer protocol used to transfer files between a client and a server.

Traditional FTP uses separate connections for control and data.

### Default ports

|Connection|Traditional FTP port|
|---|---|
|Control connection|TCP 21|
|Data connection|TCP 20 in classic active mode|
|Passive-mode data connection|A server-selected port negotiated during the session|

### How FTP works

- The client establishes a control connection with the FTP server.
    
- Commands such as login, file listing and transfer requests travel over the control connection.
    
- File content and directory-listing data use a separate data connection.
    
- The data connection's setup depends on active or passive mode.
    

### Active versus passive FTP

|Feature|Active mode|Passive mode|
|---|---|---|
|Control connection|Client to server TCP 21|Client to server TCP 21|
|Data connection|Server initiates the data connection toward the client|Client initiates the data connection to a server-advertised port|
|Common complication|Client-side firewalls or NAT may block incoming data connections|Requires the server's passive ports to be reachable|

### Important security point

Traditional FTP does not encrypt usernames, passwords or file contents by default.

Secure alternatives include:

- FTPS: FTP secured with TLS.
    
- SFTP: SSH File Transfer Protocol, a separate protocol that operates over SSH.
    

FTPS and SFTP are not the same protocol.

### Exam traps

- FTP control connection: TCP 21.
    
- TCP 20 is associated with classic active-mode FTP data connections, not every FTP data transfer.
    
- FTP uses separate control and data connections.
    
- Traditional FTP is not secure by default.
    
- SFTP is not simply another name for FTPS.
    

# 8. SMTP — Simple Mail Transfer Protocol

SMTP is an application-layer protocol used to send and relay email.

Mail clients typically submit outgoing email to an outgoing mail server, and mail servers use SMTP to relay messages toward recipient mail servers.

### How email delivery works

1. The sender composes an email in a mail application.
    
2. The application submits the outgoing message to a mail server.
    
3. SMTP transfers or relays the message between mail systems.
    
4. The recipient retrieves or accesses the message using a protocol such as POP3 or IMAP.
    

### Common SMTP ports

|Port|Common purpose|
|---|---|
|TCP 25|Server-to-server SMTP relay|
|TCP 587|Message submission, commonly with STARTTLS|
|TCP 465|Message submission using implicit TLS|

These are common conventional uses; individual systems may be configured differently.

### Important SMTP commands

|Command|Purpose|
|---|---|
|HELO / EHLO|Introduce the client; EHLO supports extended SMTP features|
|MAIL FROM|Specify the envelope sender|
|RCPT TO|Specify a recipient|
|DATA|Begin transfer of message content|
|QUIT|End the SMTP session|

SMTP commands are part of the protocol conversation; they are not separate network protocols.

### SMTP versus POP3

|SMTP|POP3|
|---|---|
|Sends and relays email|Retrieves email from a mail server|
|Used for outgoing mail|Used by a client to access received mail|
|Common ports: 25, 465 and 587 for different functions|Common ports: 110 and 995|
|Pushes a message onward to the next mail system|Lets a mail client retrieve messages from a mailbox|

### Exam traps

- SMTP = sending/relaying email.
    
- POP3 = retrieving email.
    
- SMTP commonly uses TCP port 25 for server-to-server relay; port 587 for message submission; port 465 for implicit-TLS submission.
    
- Sending and retrieving email are different operations.
    

# 9. POP — Post Office Protocol

In a networking syllabus, POP usually refers to POP3 (Post Office Protocol version 3), an application-layer protocol used by a mail client to retrieve messages from a mail server.

### How POP3 works

1. The mail client connects to the server.
    
2. It authenticates using the configured method.
    
3. It retrieves available messages.
    
4. Depending on client and server settings, messages may be deleted from the server after retrieval or retained there.
    

POP3 is generally simpler than IMAP and is traditionally associated with downloading mail for local access.

### Common ports

|Port|Purpose|
|---|---|
|TCP 110|POP3|
|TCP 995|POP3 over implicit TLS (POP3S)|

### POP3 versus IMAP

Although IMAP is not in your list, this comparison helps prevent exam confusion.

|Feature|POP3|IMAP|
|---|---|---|
|Main purpose|Retrieve email|Access and synchronize email|
|Typical behaviour|Download messages to a client|Manage and synchronize messages on the server|
|Server-side folders|Limited support in the traditional model|Supports server-side mailbox and folder management|
|Common ports|TCP 110, 995 for POP3S|TCP 143, 993 for IMAP over implicit TLS|

Modern POP3 clients can retain copies on the server, so “POP always deletes messages from the server” is not correct.

### Exam traps

- POP3 retrieves email; SMTP sends and relays email.
    
- POP3 default port: TCP 110.
    
- POP3 over implicit TLS: TCP 995.
    
- POP3 and IMAP are not the same protocol.
    

# 10. DNS — Domain Name System

DNS is an application-layer naming system that resolves domain names to records, including IP addresses.

It lets people use names such as `example.com` rather than needing to memorize numerical IP addresses.

### How DNS resolution works

Suppose you enter `www.example.com` into a browser.

1. The device checks relevant local caches and configuration.
    
2. If necessary, it asks a DNS resolver.
    
3. The resolver obtains the required record from its cache or by querying other DNS servers.
    
4. The result is returned to the client.
    
5. The browser can then use the IP address to connect to the server.
    

### Basic DNS Resolution

Browser / Device

Requests a domain name

DNS Resolver

Checks cache / looks up records

DNS Records

A / AAAA or other record types

IP address or DNS response

### Important DNS record types

|Record|Function|
|---|---|
|A|Maps a name to an IPv4 address|
|AAAA|Maps a name to an IPv6 address|
|MX|Specifies mail servers for a domain|
|CNAME|Gives an alias to another domain name|
|NS|Identifies authoritative name servers for a zone|
|PTR|Used for reverse lookup, mapping an address to a name|
|TXT|Stores text data used for various purposes, including some email-security records|

### DNS port numbers

- UDP port 53: Commonly used for ordinary DNS queries and responses.
    
- TCP port 53: Used for zone transfers and also for DNS queries when needed, such as when responses require TCP.
    

DNS can also use encrypted transports such as DNS over TLS or DNS over HTTPS, which use different ports and encapsulation.

### DNS versus DHCP

|DNS|DHCP|
|---|---|
|Resolves domain names and other DNS records|Provides network configuration to clients|
|Example: `example.com` → IP address|Example: supplies a client with an IP address and gateway|
|Common port: 53 over UDP or TCP|IPv4 DHCP uses UDP ports 67 and 68|

### Exam traps

- DNS stands for Domain Name System.
    
- DNS is not limited to mapping domain names to IPv4 addresses; it supports IPv6 and many other record types.
    
- DNS normally uses UDP port 53, but TCP port 53 is also important.
    
- DNS is not the same as DHCP.
    

# 11. DHCP — Dynamic Host Configuration Protocol

DHCP automatically supplies network configuration to clients, reducing the need for manual configuration.

For IPv4, a DHCP server can provide an IP address, subnet mask, default gateway, DNS server information and lease duration.

### What can DHCP provide?

- IP address.
    
- Subnet mask.
    
- Default gateway.
    
- DNS server addresses.
    
- Lease duration and other configuration options.
    

### DHCP ports (IPv4)

|Device / role|Port|
|---|---|
|DHCP server|UDP 67|
|DHCP client|UDP 68|

A client without an assigned IPv4 address commonly uses broadcast messages during initial discovery.

### DHCP DORA process

A classic IPv4 DHCP exchange is commonly remembered as DORA.

## D

Discover

The client searches for available DHCP servers.

## O

Offer

A server offers an address and configuration.

## R

Request

The client requests the offered configuration.

## A

Acknowledgement

The server confirms the lease and configuration.

### Example

When your laptop joins a home Wi-Fi network, the router commonly acts as a DHCP server. It can assign an address such as `192.168.1.25`, along with the subnet mask, default gateway and DNS server information.

### DHCP versus static addressing

- Dynamic addressing: A DHCP server assigns or renews a lease.
    
- Static addressing: An administrator or user manually configures the address, or creates a fixed reservation in DHCP, depending on the setup.
    

### Exam traps

- DHCP stands for Dynamic Host Configuration Protocol.
    
- DHCP automates host configuration; DNS resolves names.
    
- IPv4 DHCP uses UDP server port 67 and client port 68.
    
- DHCP uses leases: a typical dynamic address is assigned for a defined period rather than necessarily being permanent.
    
- DHCPv6 differs from IPv4 DHCP and uses UDP ports 546 (client) and 547 (server).
    

# 12. ARP — Address Resolution Protocol

ARP resolves a known IPv4 address to a link-layer address, usually a MAC address, on the local network.

For example, a computer might know that its destination is `192.168.1.20`, but it needs the corresponding Ethernet MAC address to deliver a frame directly on the local LAN.

### Why is ARP needed?

IP addresses are used for logical addressing and routing, while Ethernet frames use MAC addresses for local-link delivery.

When an IPv4 host needs to send an Ethernet frame to a local destination and does not already know the destination's MAC address, it can use ARP.

### How ARP works

Suppose Computer A (`192.168.1.10`) wants to send data to Computer B (`192.168.1.20`) on the same IPv4 LAN.

1. Computer A checks its ARP cache.
    
2. If the mapping is missing, A sends an ARP Request, usually as a local broadcast.
    
3. The device using `192.168.1.20` recognizes the request and responds with its MAC address.
    
4. A stores the mapping in its ARP cache for future use.
    
5. A sends the IP packet inside an Ethernet frame addressed to B's MAC address.
    

### ARP Request and Reply

Computer A

192.168.1.10

ARP Request

Broadcast

Computer B

192.168.1.20

ARP Reply

B's MAC address

A learns the local MAC address corresponding to B's IPv4 address and can then send Ethernet frames to B.

### What happens if the destination is on another network?

This is a very important exam detail.

Suppose the computer wants to send an IP packet to a remote server outside its LAN. It does not ordinarily ARP for the remote server's MAC address.

Instead:

1. It identifies that the destination IP is outside its local subnet.
    
2. It sends the packet to its default gateway.
    
3. If necessary, it uses ARP to resolve the gateway's local IPv4 address to its MAC address.
    
4. The router forwards the IP packet toward the remote network.
    

The Ethernet frame's destination MAC address is the next hop's MAC address; the IP packet's destination remains the remote server's IP address, subject to any relevant network-level transformations.

### Important ARP concepts

|Feature|Detail|
|---|---|
|Full form|Address Resolution Protocol|
|Primary purpose|Resolve IPv4 address to link-layer address on a local link|
|Common use|Ethernet LANs using IPv4|
|Request|Usually broadcast on the local LAN|
|Reply|Commonly unicast to the requester|
|Cache|Stores address mappings temporarily|
|OSI/TCP-IP classification|Commonly linked to Data Link / Network Access; often described as a boundary protocol|
|IPv6 equivalent|Neighbor Discovery Protocol (NDP), using ICMPv6|

ARP is not an application-layer protocol and is not used to resolve domain names. DNS does that.

### ARP versus DNS

|ARP|DNS|
|---|---|
|Maps an IPv4 address to a local link-layer address|Resolves domain names and other DNS records|
|Operates on the local link|Uses DNS client/server communication|
|Used for local frame delivery|Helps applications discover names and addresses|
|No TCP/UDP port number for classic ARP|Commonly UDP/TCP port 53|

### Security point

ARP spoofing or ARP poisoning occurs when an attacker sends deceptive ARP information to associate an IPv4 address with an incorrect MAC address. This can redirect traffic on a local network.

### Exam traps

- ARP resolves IPv4 → MAC, not domain name → IP.
    
- ARP requests are commonly broadcast on a local Ethernet LAN.
    
- ARP does not route packets between networks.
    
- For a remote destination, a host normally resolves the default gateway's MAC address, not the remote server's MAC address.
    
- IPv6 uses NDP rather than ARP for neighbour and link-layer address discovery.
    

# 13. Complete protocol comparison table

This is one of the most useful tables for final revision.

|Protocol|TCP/IP layer|Common port(s)|Main function|Key exam clue|
|---|---|---|---|---|
|TCP|Transport|No single default port; uses ports chosen by endpoints|Reliable, ordered byte stream|Three-way handshake|
|UDP|Transport|No single default port; uses ports chosen by endpoints|Connectionless datagrams|8-byte header|
|IP|Internet|Not applicable|Addressing and packet forwarding|IPv4 = 32-bit; IPv6 = 128-bit|
|HTTP|Application|TCP 80 conventionally|Web communication|Request-response|
|HTTPS|Application|TCP 443 conventionally; UDP 443 for HTTP/3/QUIC by default|Protected web communication|TLS|
|FTP|Application|TCP 21 control; TCP 20 in classic active mode|File transfer|Separate control and data connections|
|SMTP|Application|TCP 25, 587, 465 for common uses|Send and relay email|Outgoing email|
|POP3|Application|TCP 110; TCP 995 for implicit TLS|Retrieve email|Download-oriented mailbox access|
|DNS|Application|UDP/TCP 53|Resolve domain names and other records|Domain-name resolution|
|DHCPv4|Application|UDP 67 server; UDP 68 client|Automatic IPv4 configuration|DORA|
|ARP|Link / Network Access association|No TCP/UDP port|Resolve IPv4 address to local MAC address|Request and reply|

Port-number caution: These are conventional defaults, not immutable requirements. Services can be configured to use different ports. Also, ports identify transport endpoints; IP and ARP do not use TCP/UDP port numbers as their own addressing mechanism.

## 14. Common protocol mix-ups

### TCP vs IP

TCP handles reliable, ordered communication between transport endpoints. IP carries packets between networks using IP addresses.

### HTTP vs HTTPS

HTTP defines web requests and responses. HTTPS secures HTTP communication using TLS. A secure connection does not guarantee the website itself is trustworthy.

### FTP vs SMTP

FTP transfers files. SMTP sends and relays email. SMTP is not the standard protocol for downloading a mailbox to an email client.

### SMTP vs POP3

SMTP sends or relays outgoing messages; POP3 retrieves messages from a mail server.

### DNS vs DHCP

DNS resolves domain names and other records. DHCP gives clients network configuration such as an IP address and default gateway.

### ARP vs DNS

ARP resolves an IPv4 address to a local-link MAC address. DNS resolves names to records such as IP addresses. They solve different problems.

### UDP vs TCP

TCP provides a reliable, ordered byte stream. UDP provides datagrams without built-in delivery and ordering guarantees. UDP is not automatically the better choice for every low-latency application.

## 16. Last-minute revision sheet

Memorize these high-yield facts before moving to the next topic:

- TCP: Reliable, ordered stream; three-way handshake.
    
- UDP: Connectionless datagrams; 8-byte header.
    
- IP: Routing and logical addressing; IPv4 uses 32-bit addresses, IPv6 uses 128-bit addresses.
    
- HTTP: Web communication; conventional TCP port 80.
    
- HTTPS: HTTP secured using TLS; conventional TCP port 443, with HTTP/3 using QUIC over UDP.
    
- FTP: File transfer; TCP port 21 for control.
    
- SMTP: Send and relay email; TCP ports 25 and 587 are important.
    
- POP3: Retrieve email; TCP port 110, or 995 for implicit TLS.
    
- DNS: Name resolution; UDP/TCP port 53.
    
- DHCP: Automatic network configuration; IPv4 uses UDP ports 67 and 68.
    
- ARP: Resolve local IPv4 addresses to MAC addresses.
    

Best memory chain: TCP/UDP handle transport, IP handles routing, HTTP/HTTPS handle web communication, FTP transfers files, SMTP sends email, POP3 retrieves email, DNS resolves names, DHCP configures hosts, and ARP finds the local MAC address for an IPv4 destination.

Next, study IPv4 addressing, subnet masks, private/public IP addresses, IPv6, and subnetting. These build directly on IP, DHCP, DNS and ARP.