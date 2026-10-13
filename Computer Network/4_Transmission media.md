## 1. What is transmission media?

Transmission media is the physical path or wireless channel through which data signals travel from a sender to a receiver.

For example, when you connect a computer to a router, data may travel through an Ethernet cable or through Wi-Fi radio waves.

Transmission media is classified into two main categories:

## 1. Guided (Wired) Media

Signals follow a physical path or cable.

Twisted Pair

Coaxial

Fibre Optic

## 2. Unguided (Wireless) Media

Signals travel through air, space or another propagation medium without a guiding cable.

Radio Waves

Microwaves

Infrared

Memory trick: Guided media = physical cables; unguided media = wireless transmission through electromagnetic waves.

# Part A — Guided transmission media

## 2. Twisted-pair cable

A twisted-pair cable consists of two insulated copper wires twisted around each other. Twisting helps reduce electromagnetic interference and crosstalk between pairs.

It is one of the most common media for Ethernet LANs and telephone wiring.

### Basic structure

Illustration of a twisted pair; actual cables may contain four pairs or more.

### Types of twisted-pair cable

A. UTP — Unshielded Twisted Pair

- Does not have additional metallic shielding around the pairs.
    
- Usually less expensive, flexible and easy to install.
    
- Commonly used in office Ethernet networks and home networks.
    
- More exposed to external electromagnetic interference than a suitably shielded cable.
    

B. STP — Shielded Twisted Pair

- Includes metallic shielding around pairs, the cable or both, depending on its design.
    
- Provides additional protection against external interference.
    
- Generally more expensive and may require proper shield grounding and compatible connectors.
    

### Advantages

- Relatively inexpensive.
    
- Easy to install and maintain.
    
- Widely available for LAN connections.
    
- Twisting helps reduce noise and crosstalk.
    

### Disadvantages

- Copper cable is susceptible to interference to a degree that depends on construction and environment.
    
- Performance is affected by cable category, link length and installation quality.
    
- Copper Ethernet links generally cover shorter distances than long-haul fibre links without repeaters or other active equipment.
    

### Applications

- Ethernet LANs.
    
- Telephone lines.
    
- Connections from a switch to computers and other network devices.
    

Exam traps:

- UTP stands for Unshielded Twisted Pair.
    
- STP stands for Shielded Twisted Pair.
    
- The twisting is primarily intended to reduce interference and crosstalk.
    
- Twisted-pair cables use copper conductors and carry electrical signals.
    

## 3. Coaxial cable

A coaxial cable contains a central conductor surrounded by an insulating dielectric, a conductive shield and an outer protective jacket. The inner conductor and the outer conductive shield share a common axis, which gives the cable its name.

### Layers of a coaxial cable

Outer protective jacket

Conductive shield

Dielectric insulator

Central copper conductor

Simplified cross-section. The metallic shield can also serve as the return conductor.

### How it works

Electrical signals travel along the central conductor, with the surrounding conductive shield helping contain the electromagnetic field and reduce external interference.

### Advantages

- Better shielding against external interference than many unshielded copper arrangements.
    
- Can support relatively high-frequency signals.
    
- Has been widely used for cable television and broadband access.
    
- More robust against certain noise sources than unshielded twisted pair, depending on cable construction.
    

### Disadvantages

- Bulkier and less flexible than many twisted-pair cables.
    
- Can be more expensive or cumbersome to install than ordinary UTP.
    
- Requires suitable connectors and installation practices.
    

### Applications

- Cable television.
    
- Cable broadband Internet access.
    
- CCTV and RF signal systems.
    
- Older Ethernet implementations, such as 10BASE2 and 10BASE5.
    

Exam traps:

- Twisted-pair cable has twisted copper conductors; coaxial cable has a central conductor with surrounding insulation and shielding.
    
- Coaxial cable is not an optical cable.
    
- Both twisted pair and coaxial cable use electrical signals in their copper conductors.
    

## 4. Fibre-optic cable

A fibre-optic cable transmits information using light through thin strands of glass or plastic.

It consists primarily of a core, cladding and protective coating or jacket.

### Basic fibre-optic structure

Protective jacket and layers

Cladding

Core

The core carries the light; the cladding helps confine it through differences in refractive index.

### How does fibre-optic transmission work?

Light is guided through the core by the optical properties of the core and cladding. In the standard introductory explanation, this is described using total internal reflection.

Information is encoded into optical signals, and a receiver converts those signals back into data.

### Types of optical fibre

|Feature|Single-mode fibre|Multimode fibre|
|---|---|---|
|Core size|Smaller|Larger|
|Light propagation|One principal mode|Multiple modes|
|Typical use|Long-distance links and telecommunications|Shorter-distance links, such as many building or data-centre links|
|Modal dispersion|Very low|Generally greater|
|Common light sources|Lasers|LEDs or lasers, depending on the system|

### Advantages

- Supports very high data rates and high bandwidth.
    
- Suitable for long-distance communication.
    
- Immune to electromagnetic interference.
    
- Provides electrical isolation between endpoints.
    
- Difficult to tap without potentially introducing detectable changes, though fibre is not automatically secure.
    

### Disadvantages

- Optical equipment and installation can cost more than basic copper alternatives.
    
- Fibres need careful handling and suitable connectors or splicing.
    
- Repair and testing may require specialized tools.
    
- Fibre does not directly carry ordinary electrical signals in the way copper conductors do.
    

### Applications

- Internet backbone and undersea communication links.
    
- Telecommunications networks.
    
- Fibre-to-the-home (FTTH).
    
- Data centres and high-speed building interconnections.
    

Exam traps:

- Fibre optics use light, not electrical current in the fibre core.
    
- Fibre is highly resistant to electromagnetic interference.
    
- Optical communication is not limited to short distances: single-mode fibre is commonly used over long distances.
    
- Fibre carries signals in the core, while the cladding helps guide the light.
    

# Part B — Unguided transmission media

Unguided media transmits electromagnetic signals without guiding them through a cable. The three syllabus topics below are radio waves, microwaves and infrared.

## 5. Radio waves

Radio-wave transmission sends information wirelessly using radio-frequency electromagnetic waves.

Radio systems can transmit over different distances and in different directions, depending on frequency, antenna design, power, environment and propagation conditions.

### Characteristics

- Can support communication without a physical cable.
    
- Many radio systems can operate without a direct visual line of sight.
    
- Signals may diffract around obstacles or penetrate some materials, depending on frequency and construction.
    
- Can be affected by interference from other transmitters and electrical equipment.
    
- May support broadcast or point-to-point communication.
    

### Applications

- Radio broadcasting.
    
- Wi-Fi and Bluetooth, which use radio frequencies.
    
- Mobile communication.
    
- Wireless local-area and wide-area networks.
    

Exam trap: Wi-Fi is radio-based wireless communication. It does not use infrared merely because it works without a cable.

## 6. Microwaves

Microwave transmission uses electromagnetic waves in the microwave frequency region. Many terrestrial microwave communication links use directional antennas and a relatively clear line of sight between them.

Microwave communication is also used in satellite systems.

### Types

A. Terrestrial microwave

Antennas on towers, rooftops or other elevated locations transmit signals to each other. Relay stations may be used over longer distances.

B. Satellite microwave

An Earth station transmits toward a satellite, which relays the signal to another Earth station or coverage region.

### Characteristics

- Often uses directional antennas.
    
- Many terrestrial links need a clear line of sight or a carefully engineered propagation path.
    
- Can support high-capacity point-to-point communication.
    
- Links may be affected by obstacles, weather and frequency, especially in higher-frequency bands.
    
- Satellite paths can introduce significant propagation delay because the signal travels over a very long distance.
    

### Applications

- Point-to-point backhaul links.
    
- Satellite TV and communication.
    
- Some cellular network backhaul.
    
- Radar and other microwave systems.
    

Exam traps:

- Microwave links often use directional antennas.
    
- Terrestrial microwave generally requires a suitable line-of-sight path.
    
- Satellite communication commonly uses microwave frequencies.
    
- A microwave link is not automatically faster than fibre; performance depends on the technology and system design.
    

## 7. Infrared (IR)

Infrared transmission uses electromagnetic radiation in the infrared region to communicate over relatively short distances in many common networking applications.

Infrared is used in devices such as remote controls and some short-range data links.

### Characteristics

- Commonly used for short-range communication.
    
- Many IR systems require a direct line of sight or a suitable reflected optical path.
    
- Ordinary infrared remote-control signals generally do not pass through walls.
    
- It does not use radio-frequency transmission in the way Wi-Fi and Bluetooth do.
    
- It can be affected by obstacles, ambient infrared sources and receiver orientation.
    

### Applications

- Television and appliance remote controls.
    
- Short-range device communication.
    
- Infrared sensors and optical communication systems.
    

### Advantages

- Useful for short-range links.
    
- Can limit communication to a room or a specific direction.
    
- Does not create the same radio-frequency interference profile as RF communication.
    

### Disadvantages

- Common implementations are limited by range and obstacles.
    
- Many systems require favourable alignment or line of sight.
    
- Strong ambient light or other infrared sources can interfere with reception in some implementations.
    

Exam traps:

- Infrared is an electromagnetic wave, not a sound wave.
    
- Ordinary infrared remote-control signals generally do not pass through walls.
    
- Wi-Fi uses radio frequencies, not infrared.
    
- Not every infrared system requires a perfectly direct beam; some use diffuse or reflected paths.
    

## 8. Radio vs microwave vs infrared

|Feature|Radio waves|Microwaves|Infrared|
|---|---|---|---|
|Medium|Wireless electromagnetic waves|Wireless electromagnetic waves|Wireless electromagnetic radiation|
|Typical networking examples|Wi-Fi, Bluetooth, mobile communication|Terrestrial backhaul, satellite links|Remote controls, short-range optical links|
|Direction|Can be omnidirectional or directional|Often directional|Often directional or confined to a room in common applications|
|Line of sight|Not always required|Commonly important for terrestrial links|Commonly required by direct-beam systems|
|Wall penetration|Possible at some frequencies, depending on materials|Often limited and frequency-dependent|Ordinary IR remote signals generally do not pass through walls|
|Common constraints|Interference, congestion, obstacles|Alignment, obstacles, weather at some frequencies|Obstacles, alignment, ambient IR|
|Main distinction|Broad class of radio communication|Higher-frequency radio region, often directional links|Infrared region of the electromagnetic spectrum|

Important: These are broad introductory comparisons. Exact propagation and coverage depend on the frequency band, antennas, power, materials and system design.

## 9. Comparison of all six transmission media

|Feature|Twisted pair|Coaxial|Fibre optic|Radio|Microwave|Infrared|
|---|---|---|---|---|---|---|
|Category|Guided|Guided|Guided|Unguided|Unguided|Unguided|
|Signal carried|Electrical|Electrical|Light|Radio waves|Microwave electromagnetic waves|Infrared radiation|
|Physical cable|Yes|Yes|Yes|No|No|No|
|Resistance to EMI|Depends on type; twisting reduces interference|Good shielding in a suitable cable|Immune to electromagnetic interference in the fibre|Susceptible to RF interference|Can face interference and propagation effects|Not subject to RF interference in the same way|
|Common application|Ethernet, telephone wiring|Cable TV, broadband|Backbone, FTTH, long-distance links|Wi-Fi, mobile, broadcasting|Satellite and point-to-point links|Remote controls|
|Key exam clue|Twisted copper pairs|Central conductor and shield|Light in a core|Wireless radio communication|Directional links / satellite|Short-range, commonly blocked by walls|

No single medium is always the best: the choice depends on required capacity, distance, installation cost, interference, mobility and reliability.

## 10. Which medium should you choose?

|Requirement|Commonly suitable medium|Reason|
|---|---|---|
|Affordable wired office LAN|Twisted pair|Cost-effective and easy to install|
|Cable-TV signal distribution|Coaxial cable|Suitable shielding and RF signal transmission|
|Very high capacity over long distances|Fibre optic|High bandwidth and low signal loss over suitable links|
|Wireless access for phones and laptops|Radio waves|Supports wireless networking and mobility|
|Directional link between distant towers|Terrestrial microwave|Suitable for engineered point-to-point links|
|TV remote control|Infrared|Common short-range control technology|

## 11. High-yield exam facts

Memorize these before attempting the MCQs:

- UTP: Unshielded Twisted Pair.
    
- STP: Shielded Twisted Pair.
    
- Twisted pair: Twisting reduces interference and crosstalk.
    
- Coaxial: Central conductor, dielectric, conductive shield and jacket.
    
- Fibre optic: Light travels through a core; cladding helps confine the light.
    
- Single-mode fibre: Commonly used for long-distance optical links.
    
- Multimode fibre: Commonly used for shorter links.
    
- Radio waves: Used by Wi-Fi, Bluetooth and mobile networks.
    
- Microwaves: Commonly used for directional terrestrial links and satellite communication.
    
- Infrared: Used by many remote controls; ordinary IR remote signals generally cannot pass through walls.
    
- Guided media: Twisted pair, coaxial and fibre optic.
    
- Unguided media: Radio waves, microwaves and infrared.