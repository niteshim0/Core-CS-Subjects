# OSI Model

The OSI (Open System Interconnection) model is a reference model developed by the International Organization for Standardization (ISO) in 1984. It describes how information from a software application in one computer moves through a physical medium to a software application in another computer.

## Characteristics of OSI Model

- **Layered Architecture:** Divides tasks into seven layers, each performing a specific network function.
- **Independence:** Each layer is self-contained, allowing independent task execution.

## Layers of OSI Model

The OSI model is divided into two sets of layers: upper layers and lower layers.

### Upper Layers

- **Function:** Deal with application-related issues.
- **Implementation:** Only in software.
- **Layers:**
  1. **Application Layer:** Closest to the end user; interacts with software applications.
  2. **Presentation Layer:** Translates data formats between applications and the network.
  3. **Session Layer:** Manages and controls the connections between computers.

### Lower Layers

- **Function:** Deal with data transport issues.
- **Implementation:** In hardware and software.
- **Layers:**
  4. **Transport Layer:** Ensures error-free data delivery between hosts.
  5. **Network Layer:** Determines the best physical path for data.
  6. **Data-Link Layer:** Handles error detection and correction from the physical layer.
  7. **Physical Layer:** Closest to the physical medium; responsible for placing information on the physical medium.


![Characteristics of OSI Model](https://static.javatpoint.com/tutorial/computer-network/images/osi-model.png)


## 7 Layers of OSI Model

![Layers of OSI Model](https://static.javatpoint.com/tutorial/computer-network/images/osi-model2.png)

# Physical Layer (OSI Model)

The Physical Layer is the lowest layer of the OSI model. Its main function is to transmit individual bits from one node to another.

## Key Functions

1. **Transmission of Bits:**
   - Transmits individual bits over a physical medium.

2. **Physical Connection:**
   - Establishes, maintains, and deactivates the physical connection.

3. **Specifications:**
   - Defines mechanical, electrical, and procedural network interface specifications.

## Detailed Functions

1. **Line Configuration:**
   - Defines how two or more devices are physically connected.

2. **Data Transmission:**
   - Specifies the transmission mode:
     - **Simplex:** One-way communication.
     - **Half-Duplex:** Two-way communication, but not simultaneously.
     - **Full-Duplex:** Two-way communication simultaneously.

3. **Topology:**
   - Defines the arrangement of network devices (e.g., star, bus, ring, mesh).

4. **Signals:**
   - Determines the type of signals used for transmitting information (e.g., electrical, optical).




