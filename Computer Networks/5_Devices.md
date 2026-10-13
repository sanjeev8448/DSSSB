## 1. Modem

Full form: Modulator-Demodulator

A modem is a communication device that converts data into signals suitable for a communication link and recovers the transmitted data at the receiving end. The exact process depends on the technology.

### How does a modem work?

- Modulation: Represents information by modifying a carrier signal's properties according to a defined scheme.
    
- Demodulation: Recovers the transmitted information from the received signal.
    

A modem commonly supports both functions, hence its name.

### Basic Modem Communication

Digital data

Modem

Modulation

Communication link

Carries the encoded signal

Modem

Demodulation

Digital data

### Types and applications

|Type|Common application|
|---|---|
|DSL modem|Internet over telephone-line infrastructure|
|Cable modem|Internet over cable-TV coaxial infrastructure|
|Cellular modem|Mobile data through a cellular network|
|Satellite modem|Communication through satellite infrastructure|

### Important exam facts

- Modem stands for Modulator-Demodulator.
    
- Modulation and demodulation are its defining functions.
    
- A modem is not the same as a router.
    
- A combined home device may contain a modem, router, Ethernet switch and Wi-Fi access point.
    

Exam trap: A modem provides the communication-link interface; a router forwards traffic between IP networks. They may be integrated into one physical box, but their functions are different.

## 2. NIC — Network Interface Card

A Network Interface Card (NIC) is a hardware interface that enables a computer or other device to connect to a network.

The NIC may be integrated into a motherboard or provided as a separate expansion card or adapter.

### Functions of a NIC

- Connects the device to a wired or wireless network.
    
- Transmits and receives network data.
    
- Handles relevant link-layer functions.
    
- Provides a MAC address in typical Ethernet and Wi-Fi interfaces.
    
- Works with the operating system's network driver.
    

### Computer with a Wired NIC

Computer

NIC

Network

### What is a MAC address?

A Media Access Control (MAC) address is a link-layer address associated with a network interface.

For example:

`00:1A:2B:3C:4D:5E`

This is an illustrative 48-bit address written in hexadecimal notation.

### NIC and OSI layer

In introductory networking exams, a traditional Ethernet NIC is generally associated with the Data Link layer (Layer 2) and the Physical layer (Layer 1), because it handles functions involving both framing and physical transmission.

Exam trap: A MAC address is not the same as an IP address.

- MAC address: Used for local-link delivery at Layer 2.
    
- IP address: Used for logical addressing and routing at Layer 3.
    

The MAC address alone does not normally identify a device's geographical location.

## 3. Repeater

A repeater is a network device that regenerates or restores a signal so it can travel farther through a communication medium.

A signal may weaken as it travels due to attenuation. A repeater receives the signal and regenerates it before sending it onward.

### Repeater

Incoming signal

Weakened

Repeater

Outgoing signal

Regenerated

### Functions

- Extends the reach of a communication link.
    
- Regenerates signals in traditional digital repeater systems.
    
- Helps overcome signal attenuation over a longer path.
    

### Advantages

- Extends communication distance.
    
- Simple function compared with a router or gateway.
    
- Does not need to make IP-routing decisions.
    

### Limitations

- Does not select a destination based on IP addresses.
    
- Does not normally filter traffic according to MAC addresses.
    
- Cannot fix every source of poor network performance; it does not automatically eliminate congestion.
    

### OSI layer

A traditional repeater operates at the Physical layer (Layer 1).

Exam trap: A repeater regenerates signals; it does not route packets or intelligently filter Ethernet frames.

## 4. Hub

A hub is a basic networking device that connects multiple devices in a LAN and repeats incoming signals to the other ports.

It is essentially a multiport repeater.

### Hub forwards signals to other ports

Hub

PC 1

PC 2

PC 3

PC 4

An incoming signal is repeated to the other ports; the hub does not selectively forward according to a destination MAC address.

### How a hub works

Suppose PC 1 sends a frame into a hub. The hub repeats the signal to the other connected ports, so PC 2, PC 3 and PC 4 may all receive it. The intended recipient processes the frame; the other devices generally discard it if it is not addressed to them.

### Characteristics

- Operates at the Physical layer (Layer 1).
    
- Does not maintain a MAC-address forwarding table.
    
- Shares the medium among connected devices.
    
- Traditional Ethernet hubs create a shared collision domain.
    
- Generally operates in half-duplex mode with traditional Ethernet.
    

### Advantages

- Simple to install.
    
- Historically inexpensive.
    
- Can connect several devices to one shared Ethernet segment.
    

### Disadvantages

- Sends signals to all other ports rather than selecting a destination.
    
- Can experience Ethernet collisions in traditional shared-medium operation.
    
- Uses shared bandwidth inefficiently as the number of active devices grows.
    
- Provides no intelligent Layer 2 filtering.
    

### Hub versus repeater

A repeater typically connects two segments or extends a link, while a hub provides multiple ports for a shared network segment. A hub is commonly described as a multiport repeater.

Exam trap: A hub does not learn MAC addresses or make forwarding decisions based on them. A switch does.

## 5. Switch

A network switch connects devices within a LAN and forwards Ethernet frames based on their destination MAC addresses.

An ordinary Layer 2 switch learns source MAC addresses from incoming frames and associates those addresses with the ports on which they were received.

### Switch forwarding

Ethernet switch

MAC address table

PC A

PC B

PC C

Printer

### How does a switch learn MAC addresses?

Consider this simplified process:

1. PC A sends an Ethernet frame to the switch.
    
2. The switch records the source MAC address and incoming port.
    
3. It examines the destination MAC address.
    
4. If the destination is known, it generally forwards the frame through the appropriate port.
    
5. If the destination is unknown, it typically floods the frame through eligible ports in the same VLAN, excluding the incoming port.
    

Broadcast frames are also flooded within the appropriate VLAN, subject to switch configuration.

### Advantages

- Forwards known unicast traffic selectively.
    
- Reduces unnecessary traffic to unrelated ports.
    
- Each full-duplex switched Ethernet link normally has its own collision domain.
    
- Supports efficient LAN communication.
    
- Can support VLANs and other advanced features depending on the model.
    

### Limitations

- A switch does not automatically route between separate IP networks unless it has Layer 3 routing functionality.
    
- Loops between switches must be managed; Layer 2 loops can cause broadcast storms.
    
- Switch capacity and configuration still matter for performance and security.
    

### OSI layer

A conventional Layer 2 Ethernet switch operates at the Data Link layer (Layer 2). A multilayer or Layer 3 switch can also route packets at Layer 3.

### Hub versus switch

|Feature|Hub|Layer 2 switch|
|---|---|---|
|OSI layer|Layer 1|Layer 2|
|Forwards using MAC table|No|Yes|
|Incoming unicast signal/frame|Repeated to other ports|Usually sent to the relevant port if destination is known|
|Collision domains|Traditionally one shared collision domain|Typically one per switched Ethernet port|
|Typical duplex|Half-duplex in traditional Ethernet|Full-duplex on modern links|
|Efficiency|Lower in shared-medium networks|Generally higher|

Exam trap: When a question simply says “switch,” the expected answer is usually Layer 2 and MAC-based forwarding. Remember that Layer 3 switches also exist.

## 6. Router

A router connects different IP networks and forwards packets between them using destination IP addresses and routing information.

For example, a home router connects your local network to your Internet service provider's network.

### Router connecting two networks

LAN A — Office

Router

IP routing table

WAN / Another network

### How does a router work?

When a router receives an IP packet, it examines the destination IP address, consults its routing table and selects the appropriate next hop and outgoing interface.

The router normally reduces the IPv4 Time to Live (TTL) or IPv6 Hop Limit as it forwards a packet. It then sends the packet onward in a new link-layer frame appropriate to the next network link.

### Main functions

- Connects separate IP networks.
    
- Forwards packets using routing information.
    
- Selects routes based on the routing table.
    
- Can separate broadcast domains.
    
- May provide NAT, DHCP, firewall and Wi-Fi functions in a home router, depending on the device.
    

### OSI layer

A traditional router operates at the Network layer (Layer 3).

### Advantages

- Connects different networks.
    
- Enables communication between subnets.
    
- Can select between available routes.
    
- Helps control traffic between networks.
    

### Limitations

- Requires routing configuration and appropriate addressing.
    
- Can introduce processing delay.
    
- A failed router may disconnect networks that depend on it, unless redundancy is available.
    

### Switch versus router

|Feature|Switch|Router|
|---|---|---|
|Main purpose|Connect devices within a LAN|Connect different IP networks|
|Common layer|Layer 2|Layer 3|
|Main forwarding information|MAC address table|IP routing table|
|Typical forwarding unit|Ethernet frame|IP packet|
|Separates IP networks?|Not normally with Layer 2 switching alone|Yes|
|Typical example|Connects office PCs|Connects office LAN to the Internet|

Exam trap: A router does not forward packets merely by looking at destination MAC addresses. It makes its routing decision primarily from the destination IP address.

When a packet moves through a router, the Layer 2 frame is replaced for the next link, while the IP packet is forwarded subject to normal IP processing.

## 7. Gateway

A gateway is a device or software system that acts as an entry or exit point between networks or systems. In the broad sense, it can also translate between different protocols, formats or application systems.

The word gateway is used in two important ways.

### A. Default gateway

A default gateway is the router or Layer 3 device that a host sends traffic to when the destination is outside the host's directly connected network and no more specific route applies.

Example: A PC on a home LAN sends a packet to an Internet destination. The PC forwards it to its configured default gateway, commonly the home router.

### B. Protocol gateway

A protocol gateway connects systems that use different protocols and may translate between them.

For example, a specialized gateway might connect an industrial control network to an IP-based monitoring system.

### Gateway between different systems

System A

Protocol A

Gateway

Translation

System B

Protocol B

### Gateway versus router

|Feature|Router|Gateway|
|---|---|---|
|Main role|Routes IP packets between networks|Broad term for an entry/exit point; may translate protocols|
|Typical operation|IP routing|Depends on gateway type|
|OSI layer|Layer 3 for conventional routing|Can operate at several layers|
|Example|Home router routing LAN traffic to an ISP|Protocol converter or default gateway|

### Very important exam clarification

In many basic networking questions, the default gateway is a router. In other questions, a gateway performs translation between unlike protocols or systems.

A router can therefore function as a default gateway, but the general term gateway is broader than a router.

Exam trap: If the question asks for the device that routes packets between IP networks, choose router. If it asks for a translator between dissimilar protocols, choose gateway.

## 8. Wi-Fi adapter

A Wi-Fi adapter is a network interface that enables a device to connect to a wireless LAN using Wi-Fi, based on IEEE 802.11 standards.

It may be integrated into a laptop or phone, built into an expansion card, or connected externally through USB.

### How it works

1. The adapter transmits and receives radio signals.
    
2. It exchanges Wi-Fi frames with a wireless access point or another supported Wi-Fi device.
    
3. It uses a wireless interface's link-layer functions, including MAC addressing.
    
4. The operating system uses the adapter and its driver to provide network connectivity.
    

### Wi-Fi connection

Laptop

Wi-Fi adapter

Radio link

Access point

The access point provides wireless LAN connectivity and may connect onward to a router or other network.

### Types

- Integrated: Built into a laptop, tablet or phone.
    
- USB adapter: External adapter connected through a USB port.
    
- PCIe adapter: Internal desktop adapter, often with external antennas.
    

### Advantages

- Provides wireless connectivity without an Ethernet cable to the device.
    
- Allows mobility within the coverage area.
    
- Convenient for laptops and portable equipment.
    

### Limitations

- Performance depends on signal strength, interference, distance, obstacles and congestion.
    
- Wireless security and proper configuration are important.
    
- A Wi-Fi adapter alone does not necessarily provide Internet access; it must connect to a suitable network that has the required connectivity.
    

### Wi-Fi adapter versus router

A Wi-Fi adapter allows an endpoint to join a wireless network. A wireless router usually routes IP traffic and may also contain a wireless access point, switch and other functions.

Exam trap: An adapter is a type of network interface, not automatically a router. Wi-Fi devices transmit radio signals but still use network-layer IP when communicating over IP networks.

## 9. OSI layers — most important comparison

These are the conventional OSI layer classifications expected in introductory networking exams.

|Device|Main OSI layer|Key function|
|---|---|---|
|Repeater|Layer 1 — Physical|Regenerates signals|
|Hub|Layer 1 — Physical|Repeats signals to other ports|
|NIC|Layer 1 and Layer 2 functions|Connects a device to the network|
|Wi-Fi adapter|Layer 1 and Layer 2 functions|Wireless network interface|
|Layer 2 switch|Layer 2 — Data Link|Forwards frames using MAC addresses|
|Router|Layer 3 — Network|Routes packets using IP addresses|
|Gateway|Depends on its function; can operate across layers|Connects or translates between systems|
|Modem|Depends on implementation; commonly associated with physical-layer signalling|Modulates and demodulates signals|

Remember: A gateway does not have one universal OSI layer. A protocol-converting application gateway may operate at higher layers, while the default gateway on a host is commonly a router operating at Layer 3.

NICs and modems can also involve functions that cross strict OSI boundaries, so questions usually expect the primary function rather than a claim that the hardware operates exclusively at one layer.

## 10. Master comparison table

|Device|Main job|Main information or signal it handles|Typical exam clue|
|---|---|---|---|
|Modem|Modulation and demodulation|Communication signals|Modulator-Demodulator|
|NIC|Network connection for an endpoint|Frames and physical transmission|MAC address / network interface|
|Repeater|Regenerate a signal|Signal|Extends transmission distance|
|Hub|Repeat incoming signals to other ports|Physical-layer signal|Multiport repeater|
|Switch|Forward frames within a LAN|MAC addresses|MAC address table|
|Router|Connect IP networks|IP addresses|Routing table|
|Gateway|Connect or translate between systems|Depends on function|Protocol conversion / default route|
|Wi-Fi adapter|Connect an endpoint to a wireless LAN|Wi-Fi radio and frames|IEEE 802.11|

### Quick scenarios

- A weak signal needs regeneration: Repeater.
    
- Several Ethernet devices need a simple shared connection: Hub in a traditional networking scenario.
    
- Office PCs need efficient MAC-based communication: Switch.
    
- Two different IP networks need to communicate: Router.
    
- A device must connect to Wi-Fi: Wi-Fi adapter.
    
- Copper or optical communication needs a suitable modem function: Modem, where the access technology requires one.
    
- A host needs a next hop to reach an external network: Default gateway, usually a router.
    
- Two unlike protocol systems need translation: Gateway.
    
- A computer needs hardware or a logical interface for network access: NIC.
Revision order: First memorize the Layer 1, Layer 2 and Layer 3 devices; then revise the distinction between MAC addressing, IP routing, signal regeneration and protocol translation. Those comparisons are especially useful for elimination-based MCQs.