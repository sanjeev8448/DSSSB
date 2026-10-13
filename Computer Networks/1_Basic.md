## 1. Network

A computer network is a collection of two or more computers or other devices connected through communication links so they can exchange data and share resources.

Examples include a home Wi-Fi network, computers in an office connected to a local network, and the Internet.

Example: Office Computer Network

Computer A

Switch / Network

Computer B

The computers can exchange data and may share resources such as files and printers.

### Why do we need computer networks?

- Resource sharing: Share printers, files, storage and applications.
    
- Communication: Email, messaging, video calls and file transfer.
    
- Data sharing: Exchange information between connected devices.
    
- Centralized management: Manage accounts, data and security through servers.
    
- Remote access: Access systems or services from another location.
    

### Common network types

|Network|Full form / meaning|Typical coverage|
|---|---|---|
|PAN|Personal Area Network|Around an individual; e.g. Bluetooth|
|LAN|Local Area Network|Room, home, office or building|
|MAN|Metropolitan Area Network|City or metropolitan area|
|WAN|Wide Area Network|Large geographical areas|
|WLAN|Wireless LAN|Local network using wireless communication|

Exam trap: The Internet is commonly described as a global network of networks. A LAN normally covers a smaller area than a WAN, but the exact boundaries depend on the network design.

## 2. Communication

Data communication is the exchange of data between two or more devices through a transmission medium according to agreed rules.

For successful data communication, five basic components are commonly identified:

1. Sender: The device that sends data.
    
2. Receiver: The device that receives data.
    
3. Message: The information being communicated.
    
4. Transmission medium: The path through which the data travels.
    
5. Protocol: The rules governing communication.
    

Basic Data Communication Model

Sender

Medium

Receiver

Protocols define how the sender and receiver format, transmit and interpret the data.

For example, when you send a WhatsApp message, your phone acts as the sender, your message is the data, communication links carry the data, and the recipient's phone receives it. Network protocols govern the communication.

### Characteristics of effective data communication

|Characteristic|Meaning|
|---|---|
|Delivery|Data reaches the intended destination.|
|Accuracy|Data arrives without unintended corruption.|
|Timeliness|Data arrives when it is needed.|
|Jitter|Variation in the arrival times of packets; important for audio and video.|

Remember: Accuracy concerns correctness, while timeliness concerns delay. Jitter is not the same thing as latency.

## 3. Sender

A sender is the source device or entity that initiates a data transmission.

Examples include a computer uploading a file, a mobile phone sending a message, and a server responding to a request.

At a basic level, the sender:

1. Produces the message.
    
2. Encodes the data into a form suitable for transmission.
    
3. Sends it through the communication system.
    

The actual networking process can involve several protocol layers and intermediary devices.

Exam point: Sender and source refer to the origin of a communication. In a reply or reverse-direction exchange, the original receiver may become the sender.

## 4. Receiver

A receiver is the destination device or entity for which transmitted data is intended.

Examples include a computer receiving a file, a phone receiving a message, or a server receiving a browser request.

At a basic level, the receiver obtains the transmitted signals, interprets the encoded information, and delivers the data to the appropriate application or process.

The receiver may check whether data is corrupted and, when the protocol supports it, request retransmission or send acknowledgements.

Exam trap: Receiving data does not necessarily mean that the application has successfully processed it. Network delivery and application processing are different stages.

## 5. Message

A message is the information exchanged between communicating entities.

Messages can contain text, images, audio, video, files, commands or numerical data.

For example, the text `HELLO` is a message. Before transmission, its characters are represented using an encoding, such as ASCII or UTF-8, and the resulting data is carried by the communication system.

### Message, data and packet

|Term|Meaning|
|---|---|
|Message|Information intended to be communicated|
|Data|Information represented in a form that can be stored or processed|
|Packet|A unit of network-layer data transmitted over a network|
|Frame|A data-link-layer unit carried over a particular link|
|Bit|A binary digit: `0` or `1`|

A large message may be divided into multiple packets for transmission. Packets can then be encapsulated inside frames on individual network links.

Important: A message is not necessarily the same size as one packet. Nor is every message necessarily split into packets.

## 6. Protocol

A network protocol is a set of rules that controls how devices communicate and exchange data.

A protocol specifies matters such as message format, addressing, timing, sequencing, error handling and what devices should do when communication problems occur. The exact rules depend on the protocol.

### Three fundamental aspects of a protocol

|Aspect|Meaning|Example|
|---|---|---|
|Syntax|Format and structure of data|Order and layout of header fields|
|Semantics|Meaning of fields and required actions|What an acknowledgement indicates|
|Timing|When data is sent and at what rate|Transmission timing or synchronization|

These three terms are especially useful for objective examination questions.

### Common network protocols

|Protocol|Main purpose|
|---|---|
|HTTP|Transfers web content|
|HTTPS|HTTP secured using TLS|
|FTP|File transfer|
|SMTP|Sending email|
|POP3|Retrieving email, commonly by downloading it|
|IMAP|Accessing and synchronizing email on a server|
|DNS|Resolves domain names to DNS records, including IP addresses|
|DHCP|Automatically provides IP configuration to clients|
|TCP|Reliable, ordered byte-stream transport|
|UDP|Connectionless transport with low protocol overhead and no built-in delivery guarantee|
|IP|Addressing and forwarding packets between networks|
|Ethernet|Common wired LAN technology|
|Wi-Fi|Wireless LAN technology based on IEEE 802.11|

### Example: Opening a website

When you open a website, several protocols may work together:

1. DNS may help resolve the website's domain name.
    
2. IP carries packets toward the destination.
    
3. TCP may provide transport for an HTTPS connection, or QUIC may be used with HTTP/3.
    
4. TLS provides security for HTTPS.
    
5. HTTP defines how the browser and server exchange web requests and responses.
    

Exam traps:

- HTTP is an application-layer protocol; IP is a network-layer protocol.
    
- TCP and UDP are transport-layer protocols.
    
- DNS is not the same as DHCP: DNS resolves names, while DHCP provides network configuration.
    
- HTTPS is not a separate replacement for HTTP's request/response model; it is HTTP secured using TLS.
    
- A protocol is a set of communication rules, not a physical cable or device.
    

## 7. Bandwidth

In computer networks, bandwidth has two closely related uses, so read the context of a question carefully.

### A. Digital communication bandwidth

This is the range of frequencies occupied or supported by a signal or communication channel, measured in hertz (Hz).

For a channel operating between frequencies \(f_H\) and \(f_L\):

\[ \text{Bandwidth}=f_H-f_L \]

Example: A channel operating from 1 MHz to 5 MHz has a bandwidth of:

\[ 5-1=4\text{ MHz} \]

### B. Internet or network bandwidth

In everyday networking, bandwidth is often used to mean the maximum or nominal data-carrying capacity of a link, commonly expressed in bits per second (bps).

For example, a link rated at 100 Mbps has a nominal capacity of 100 million bits per second.

This is different from the amount of data actually delivered per second. Real throughput may be lower because of protocol overhead, congestion, signal conditions and other limitations.

### Analogy

Imagine a road:

- Bandwidth: how much capacity is available.
    
- Data rate: how quickly bits are being transmitted at a given time.
    
- Throughput: how much useful data is actually delivered per unit of time.
    

The analogy is not exact, but it helps to separate the concepts.

### Bandwidth-related terms

|Term|Meaning|Usual unit|
|---|---|---|
|Frequency bandwidth|Width of the frequency range|Hz, kHz, MHz|
|Link capacity / nominal bandwidth|Maximum or rated data-carrying capacity|bps, Mbps, Gbps|
|Data rate|Bits transmitted per second|bps|
|Throughput|Actual rate of successful data delivery|bps|
|Goodput|Useful application data delivered per second, excluding protocol overhead and retransmitted data|bps|
|Latency|Time taken for data to travel between endpoints|ms, µs|
|Jitter|Variation in packet delay|ms, µs|

Exam trap: In signal theory, bandwidth is measured in hertz. In practical Internet discussions, it is commonly expressed in bits per second. Do not automatically use Hz for a question about a link's 100 Mbps capacity.

## 8. Data rate

Data rate is the number of bits transmitted per unit of time. It is normally measured in bits per second (bps).

The basic formula is:

\[ \boxed{\text{Data rate}=\frac{\text{Number of bits transmitted}}{\text{Transmission time}}} \]

For example, if 12,000 bits are transmitted in 2 seconds:

\[ \text{Data rate}=\frac{12,000}{2}=6,000\text{ bps} \]

Therefore, the data rate is 6 kbps using the decimal networking convention.

### Units of data rate

|Unit|Meaning|Decimal value|
|---|---|---|
|bps|Bits per second|1 bit/s|
|kbps|Kilobits per second|\(10^3\) bps|
|Mbps|Megabits per second|\(10^6\) bps|
|Gbps|Gigabits per second|\(10^9\) bps|
|Tbps|Terabits per second|\(10^{12}\) bps|

In networking, these prefixes generally use the decimal system.

### Bits versus bytes

This is a very common source of errors.

- b means bit.
    
- B means byte.
    
- One byte normally contains 8 bits.
    

Hence:

\[ 1\text{ MB}=8\text{ Mb} \]

under decimal units, assuming 1 byte = 8 bits.

Suppose a file is 20 MB and the connection's data rate is 40 Mbps. Ignoring overhead and other delays:

\[ \text{Time}=\frac{20\times8\text{ Mb}}{40\text{ Mbps}} =\boxed{4\text{ seconds}} \]

The file size must be converted from megabytes to megabits before dividing by Mbps.

In real networks, the actual download may take longer because link rate is not necessarily equal to application goodput.

### Data rate versus baud rate

Bit rate is measured in bits per second, while baud rate is measured in symbols per second.

A symbol can represent one bit or multiple bits, depending on the modulation scheme.

\[ \text{Bit rate}=\text{Symbol rate}\times\text{Bits per symbol} \]

For example, if a communication system transmits 2,000 symbols per second and each symbol represents 4 bits:

\[ 2,000\times4=\boxed{8,000\text{ bps}} \]

Here, the baud rate is 2,000 baud and the bit rate is 8,000 bps.

Exam trap: Bit rate and baud rate are not always equal. They are equal when each symbol represents exactly one bit.

## 9. Bandwidth versus data rate versus throughput

This comparison is especially important because exam questions often use these terms together.

|Feature|Bandwidth / capacity|Data rate|Throughput|
|---|---|---|---|
|What it describes|Available frequency range or rated link capacity, depending on context|Rate at which bits are transmitted|Rate of successful data delivery|
|Typical unit|Hz or bps, depending on meaning|bps|bps|
|Example|Link capacity rated at 100 Mbps|Bits sent at 80 Mbps at a given time|Useful data delivered at 72 Mbps|
|Always equal?|No|No|No|

Imagine that a link has a rated capacity of 100 Mbps. A sender transmits at 80 Mbps, while the receiver gets 72 Mbps of successfully delivered data. In that example:

- Rated capacity = 100 Mbps
    
- Data transmission rate = 80 Mbps
    
- Throughput = 72 Mbps
    

These numbers are illustrative, not a rule that throughput must always be a fixed percentage of bandwidth.

### Quick distinction to memorize

- Bandwidth: capacity or frequency range, depending on context.
    
- Data rate: bits per second being transmitted.
    
- Throughput: successful data delivery per second.
    
- Goodput: useful application data delivered per second.
    
- Latency: delay.
    
- Jitter: variation in delay.
    

## 10. Basic numerical practice

### Example 1 — Calculate data rate

A system transfers 50,000 bits in 5 seconds.

\[ R=\frac{50,000}{5}=10,000\text{ bps} \]

Answer: 10 kbps.

### Example 2 — Calculate transmission time

A 10 Mb file must be transmitted across a link at 5 Mbps. Ignore overhead.

\[ T=\frac{\text{Data size in bits}}{\text{Data rate}} =\frac{10\text{ Mb}}{5\text{ Mbps}} \]

Answer: 2 seconds.

### Example 3 — Find frequency bandwidth

A communication channel extends from 2 MHz to 8 MHz.

\[ B=8-2=6\text{ MHz} \]

Answer: 6 MHz.

### Example 4 — Convert MB to Mb

A file contains 4 MB of data. Assuming decimal units:

\[ 4\text{ MB}\times8=32\text{ Mb} \]

At 8 Mbps, the ideal transmission time is:

\[ T=\frac{32}{8}=4\text{ seconds} \]

Answer: 4 seconds, ignoring overhead and other delays.

### Example 5 — Find bit rate from baud rate

A modem transmits at 1,200 baud with 8 bits represented by each symbol.

\[ R=1,200\times8=9,600\text{ bps} \]

Answer: 9,600 bps.

## 11. High-yield exam revision

|Question|Correct concept|
|---|---|
|Rules that govern communication|Protocol|
|Origin of a transmission|Sender|
|Intended destination|Receiver|
|Information being exchanged|Message|
|Exchange of data between devices|Data communication|
|Unit of frequency bandwidth|Hertz (Hz)|
|Unit of bit rate|Bits per second (bps)|
|Unit of baud rate|Symbols per second (baud)|
|1 byte|8 bits|
|Actual successful data delivery rate|Throughput|
|Useful application data rate|Goodput|
|Variation in packet delay|Jitter|
|Protocol elements often described as three aspects|Syntax, semantics and timing|
|DNS|Name resolution|
|DHCP|Dynamic network configuration|

Memory trick: A Sender sends a Message through a medium to a Receiver; a Protocol defines the rules, Bandwidth describes channel range or capacity, and Data rate tells how many bits are transmitted per second.