# Network Protocols

## Layers of Protocol
![Network Layer](https://static.javatpoint.com/tutorial/computer-network/images/osi-model.png)
### Application Layer Protocol

#### Client-Server Protocols

1. **HTTP (HyperText Transfer Protocol)**
   - **Use Cases:** Used for transferring web pages on the internet. It enables web browsers to fetch and display content from web servers.
   - **How It Works:** HTTP operates over TCP. A client (browser) sends an HTTP request to a server, which processes the request and returns the appropriate HTTP response (e.g., an HTML page).
   - **Data Transfer:** Data is transferred as packets using TCP, ensuring reliable delivery.
   - **Connection Type:** Typically, HTTP uses a single connection per request/response cycle, though HTTP/2 can reuse connections.
   - **Acknowledgement:** TCP handles acknowledgements of data receipt.

2. **HTTPS (HyperText Transfer Protocol Secure)**
   - **Use Cases:** Secured version of HTTP, used for secure communication over a computer network within a browser.
   - **How It Works:** HTTPS uses SSL/TLS to encrypt data between client and server, ensuring confidentiality and integrity.
   - **Data Transfer:** Similar to HTTP, data is transferred as packets over TCP with encryption.
   - **Connection Type:** Uses secure, encrypted connections.

3. **FTP (File Transfer Protocol)**
   - **Use Cases:** Used for transferring files between a client and a server.
   - **How It Works:** FTP operates on two channels: command (control) and data. The control connection manages session parameters, while the data connection transfers files.
   - **Data Transfer:** Data is transferred as packets over TCP.
   - **Connection Type:** Requires multiple connections (one for control and one for each data transfer).

4. **SMTP (Simple Mail Transfer Protocol)**
   - **Use Cases:** Used for sending emails.
   - **How It Works:** SMTP transfers email from a client to an email server or between email servers.
   - **Data Transfer:** Data is transferred as packets over TCP.
   - **Connection Type:** Typically a single connection for sending an email.
   - **Acknowledgement:** Uses TCP acknowledgements.

5. **POP3 (Post Office Protocol version 3)**
   - **Use Cases:** Used for retrieving emails from a server to a client.
   - **How It Works:** POP3 downloads emails from the server to the client and often deletes them from the server.
   - **Data Transfer:** Data is transferred as packets over TCP.
   - **Connection Type:** Single connection for session.
   - **Acknowledgement:** Uses TCP acknowledgements.

6. **IMAP (Internet Message Access Protocol)**
   - **Use Cases:** Used for managing and retrieving emails from a server.
   - **How It Works:** Unlike POP3, IMAP allows multiple devices to access the same mailbox.
   - **Data Transfer:** Data is transferred as packets over TCP.
   - **Connection Type:** Maintains a persistent connection to synchronize email state.
   - **Acknowledgement:** Uses TCP acknowledgements.

7. **WebSockets**
   - **Use Cases:** Used for real-time communication between client and server.
   - **How It Works:** WebSockets establish a persistent, full-duplex connection over a single TCP connection.
   - **Data Transfer:** Data is transferred as packets over TCP.
   - **Connection Type:** Persistent connection.
   - **Acknowledgement:** Uses TCP acknowledgements.

#### Peer-to-Peer Protocols

1. **BitTorrent**
   - **Use Cases:** Used for distributing large amounts of data across a decentralized network.
   - **How It Works:** Files are split into pieces and distributed among peers. Peers download pieces from each other simultaneously.
   - **Data Transfer:** Data is transferred in chunks over TCP or UDP.
   - **Connection Type:** Multiple simultaneous connections to various peers.
   - **Acknowledgement:** Uses TCP acknowledgements if TCP is used; otherwise, it relies on the protocol’s own mechanisms.

2. **WebRTC (Web Real-Time Communication)**
   - **Use Cases:** Used for real-time audio, video, and data communication in web applications.
   - **How It Works:** Establishes peer-to-peer connections using signaling servers to negotiate connections and then directly exchanges media and data streams.
   - **Data Transfer:** Data can be transferred over UDP for lower latency, or TCP for reliability.
   - **Connection Type:** Peer-to-peer connections.
   - **Acknowledgement:** Typically uses UDP, so acknowledgements are handled at the application level.

### Transport Layer Protocols

The Transport Layer is responsible for end-to-end communication and error recovery. It ensures complete data transfer and can provide error checking and flow control.

1. **TCP/IP (Transmission Control Protocol/Internet Protocol)**
   - **Use Cases:** Used for reliable, ordered, and error-checked delivery of data between applications.
   - **How It Works:** TCP establishes a connection through a three-way handshake, ensures data is delivered in order, and retransmits lost packets.
   - **Data Transfer:** Data is transferred in packets.
   - **Connection Type:** Connection-oriented.
   - **Acknowledgement:** Acknowledgements are sent for received data, ensuring reliable transfer.

2. **UDP/IC (User Datagram Protocol/Internet Control)**
   - **Use Cases:** Used for applications where speed is critical and error correction can be handled by the application (e.g., streaming, gaming).
   - **How It Works:** UDP sends datagrams without establishing a connection, making it faster but less reliable.
   - **Data Transfer:** Data is transferred in datagrams.
   - **Connection Type:** Connectionless.
   - **Acknowledgement:** No built-in acknowledgements; applications handle error-checking if needed.

3. **SCTP (Stream Control Transmission Protocol)**
   - **Use Cases:** Used for telephony over IP, signaling, and other real-time applications requiring multiple streams.
   - **How It Works:** Combines features of TCP and UDP, supporting multi-homing and multi-streaming.
   - **Data Transfer:** Data is transferred in chunks, similar to packets.
   - **Connection Type:** Connection-oriented.
   - **Acknowledgement:** Provides acknowledgements for reliable delivery and can also support unordered delivery.

### Summary of Data Transfer

- **Packets vs. Datagrams:** 
  - Packets: Used in TCP, ensure ordered and reliable delivery.
  - Datagrams: Used in UDP, may be delivered out of order or lost, with no guarantees.
- **Connections:**
  - Connection-oriented (e.g., TCP, SCTP) ensures reliability and order.
  - Connectionless (e.g., UDP) prioritizes speed over reliability.
- **Acknowledgements:**
  - Integral to TCP, ensuring reliable delivery.
  - Not present in UDP, relying on application-level handling.
  - SCTP provides both reliable and unreliable service options.

