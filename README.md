# cybersecurity-networking
My beginner notes on networking and cybersecurity
# Cybersecurity & Networking Learning Notes

## Lesson 1: IP Addresses & DNS (The Internet's Phonebook)
* **IP Address:** Every phone, laptop, and cloud server gets a unique number address (like `192.168.1.1`) so internet traffic knows where to deliver messages.
* **DNS (Domain Name System):** A digital phonebook that translates easy website names (like `github.com`) into their secret IP address numbers.

## Lesson 2: Ports & Protocols (Digital Doors & Languages)
* **Ports (Digital Doors):** A single server has thousands of numbered virtual doors (ports) for different jobs—like Port 80 and Port 443 for websites, or Port 22 for remote admin login.
* **HTTP vs. HTTPS (Ports 80 & 443):** HTTP sends website data in plain text that hackers can spy on, while **HTTPS** locks and encrypts the traffic with a padlock.
* **SSH (Port 22):** Secure Shell lets cloud engineers safely log into remote servers over an encrypted tunnel—one of the first doors hackers try to attack if left wide open.

## Lesson 3: VPNs & Packet Sniffing (Secret Tunnels)
* **Packet Sniffing:** Hackers on public Wi-Fi (like at a café or airport) can use tools to "listen in" on unencrypted digital envelopes floating through the air.
* **VPN (Virtual Private Network):** A VPN builds an encrypted, armored tunnel between your device and the internet so snooping hackers on public Wi-Fi only see scrambled gibberish.
## Networking Detective Scorecard
**Status:** Completed | **Score:** 3 / 3 (100%)

| Case | Topic | Key Takeaway | Result |
| :--- | :--- | :--- | :--- |
| **Case 1** | **Web Security** | HTTP vs. HTTPS & Packet Sniffing | Passed |
| **Case 2** | **Remote Access** | Port 22 (SSH) Encrypted Login | Passed |
| **Case 3** | **Addressing** | DNS (The Internet's Phonebook) | Passed |
# TCP Connection Management & Security

## Core TCP Features
- **Connection-Oriented:** Establishes a formal session before sending data and closes it gracefully afterward.
- **Reliable Delivery:** Uses sequence numbers and acknowledgments (`ACK`) to retransmit lost data and reorder scrambled packets.
- **Flow Control:** Uses windowing so the receiver can tell the sender to slow down or speed up.

## 1. Formal Setup: The 3-Way Handshake
1. **`SYN` (Client → Server):** Client initiates a connection and synchronizes sequence numbers.
2. **`SYN-ACK` (Server → Client):** Server acknowledges the request and sends its own sequence number.
3. **`ACK` (Client → Server):** Client confirms receipt; the session is now `ESTABLISHED`.

## 2. Formal Close: The 4-Way Wave
1. **`FIN` (Client → Server):** Client finishes sending data and requests to close its side.
2. **`ACK` (Server → Client):** Server acknowledges the `FIN` (enters `CLOSE_WAIT` while finishing its own data).
3. **`FIN` (Server → Client):** Server finishes sending data and requests to close its side.
4. **`ACK` (Client → Server):** Client confirms closure and enters `TIME_WAIT` (2MSL) before fully closing.

## 3. Cybersecurity Scenarios
- **SYN Flood (DoS):** Attacker floods a server with spoofed `SYN` packets and never sends the final `ACK`, exhausting half-open connection memory.
- **TCP SYN Scan (Reconnaissance):** Scanner sends `SYN` → receives `SYN-ACK` → immediately sends **`RST`** (Reset) instead of `ACK` to detect open ports stealthily.

## Study Scorecard

| Topic | Score | Key Takeaway |
| :--- | :---: | :--- |
| TCP 3-Way Handshake & SYN Floods | 2 / 2 | Incomplete handshakes (`SYN` without `ACK`) indicate potential floods or scans. |
| TCP Teardown & Scan Flags (`RST`, `TIME_WAIT`) | In Progress | `RST` aborts half-open scans; `TIME_WAIT` absorbs delayed packets. |
# TCP Connection Management & Security

## Core TCP Features
- **Connection-Oriented:** Establishes a formal session before sending data and closes it gracefully afterward.
- **Flow Control:** Uses windowing so the receiver can tell the sender to slow down or speed up.

### Reliable Delivery (How TCP Protects Your Data)
TCP acts like a strict delivery tracker that makes sure nothing gets lost, broken, or mixed up:
1. **Number It (Sequence Numbers):** Puts a number on every piece of data (`1, 2, 3`) so the receiving computer can put them back in the right order—even if they arrive late or scrambled.
2. **Confirm It (`ACK` Receipts):** Every time the receiver gets a piece safely, it sends back a quick *"Got it!"* receipt (`ACK`).
3. **Resend It (Retransmission):** If a piece gets lost or damaged, the sender never gets a receipt, so it automatically sends a fresh copy.

## 1. Formal Setup: The 3-Way Handshake
1. **`SYN` (Client → Server):** Client initiates a connection and synchronizes sequence numbers.
2. **`SYN-ACK` (Server → Client):** Server acknowledges the request and sends its own sequence number.
3. **`ACK` (Client → Server):** Client confirms receipt; the session is now `ESTABLISHED`.

## 2. Formal Close: The 4-Way Wave
1. **`FIN` (Client → Server):** Client finishes sending data and requests to close its side.
2. **`ACK` (Server → Client):** Server acknowledges the `FIN` (enters `CLOSE_WAIT` while finishing its own data).
3. **`FIN` (Server → Client):** Server finishes sending data and requests to close its side.
4. **`ACK` (Client → Server):** Client confirms closure and enters `TIME_WAIT` (2MSL) before fully closing.

## 3. Cybersecurity Scenarios
- **SYN Flood (DoS):** Attacker floods a server with spoofed `SYN` packets and never sends the final `ACK`, exhausting half-open connection memory.
- **TCP SYN Scan (Reconnaissance):** Scanner sends `SYN` → receives `SYN-ACK` → immediately sends **`RST`** (Reset) instead of `ACK` to detect open ports stealthily.

## Study Scorecard

| Topic | Score | Key Takeaway |
| :--- | :---: | :--- |
| TCP 3-Way Handshake & SYN Floods | 2 / 2 | Incomplete handshakes (`SYN` without `ACK`) indicate potential floods or scans. |
| TCP Teardown & Scan Flags (`RST`, `TIME_WAIT`) | Completed | `RST` aborts half-open scans; `TIME_WAIT` absorbs delayed packets. |

# TCP vs. UDP: Transport Layer Protocols

Both **TCP** and **UDP** move data between applications across a network, but they trade off between **accuracy** and **speed**.

---

## Side-by-Side Comparison

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection Type** | **Connection-oriented** (3-way handshake setup & 4-way close) | **Connectionless** (sends data immediately with no handshake) |
| **Reliability** | **Reliable** (uses sequence numbers, `ACK` receipts, and retransmissions) | **"Unreliable"** (fire-and-forget; lost packets are never resent) |
| **Flow Control** | **Yes** (uses Window Size so the receiver can slow down the sender) | **No** (sender transmits as fast as it wants) |
| **Speed & Overhead** | **Slower** (larger header, waits for acknowledgments) | **Faster** (tiny header, zero waiting for receipts) |
| **Real-World Analogy** | Registered mail with tracking and signature confirmation | Throwing paper airplanes or live radio broadcasting |
| **Common Uses** | Web browsing (`HTTPS`), File transfers (`FTP`), Email (`SMTP`), `SSH` | Live video/voice calls, Online gaming, `DNS` lookups, `DHCP` |
| **Cybersecurity Risks** | `SYN` Floods, Session Hijacking, Slow-Read (`ZeroWindow`) attacks | `UDP` Floods, DNS/NTP Amplification DDoS attacks |

---

## Key Features Summary

### TCP (Built for Accuracy)
1. **Connection-Oriented:** Formally opens (`SYN` → `SYN-ACK` → `ACK`) and closes (`FIN` → `ACK`) sessions.
2. **Reliable Delivery:** Numbers every packet (`Seq`), confirms receipt (`ACK`), and resends missing data.
3. **Flow Control:** Uses **Window Size** (`Win`) to prevent overwhelming the receiver's buffer.

### UDP (Built for Speed)
1. **Connectionless:** No formal greeting or goodbye before sending packets.
2. **"Unreliable" Delivery:** No error recovery, packet reordering, or retransmissions.
3. **No Flow Control:** The sender controls the transmission speed regardless of receiver capacity.

---

## When to Use Which?
- **Choose TCP** when missing even one piece of data breaks the result (downloading software, loading a bank webpage, sending a password).
- **Choose UDP** when speed matters more than perfection and a tiny glitch is okay (live Zoom calls, multiplayer gaming, streaming live sports).
## Study Scorecard

| Topic | Score | Key Takeaway |
| :--- | :---: | :--- |
| TCP 3-Way Handshake & SYN Floods | 2 / 2 | Incomplete handshakes (`SYN` without `ACK`) indicate potential floods or scans. |
| TCP Teardown & Scan Flags (`RST`, `TIME_WAIT`) | 3 / 3 | `RST` aborts half-open scans; `TIME_WAIT` absorbs delayed packets. |
| TCP vs. UDP Features, Use Cases & Security | 3 / 3 | TCP prioritizes reliability & flow control; UDP prioritizes speed for real-time traffic. |

## What Is a Datagram?
A **datagram** is a single, self-contained bundle of data sent over a connectionless network (like UDP) that carries its own source and destination addresses without relying on a prior handshake or delivery tracking.

- **Self-Contained:** Holds the Source Port, Destination Port, Length, Checksum, and Payload (data) in one independent unit.
- **Independent Routing:** Each datagram is treated separately by routers and may arrive out of order or be dropped without retransmission.
- **Security Note:** Because no handshake is required, attackers can easily **spoof** (fake) the Source IP address on UDP datagrams to launch DDoS amplification attacks.

### Data Names Across Network Layers (PDU Cheat Sheet)

| Layer / Protocol | Data Unit Name | Real-World Analogy |
| :--- | :--- | :--- |
| **UDP** (Transport Layer) | **Datagram** | A **postcard** (has an address, sent solo, no tracking receipt). |
| **TCP** (Transport Layer) | **Segment** | A **numbered box** in a tracked shipment (`Seq` & `ACK` receipts). |
| **IP** (Network Layer) | **Packet** | The **shipping label** with the street address (`IP address`). |
| **Ethernet / Wi-Fi** (Data Link Layer) | **Frame** | The **delivery truck** carrying it to the next local stop (`MAC address`). |

+-------------------------------------------------------------------+

| IP Header:  Source IP: 10.0.0.15  --->  Dest IP: 8.8.8.8 (Google) |
+-------------------------------------------------------------------+

| UDP Header: Source Port: 51234    --->  Dest Port: 53 (DNS)       |
|             Length: 36 bytes      |     Checksum: 0x4a2f          |
+-------------------------------------------------------------------+

| Payload:    "What is the IP address for google.com?"              |
+-------------------------------------------------------------------+


# Common Network Ports & Protocols

Network ports (`0`–`65535`) act like virtual doors on a host, directing incoming **TCP** or **UDP** traffic to the right service.

## Essential Ports Cheat Sheet

| Port | Transport | Service | Purpose | Security Consideration |
| :--- | :---: | :--- | :--- | :--- |
| **20 / 21** | TCP | FTP | File transfers (Data / Control) | Unencrypted; replace with SFTP (`22`). |
| **22** | TCP | SSH / SFTP | Encrypted remote login & file transfer | Protect with SSH keys; block brute-force attempts. |
| **23** | TCP | Telnet | Unencrypted remote login | Obsolete & insecure; always disable. |
| **25** | TCP | SMTP | Outgoing email routing | Secure against open-relay spam abuse. |
| **53** | UDP / TCP | DNS | Domain name to IP resolution | UDP for standard queries; TCP for zone transfers. |
| **67 / 68** | UDP | DHCP | Automatic IP address assignment | Watch for rogue DHCP spoofing on LANs. |
| **80** | TCP | HTTP | Unencrypted web traffic | Plain text; redirect to HTTPS (`443`). |
| **110 / 143** | TCP | POP3 / IMAP | Email retrieval (Download / Sync) | Use encrypted POP3S (`995`) & IMAPS (`993`). |
| **161 / 162** | UDP | SNMP | Network device monitoring | Use SNMPv3 for encryption & authentication. |
| **443** | TCP | HTTPS | Encrypted web traffic (TLS) | Standard secure web port; inspect for hidden C2 traffic. |
| **445** | TCP | SMB | Windows file & printer sharing | Block at firewall perimeter; major ransomware vector. |
| **3389** | TCP | RDP | Windows graphical remote desktop | Never expose directly to internet; require VPN + MFA. |

## Port Number Ranges
- **0–1023:** Well-Known Ports (System & core protocols)
- **1024–49151:** Registered Ports (Vendor applications & databases)
- **49152–65535:** Ephemeral / Dynamic Ports (Temporary client-side ports)


