| Feature / Aspect       | **TCP (Transmission Control Protocol)**                          | **UDP (User Datagram Protocol)**                       |
|------------------------|------------------------------------------------------------------|--------------------------------------------------------|
| **Goal**               | Reliable communication between two devices                      | Send data fast, even if some is lost                   |
| **Reliability**        | Guarantees delivery and correct order of data                    | No guarantee of delivery or order                      |
| **Error Handling**     | Resends lost packets automatically                               | No automatic retransmission                            |
| **Connection Setup**   | Requires a three-way handshake before sending data               | Connectionless – sends without handshake               |
| **Speed**              | Slower due to error checking and acknowledgments                 | Faster and lighter, minimal overhead                   |
| **Best For**           | Web browsing (HTTP/HTTPS), Email, File transfers, anything where missing data breaks things | Live streaming, Online gaming, DNS lookups, speed-priority tasks |


# TCP vs UDP – How They Work Inside Packets

## 1. How TCP and UDP Fit into the Network Stack
When you send data over the internet:

1. **Application Layer** → Your app generates data (e.g., an HTTP request, game data, video frame).
2. **Transport Layer** → TCP or UDP wraps that data in a **transport segment** (adds headers with control info).
3. **Network Layer** → IP wraps the segment into a **packet** (adds source/destination IP addresses).
4. **Data Link Layer** → Ethernet/Wi-Fi frames wrap the packet to send it physically.

TCP and UDP are **transport protocols** — they sit above IP.

---

## 2. TCP Packet (Segment) Structure

A TCP segment has **two parts**:
- **Header** (control info)
- **Data** (payload from your application)

**TCP Header Fields (simplified):**

| Field                 | Purpose |
|-----------------------|---------|
| **Source Port**       | Port number of sender app |
| **Destination Port**  | Port number of receiver app |
| **Sequence Number**   | Position of the first byte in this segment (for ordering) |
| **Acknowledgment Number** | Next byte expected from the other side |
| **Flags**             | Control bits (SYN, ACK, FIN, etc.) |
| **Window Size**       | How much data can be sent before needing an ACK |
| **Checksum**          | Detects errors in header + data |
| **Data**              | Application data (HTTP body, file chunk, etc.) |


## 3. UDP Packet (Datagram) Structure

A UDP datagram is simpler:

| Field                 | Purpose |
|-----------------------|---------|
| **Source Port**       | Port number of sender app |
| **Destination Port**  | Port number of receiver app |
| **Length**            | Total size of datagram (header + data) |
| **Checksum**          | Detects errors (optional in IPv4, mandatory in IPv6) |
| **Data**              | Application data (DNS query, game movement data, video chunk) |


## 4. Key Differences Inside the Packet

| Feature        | TCP                                      | UDP                                  |
|----------------|------------------------------------------|--------------------------------------|
| Header size    | 20–60 bytes                              | 8 bytes                              |
| Reliability    | Sequence numbers + ACKs ensure delivery  | No delivery guarantee                |
| Order tracking | Yes                                      | No                                   |
| Overhead       | Higher                                   | Lower                                |
| Payload size   | Slightly less than UDP (due to bigger header) | More usable space for small packets |
