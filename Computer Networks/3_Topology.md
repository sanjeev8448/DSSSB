
## 1. What Is Network Topology?

Network topology is the arrangement of devices (nodes) and communication links in a computer network.

- **Node:** A device connected to a network, such as a computer, printer, or router.
    
- **Link:** A communication connection between devices.
    
- **Physical topology:** The physical arrangement of cables, devices, and connections.
    
- **Logical topology:** How data flows between devices, regardless of the physical arrangement.
    

Example: Devices may be physically connected to a central switch in a star topology, while the switch determines how frames are forwarded through the network.

The five topologies in this syllabus are Bus, Star, Ring, Mesh, and Tree.

## 2. Bus Topology

A bus topology connects multiple devices to a common communication cable called the backbone.

### How It Works

All devices share the same main communication cable. When a device transmits data, the signal travels along the bus and is available to connected devices. The intended destination processes the data.

In traditional coaxial Ethernet bus networks, terminators are placed at both ends of the backbone to prevent signal reflections.

### Advantages

- Requires less cable than many point-to-point arrangements.
    
- Relatively inexpensive for a small network.
    
- Does not require a central switch or hub.
    
- Simple to understand and implement in small setups.
    

### Disadvantages

- A break in the main backbone can disrupt communication across the network.
    
- Shared transmission capacity can limit performance as traffic increases.
    
- Collisions can occur in traditional shared-medium Ethernet.
    
- Troubleshooting a backbone fault can be difficult.
    
- Adding devices or extending the cable can be inconvenient.
    

### Important Exam Facts

- Main component: Common backbone cable.
    
- Traditional bus Ethernet uses terminators at both ends.
    
- Failure of a single device's branch connection may affect that device, while a backbone break can affect the entire bus.
    
- Traditional shared-bus Ethernet is associated with collisions.
    

**Memory trick:** Bus = one common backbone.

## 3. Star Topology

A star topology connects every device to a central device, usually a switch or hub.

### How It Works

Every device has a separate connection to the central hub or switch.

- With a hub, incoming signals are repeated to all other ports.
    
- With a switch, frames are usually forwarded to the appropriate port based on the destination MAC address, when the switch has learned the destination.
    

Modern wired Ethernet LANs commonly use a physical star or extended-star arrangement.

### Advantages

- Easy to install, manage, and expand.
    
- Failure of one device's cable generally affects only that device.
    
- Faults are comparatively easy to isolate.
    
- With a switch, devices can communicate efficiently without sharing one collision domain as they would on a traditional hub-based Ethernet segment.
    

### Disadvantages

- Failure of the central switch or hub can disrupt all devices connected through it.
    
- Requires more cabling than a simple bus.
    
- The central device adds cost.
    
- The central device's capacity can become a performance bottleneck.
    

### Failure Analysis

|Failure|Typical Effect|
|---|---|
|One computer fails|Other devices can continue communicating|
|One computer's link fails|That computer generally loses its network connection|
|Central switch fails|The connected star network is disrupted|
|Central hub fails|The connected star network is disrupted|

**Memory trick:** Star = all devices connect to a centre.

## 4. Ring Topology

A ring topology connects each device to its neighbouring devices, forming a closed loop.

### How It Works

Data travels from one node to the next around the ring. Depending on the technology, a ring network may use an access-control mechanism such as token passing.

In a token-passing arrangement, a special control frame called a token circulates. A device transmits when it obtains permission through the token mechanism.

Not every ring topology necessarily uses token passing.

### Advantages

- Data transmission can be orderly in token-controlled systems.
    
- Access to the medium can be predictable under suitable operating conditions.
    
- Each node can regenerate or forward data in some ring implementations.
    
- A simple ring does not inherently require a central hub.
    

### Disadvantages

- In a basic single ring, one broken link or failed node may interrupt the entire ring.
    
- Adding or removing devices can disrupt a basic ring during reconfiguration.
    
- A fault can be harder to locate than in a simple star.
    
- Delay may increase as data passes through more intermediate nodes.
    

### Important Exam Facts

- Shape: Closed loop or circle.
    
- Traditional token ring systems use token passing to control access.
    
- In a basic single ring, a link failure can break the communication path.
    
- Dual-ring designs and other protection mechanisms can provide resilience.
    

**Memory trick:** Ring = each node connects to its neighbours in a loop.

## 5. Mesh Topology

A mesh topology connects devices through multiple links, providing alternative paths for communication.

There are two main types.

### A. Full Mesh

Every node is directly connected to every other node.

### B. Partial Mesh

Only some pairs of nodes have direct connections. Multiple paths may still exist between important nodes, depending on the design.

### Number of Links in a Full Mesh

For n nodes, the number of direct links required is:

L = n(n − 1) / 2

Why? Each of the n nodes can connect to n − 1 other nodes, but counting n(n − 1) counts every link twice. Therefore, divide by 2.

**Worked example:** How many links are needed to fully mesh 5 nodes?

L = 5(5 − 1) / 2

L = 5 × 4 / 2

L = 20 / 2

**L = 10 links**

For a full mesh, each node has n − 1 direct links. Thus, with 5 nodes, every node has 4 links.

### Advantages

- High reliability because multiple alternative paths may exist.
    
- A single link failure usually does not disconnect the entire network.
    
- Fault isolation can be easier when connectivity is redundant.
    
- Dedicated links can reduce contention on individual connections.
    

### Disadvantages

- Requires a large number of links and interfaces in a full mesh.
    
- Installation and maintenance can be expensive.
    
- Configuration becomes complex as the number of nodes grows.
    
- Full mesh becomes impractical for large numbers of endpoints.
    

### Important Exam Facts

- Highest direct-link requirement among these five basic topologies: Full mesh.
    
- Full mesh links for n nodes: n(n − 1) / 2.
    
- Every node's degree in a full mesh: n − 1.
    
- A mesh provides alternative paths if the required alternate connections remain operational.
    

**Memory trick:** Mesh = many interconnections and alternative paths.

## 6. Tree Topology

A tree topology connects nodes hierarchically, using parent-child relationships. It often combines multiple star-shaped groups connected through higher-level devices or a backbone.

### How It Works

Communication between devices may pass through one or more higher-level devices. The network can be organized into branches, departments, floors, or buildings.

Example: An organization may have a core switch connected to separate switches for different floors, with computers connected below those switches.

### Advantages

- Easy to expand by adding another branch.
    
- Supports hierarchical administration and segmentation.
    
- Can accommodate networks spanning several departments or buildings.
    
- Faults in one branch may remain limited to that branch if the rest of the structure remains operational.
    

### Disadvantages

- Failure of a critical root or upper-level device can affect many downstream branches.
    
- More cabling and devices may be needed than in a simple bus.
    
- Troubleshooting may require tracing faults through multiple levels.
    
- Performance depends partly on the capacity of higher-level devices and links.
    

### Important Exam Facts

- Structure: Hierarchical.
    
- Typical shape: Root, branches, and leaf nodes.
    
- A tree topology can be viewed as a hierarchical arrangement of star networks.
    
- Failure of a critical upper-level component may affect a large portion of the network.
    

**Memory trick:** Tree = hierarchy with branches.

## 7. Topology Comparison — All Five at a Glance

|Feature|Bus|Star|Ring|Mesh|Tree|
|---|---|---|---|---|---|
|Basic structure|Common backbone|Central device|Closed loop|Multiple interconnected paths|Hierarchical branches|
|Central device required by basic structure?|No|Yes|No|No|Usually hierarchical devices|
|Main cable arrangement|Shared main cable|Separate links to centre|Neighbour-to-neighbour links|Links between nodes|Parent-child connections|
|Typical fault concern|Backbone break|Central device failure|Broken ring link|Loss of redundant paths|Root or upper-level failure|
|Relative cabling in a simple design|Low|Moderate|Moderate|Very high in full mesh|Moderate to high|
|Ease of expansion|Can be inconvenient|Generally easy|May require reconfiguration|Expensive in full mesh|Generally easy by adding branches|
|Key identifying term|Backbone|Central switch/hub|Closed loop|Multiple direct links|Hierarchy|

Cabling and reliability comparisons depend on the actual implementation. For example, a partial mesh requires fewer links than a full mesh, and a protected ring can tolerate failures that break an unprotected ring.

## 8. Common DSSSB Exam Traps

1. **Central device → Star topology.** A hub or switch failure can disrupt devices connected through that centre.
    
2. **Common backbone and terminators → Bus topology.** This is the classic shared coaxial bus arrangement.
    
3. **Token passing → Traditionally associated with Ring topology.** Do not assume every ring network uses a token.
    
4. **Maximum number of direct links → Full mesh topology.** For n nodes, use n(n − 1) / 2.
    
5. **Root and branches → Tree topology.** A critical root or upper-level link can affect many branches.
    
6. **Physical topology is not necessarily logical topology.** Physical star wiring does not automatically imply every packet is broadcast to every device; a switch normally forwards frames selectively.
    

## 9. Final Revision

- **Bus:** Common backbone.
    
- **Star:** Central hub or switch.
    
- **Ring:** Closed loop.
    
- **Mesh:** Multiple interconnections; full mesh requires n(n − 1) / 2 links.
    
- **Tree:** Hierarchical branches.
    

### What to Study Next

Study transmission media (guided and unguided), simplex/half-duplex/full-duplex transmission modes, and switching techniques. These complement network topology in Computer Networks.