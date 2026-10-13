# Part A — Network Evolution

## 1. ARPANET

Full form: Advanced Research Projects Agency Network

ARPANET was an early packet-switching computer network developed with funding from the United States Department of Defense's Advanced Research Projects Agency (ARPA). It is widely regarded as a major predecessor of the modern Internet.

![](https://www.google.com/s2/favicons?domain=https://www.darpa.mil&sz=32)

DARPA

+1

### Why was ARPANET developed?

Initially, computers at universities and research institutions operated independently. Researchers needed a way to share computing resources and communicate across geographically separated locations.

ARPANET helped demonstrate that computers connected through a packet-switched network could communicate over long distances.

### Important facts about ARPANET

|Feature|Detail|
|---|---|
|Developed under|ARPA, United States|
|First four-node network|1969|
|Main networking approach|Packet switching|
|Initial host communication protocol|NCP — Network Control Protocol|
|Major protocol transition|TCP/IP adopted on 1 January 1983|
|Historical importance|Major predecessor of the Internet|

The first four ARPANET nodes were at UCLA, Stanford Research Institute (SRI), UC Santa Barbara and the University of Utah.

![](https://www.google.com/s2/favicons?domain=https://www.darpa.mil&sz=32)

DARPA

+1

### What is packet switching?

In packet switching, data is divided into smaller units called packets. These packets are transmitted through the network and then reassembled or processed at the destination.

For example, when sending a large file, the networking system can divide its data into multiple packets rather than treating the entire file as one indivisible transmission.

Packet Switching — Basic Idea

Original message

Packet 1

Packet 2

Packet 3

Network transmission

Destination processes data

Packets may travel through different paths depending on network conditions and routing decisions.

### NCP versus TCP/IP

Initially, ARPANET used NCP for communication between hosts. As internetworking developed, TCP/IP enabled different networks to interconnect using common protocols.

On 1 January 1983, ARPANET made the significant transition from NCP to TCP/IP.

![](https://www.google.com/s2/favicons?domain=https://www.internetsociety.org&sz=32)

Internet Society

+1

Exam trap: ARPANET did not use TCP/IP from the very beginning. The 1983 transition is the key date to remember.

## 2. NSFNET

Full form: National Science Foundation Network

NSFNET was developed under the United States National Science Foundation (NSF) to connect academic researchers and supercomputing centres. It became a major backbone of the expanding Internet during the late 1980s and early 1990s.

![](https://www.google.com/s2/favicons?domain=https://www.nsf.gov&sz=32)

NSF - U.S. National Science Foundation

+1

### Why was NSFNET needed?

As demand for academic and research networking grew, a larger, higher-speed infrastructure was needed to connect universities, research institutions and regional networks.

NSFNET helped expand networking beyond the earlier ARPANET environment and contributed significantly to the growth of the Internet.

### Important facts about NSFNET

|Feature|Detail|
|---|---|
|Organization|National Science Foundation (NSF), United States|
|Initial backbone operational|1986|
|Original purpose|Connect supercomputing centres and academic researchers|
|Backbone rate in 1986|56 kbps|
|Major upgrade in 1988|1.5 Mbps (T1)|
|Backbone rate by 1991|45 Mbps (T3)|
|Backbone retirement|1995|

The backbone's growth from 56 kbps to 45 Mbps illustrates how rapidly network capacity expanded. The NSFNET backbone was retired in 1995 as commercial Internet infrastructure took over much of its role.

![](https://www.google.com/s2/favicons?domain=https://nsf.net&sz=32)

NSFNET

+2

### ARPANET versus NSFNET

|Feature|ARPANET|NSFNET|
|---|---|---|
|Main sponsoring organization|ARPA|NSF|
|Major early role|Research into packet networking and computer communication|Connect academic researchers and supercomputing centres|
|Key year|1969 — four-node network|1986 — backbone operational|
|Historical contribution|Important predecessor of Internet networking|Major backbone for Internet expansion|
|Fate|Deactivated in 1989|Backbone retired in 1995|

Sources: DARPA's ARPANET history and the NSFNET history.

![](https://www.google.com/s2/favicons?domain=https://www.darpa.mil&sz=32)

DARPA

+1

Exam trap: ARPANET and NSFNET were not identical networks. ARPANET was an early research network; NSFNET later played a major role in expanding academic networking and Internet backbone connectivity.

## 3. Internet

The Internet is a global network of interconnected networks that communicate using the TCP/IP protocol suite.

It connects millions of private, public, educational, business and government networks worldwide.

The Internet did not emerge from one single invention. It developed through packet-switching research, internetworking protocols, interconnected networks and the growth of public and commercial connectivity.

![](https://www.google.com/s2/favicons?domain=https://www.internetsociety.org&sz=32)

Internet Society

+1

### Major stages in Internet evolution

### 1969 — ARPANET

Established an early four-node packet-switched network connecting research institutions.

### 1 January 1983 — TCP/IP transition

ARPANET switched from NCP to TCP/IP, a milestone in the development of interoperable networking.

### 1986 — NSFNET backbone

NSFNET connected supercomputing centres and helped expand academic and research networking.

### 1990s — Wider Internet growth

Commercial networking expanded. NSFNET's backbone was retired in 1995 as Internet infrastructure transitioned toward commercial providers.

The dates above are useful milestones, not a claim that the Internet began on only one specific day.

![](https://www.google.com/s2/favicons?domain=https://www.darpa.mil&sz=32)

DARPA

+2

### Internet versus World Wide Web (WWW)

This distinction is very important in Computer Science exams.

|Internet|World Wide Web|
|---|---|
|Global interconnection of networks|Information system that operates over the Internet|
|Uses a range of protocols, including IP, TCP, UDP and others|Commonly uses HTTP/HTTPS to access linked resources|
|Supports web browsing, email, file transfer, voice/video communication and more|Connects web pages and other web resources through hyperlinks|
|Developed through multiple research and engineering efforts|Invented by Tim Berners-Lee at CERN in 1989|

The World Wide Web is one service that uses the Internet, not another name for the entire Internet.

![](https://www.google.com/s2/favicons?domain=https://home.cern&sz=32)

CERN

+1

Other Internet services include email, online gaming, remote access and voice/video calls. Not every Internet service is part of the Web.

### What does TCP/IP do?

- IP (Internet Protocol): Provides addressing and packet forwarding between networks.
    
- TCP (Transmission Control Protocol): Provides reliable, ordered delivery of a byte stream between endpoints.
    
- UDP (User Datagram Protocol): Provides datagram-based transport without built-in guarantees of delivery or ordering.
    

Exam memory point: TCP/IP helped networks using different underlying technologies communicate through common protocols, making large-scale internetworking possible.

![](https://www.google.com/s2/favicons?domain=https://www.internetsociety.org&sz=32)

Internet Society

+1

# Part B — Types of Networks

Networks can be classified by their geographical coverage. The three core types in your syllabus are LAN, MAN and WAN.

## 4. LAN — Local Area Network

A Local Area Network (LAN) connects devices over a relatively small geographical area, such as a room, home, office, laboratory, school building or a limited site.

### Examples

- Computers connected in a computer lab.
    
- Devices connected to a home Wi-Fi router.
    
- Computers and printers connected within an office.
    

### Characteristics

- Usually covers a relatively small area.
    
- Often owned or managed by an individual or organization.
    
- Common technologies include Ethernet and Wi-Fi.
    
- Typically offers high local data rates and relatively low latency.
    
- Can share files, printers, applications and Internet access.
    

A LAN may be wired, wireless or a combination of both.

### Example: Office LAN

Router / Gateway

LAN Switch

PC 1

PC 2

Printer

Devices communicate through the local network. The gateway can connect the LAN to other networks, including the Internet.

Exam trap: A LAN does not have to connect directly to the Internet. Devices within a LAN can communicate locally even when Internet access is unavailable.

## 5. MAN — Metropolitan Area Network

A Metropolitan Area Network (MAN) connects networks across a metropolitan area, such as a city or a large urban region.

It is often used to interconnect multiple LANs belonging to a university, business or service provider.

### Examples

- A network connecting university buildings across a city.
    
- A city-wide fibre network linking organizational sites.
    
- A metropolitan network connecting branches of an institution.
    

### Characteristics

- Covers a larger geographical area than a typical LAN.
    
- Commonly interconnects multiple LANs.
    
- May use fibre-optic links, provider infrastructure or wireless links.
    
- May be operated by a telecommunications provider, government organization, university or enterprise.
    
- Can offer high-speed connectivity across urban locations.
    

### Example: City-wide MAN

Office LAN

College LAN

Hospital LAN

Metropolitan backbone

The metropolitan network connects separate local networks around the city.

Exam trap: MAN is defined mainly by geographical scope and the interconnection of networks, not by a guaranteed speed or a particular cable type.

## 6. WAN — Wide Area Network

A Wide Area Network (WAN) connects devices or networks across large geographical areas, potentially spanning countries and continents.

WAN links can use leased lines, fibre-optic infrastructure, provider networks, microwave links, satellite links and undersea cables.

### Examples

- A company connecting offices in Delhi, Mumbai and London.
    
- A bank connecting branches throughout a country.
    
- An international organization connecting networks worldwide.
    
- The Internet, considered as a global interconnection of networks.
    

### Characteristics

- Covers a larger area than a typical LAN or MAN.
    
- Often interconnects geographically separated LANs and MANs.
    
- Frequently uses telecommunications providers or other carrier infrastructure.
    
- May have varied bandwidth, cost and latency depending on the links used.
    
- Can use public, private or hybrid infrastructure.
    

### Example: Company WAN

Delhi LAN

WAN links

London LAN

A WAN allows separated offices to exchange data across long distances.

Exam trap: A WAN does not necessarily mean a public network. An organization can build or lease a private WAN to connect its own offices.

## 7. LAN vs MAN vs WAN — comparison table

|Feature|LAN|MAN|WAN|
|---|---|---|---|
|Full form|Local Area Network|Metropolitan Area Network|Wide Area Network|
|Typical coverage|Room, building, limited site|City or metropolitan region|Country, continent or global|
|Main purpose|Connect local devices|Interconnect networks across a city|Interconnect geographically distant networks|
|Example|Computer lab|City-wide university network|International company network|
|Common infrastructure|Ethernet, Wi-Fi|Metro fibre, provider links|Leased lines, carrier networks, fibre, satellite|
|Typical ownership|Individual or organization|Provider, authority or organization|Multiple providers or a private organization|
|Relative scope|Smallest|Intermediate|Largest|

These are typical patterns, not strict rules: speed, ownership and technology alone do not determine whether a network is a LAN, MAN or WAN.

### Quick identification examples

- Computers in one computer lab: LAN.
    
- An enterprise network linking sites across Delhi: typically a MAN if it is a metropolitan network.
    
- A bank linking branches across India: WAN.
    
- A company connecting Indian and European offices: WAN.
    
- The Internet: global network of interconnected networks, commonly treated as a WAN-scale network.
    

One nuance: networks spanning a large university campus may be classified as a Campus Area Network (CAN) in some textbooks. Follow the exact terminology and classification used in your prescribed syllabus if a question specifically mentions CAN.

## 9. Last-minute revision sheet

Memorize these facts before moving on:

- ARPANET — 1969: early packet-switched network, important predecessor of the Internet.
    
- TCP/IP transition — 1 January 1983: major protocol milestone.
    
- NSFNET — 1986: academic and supercomputing network; backbone retired in 1995.
    
- WWW — 1989: invented by Tim Berners-Lee at CERN; it is not the same as the Internet.
    
- LAN: local area, such as a building or office.
    
- MAN: metropolitan area, such as a city.
    
- WAN: wide area, such as a country or the globe.
    

Historical references: [DARPA — ARPANET](https://www.darpa.mil/news/features/arpanet), [Internet Society — Internet history](https://www.internetsociety.org/internet/history-internet/brief-history-internet-related-networks/) and [CERN — History of the Web](https://home.cern/science/computing/the-birth-of-the-web/short-history-web/).