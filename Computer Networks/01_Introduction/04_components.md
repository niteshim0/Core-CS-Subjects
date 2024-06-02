# Computer Network Components

Computer network components are the major parts needed to install the software. Some important network components are NIC, switch, cable, hub, router, and modem. Depending on the type of network being installed, some components may not be required (e.g., a wireless network does not need cables).

## Major Components Required to Install a Network

### NIC (Network Interface Card)
- **Definition**: A hardware component used to connect a computer to a network.
- **Transfer Rate**: Supports 10, 100, to 1000 Mb/s.
- **MAC Address**: Encoded on the NIC chip to uniquely identify a network card, stored in PROM.

#### Types of NIC:
- **Wired NIC**: 
  - Integrated into the motherboard.
  - Uses cables and connectors to transfer data.
- **Wireless NIC**: 
  - Contains an antenna for wireless connection.
  - Common in laptops.

### Hub
- **Function**: Divides network connection among multiple devices.
- **Operation**: Broadcasts requests to the entire network.
- **Limitation**: Consumes more bandwidth and limits communication.
- **Current Use**: Mostly obsolete, replaced by switches and routers.

### Switch
- **Function**: Connects multiple devices on a network.
- **Operation**: Uses an updated table to direct messages to the correct destination based on physical address.
- **Advantage**: Provides a direct connection between source and destination, increasing network speed.

### Router
- **Function**: Connects LAN to an internet connection, forwards incoming packets to another network.
- **Operation**: Works at Layer 3 (Network layer) of the OSI model, determines the best path for packet transmission.
- **Advantages**:
  - **Security**: Only addressed devices can read transmitted data.
  - **Reliability**: Network issues in one part do not affect other networks served by the router.
  - **Performance**: Enhances network performance by splitting traffic loads.

### Modem
- **Definition**: A device that allows computers to connect to the internet over telephone lines.
- **Integration**: Installed on the PCI slot of the motherboard, not integrated.
- **Function**: Converts digital data into an analog signal.
- **Types**:
  - **Standard PC Modem (Dial-up Modem)**
  - **Cellular Modem**
  - **Cable Modem**

### Cables and Connectors
- **Function**: Transmission media for signals.

#### Types of Cables:
- **Twisted Pair Cable**: High-speed, transmits data over 1Gbps or more.
- **Coaxial Cable**: Resembles TV installation cable, provides high data transmission speed.
- **Fibre-Optic Cable**: Uses light beams for data transmission, offers the highest speed, and is expensive.

### Additional Components
- **Access Points**: 
  - **Function**: Connect wireless devices to a wired network, extending the network's reach.
  - **Types**: 
    - **Standalone**: Operate independently.
    - **Controller-based**: Managed by a network controller for large-scale environments.
- **Firewalls**: 
  - **Function**: Provide security by controlling incoming and outgoing network traffic based on predetermined security rules.
  - **Types**:
    - **Hardware Firewalls**: Dedicated devices.
    - **Software Firewalls**: Installed on individual computers.
- **Repeaters**: 
  - **Function**: Amplify and extend the range of signals in a network.
  - **Usage**: Useful in long-distance or large area networks to maintain signal strength.
- **Bridges**: 
  - **Function**: Connects two or more network segments, making them function as a single network.
  - **Operation**: Filters traffic, reduces collisions, and improves performance.
- **Gateways**: 
  - **Function**: Acts as a bridge between different networking protocols or formats.
  - **Usage**: Essential for connecting different network architectures, like connecting a local network to the internet.
- **Network Interface Devices (NID)**: 
  - **Function**: Acts as the demarcation point between the customer's inside wiring and the external wiring of the telecom service provider.
- **Patch Panels**: 
  - **Function**: A mounted hardware assembly containing ports to manage and connect incoming and outgoing network cables.
- **Power over Ethernet (PoE) Devices**: 
  - **Function**: Allows network cables to carry electrical power.
  - **Usage**: Commonly used for devices like IP cameras, VoIP phones, and wireless access points.

