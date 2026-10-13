## 1. What is network topology?

Network topology is the arrangement of devices (nodes) and communication links in a computer network.

- Node: A device connected to a network, such as a computer, printer or router.
    
- Link: A communication connection between devices.
    
- Physical topology: The physical arrangement of cables, devices and connections.
    
- Logical topology: How data flows between devices, regardless of the physical arrangement.
    

For example, devices may be physically connected to a central switch in a star, while the data follows different logical paths depending on the network technology.

The five topologies in your syllabus are Bus, Star, Ring, Mesh and Tree.

## 2. Bus topology

A bus topology connects multiple devices to a common communication cable called the backbone.

### Bus Topology

Terminator

PC 1

PC 2

PC 3

PC 4

│　　 │　　 │　　 │

════════════════

Common backbone cable

Terminator at the opposite end (not drawn to scale)

### How it works

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
    

### Important exam facts

- Main component: Common backbone cable.
    
- Traditional bus Ethernet uses: Terminators at both ends.
    
- Failure of a single device's branch connection may affect that device, while a backbone break can affect the entire bus.
    
- Traditional shared-bus Ethernet is associated with collisions.
    

Memory trick: Bus = one common backbone.

## 3. Star topology

A star topology connects every device to a central device, usually a switch or hub.

### Star Topology

Central Switch

PC 1

PC 2

PC 3

PC 4

### How it works

Every device has a separate connection to the central hub or switch.

- With a hub, incoming signals are repeated to all other ports.
    
- With a switch, frames are usually forwarded to the appropriate port based on the destination MAC address, when the switch has learned the destination.
    

Modern wired Ethernet LANs commonly use a physical star or extended-star arrangement.

### Advantages

- Easy to install, manage and expand.
    
- Failure of one device's cable generally affects only that device.
    
- Faults are comparatively easy to isolate.
    
- With a switch, devices can communicate efficiently without sharing one collision domain as they would on a traditional hub-based Ethernet segment.
    

### Disadvantages

- Failure of the central switch or hub can disrupt all devices connected through it.
    
- Requires more cabling than a simple bus.
    
- The central device adds cost.
    
- The central device's capacity can become a performance bottleneck.
    

### Important exam facts

|Failure|Typical effect|
|---|---|
|One computer fails|Other devices can continue communicating|
|One computer's link fails|That computer generally loses its network connection|
|Central switch fails|The connected star network is disrupted|
|Central hub fails|The connected star network is disrupted|

Memory trick: Star = all devices connect to a centre.

## 4. Ring topology

A ring topology connects each device to its neighbouring device, forming a closed loop.

### Ring Topology

PC 1

PC 2

PC 4

PC 3

Each node connects to its neighbours to form a closed loop.

### How it works

Data travels from one node to the next around the ring. Depending on the technology, a ring network may use a particular access-control mechanism, such as token passing.

In a token-passing arrangement, a special control frame called a token circulates. A device transmits when it obtains permission through the token mechanism.

Not every ring topology necessarily uses token passing.

### Advantages

- Data transmission can be orderly in token-controlled systems.
    
- Access to the medium can be predictable under suitable operating conditions.
    
- Each node can regenerate or forward data in some ring implementations.
    
- Does not inherently require a central hub for a simple ring.
    

### Disadvantages

- In a basic single ring, one broken link or failed node may interrupt the entire ring.
    
- Adding or removing devices can disrupt a basic ring during reconfiguration.
    
- A fault can be harder to locate than in a simple star.
    
- Delay may increase as data passes through more intermediate nodes.
    

### Important exam facts

- Shape: Closed loop or circle.
    
- In traditional token ring systems: Token passing controls access.
    
- In a basic single ring: A link failure can break the communication path.
    
- Dual-ring designs and other protection mechanisms can provide resilience, so not all ring networks fail completely after one link break.
    

Memory trick: Ring = each node connects to its neighbours in a loop.

## 5. Mesh topology

A mesh topology connects devices through multiple links, giving the network alternative paths for communication. In a full mesh, every node has a direct link to every other node.

There are two main types.

### A. Full mesh

Every node is directly connected to every other node.

### Full Mesh — Four Nodes

Every pair of nodes has a direct connection. The six links are shown for four nodes.

### B. Partial mesh

Only some pairs of nodes have direct connections. Multiple paths may still exist between important nodes, depending on the design.

### Number of links in a full mesh

For \(n\) nodes, the number of direct links required is:

\[ \boxed{L=\frac{n(n-1)}{2}} \]

Why? Each of the \(n\) nodes can connect to \(n-1\) other nodes, but counting \(n(n-1)\) counts every link twice. Therefore, divide by 2.

Example: How many links are needed to fully mesh 5 nodes?

\[ L=\frac{5(5-1)}{2} =\frac{20}{2}=\boxed{10} \]

For a full mesh, each node has \(n-1\) direct links. Thus, with 5 nodes, every node has 4 links.

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
    

### Important exam facts

- Highest direct-link requirement among these five basic topologies: full mesh.
    
- Full mesh links for \(n\) nodes: \(n(n-1)/2\).
    
- Every node's degree in a full mesh: \(n-1\).
    
- A mesh provides alternative paths if the required alternate connections remain operational.
    

Memory trick: Mesh = many interconnections and alternative paths.

## 6. Tree topology

A tree topology connects nodes hierarchically, using parent-child relationships. It often combines multiple star-shaped groups connected through higher-level devices or a backbone.

### Tree Topology

Root Switch

Switch A

PC 1

PC 2

Switch B

PC 3

PC 4

Higher-level devices connect to lower-level branches, creating a hierarchy.

### How it works

Communication between devices may pass through one or more higher-level devices. The network can be organized into branches, departments, floors or buildings.

For example, an organization may have a core switch connected to separate switches for different floors, with computers connected below those switches.

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
    

### Important exam facts

- Structure: Hierarchical.
    
- Typical shape: Root, branches and leaf nodes.
    
- A tree topology can be viewed as a hierarchical arrangement of star networks.
    
- Failure of a critical upper-level component may affect a large portion of the network.
    

Memory trick: Tree = hierarchy with branches.

## 7. Topology comparison — all five at a glance

|Feature|Bus|Star|Ring|Mesh|Tree|
|---|---|---|---|---|---|
|Basic structure|Common backbone|Central device|Closed loop|Multiple interconnected paths|Hierarchical branches|
|Central device required by the basic structure?|No|Yes|No|No|Usually uses hierarchical devices|
|Main cable arrangement|Shared main cable|Separate links to centre|Neighbour-to-neighbour links|Links between nodes|Parent-child connections|
|Typical fault concern|Backbone break|Central device failure|Broken ring link|Loss of redundant paths|Root or upper-level failure|
|Relative cabling in a simple design|Low|Moderate|Moderate|Very high in full mesh|Moderate to high|
|Ease of expansion|Can be inconvenient|Generally easy|May require reconfiguration|Expensive in full mesh|Generally easy by adding branches|
|Key identifying term|Backbone|Central switch/hub|Closed loop|Multiple direct links|Hierarchy|

Cabling and reliability comparisons depend on the actual implementation. For example, a partial mesh can require far fewer links than a full mesh, and a protected ring can tolerate failures that break an unprotected ring.

## 8. Common DSSSB exam traps

1. Central device → Star topology. A hub or switch failure can disrupt devices connected through that centre.
    
2. Common backbone and terminators → Bus topology. This is the classic shared coaxial bus arrangement.
    
3. Token passing → Traditionally associated with Ring topology. Do not assume every ring network uses a token.
    
4. Maximum number of direct links → Full mesh topology. For \(n\) nodes, use \(n(n-1)/2\).
    
5. Root and branches → Tree topology. A critical root or upper-level link can affect many branches.
    
6. Physical topology is not necessarily logical topology. Physical star wiring does not automatically imply every packet is broadcast to every device; a switch normally forwards frames selectively.
### Final revision

- Bus: Common backbone.
    
- Star: Central hub or switch.
    
- Ring: Closed loop.
    
- Mesh: Multiple interconnections; full mesh requires \(n(n-1)/2\) links.
    
- Tree: Hierarchical branches.
    

Next, study transmission media (guided and unguided), simplex/half-duplex/full-duplex transmission modes, and switching techniques. These complement network topology in Computer Networks.