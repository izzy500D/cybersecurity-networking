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

# Networking Basics: IPv4, Sockets, Ports, and DNS

## 1. IPv4 Addresses (The Building Address)
* **IPv4 (Internet Protocol version 4):** The standard 4-part numerical address used to identify devices on a network (e.g., `192.168.1.10`).
* **Private IP:** Assigned by your home router to devices inside your local network (e.g., `192.168.x.x` or `10.x.x.x`). Not visible on the public internet.
* **Public IP:** Assigned by your Internet Service Provider (ISP) to your router to communicate on the wider internet.
* **NAT (Network Address Translation):** The process your router uses to translate your device's private IP into your router's public IP when sending traffic out to the internet.

---

## 2. Sockets & Ports (The Full Delivery Label)
* **Socket:** The complete communication endpoint combining an **IP Address + Protocol + Port Number**.
  * **Client Socket (Your Device):** `192.168.1.10 : 61204` (Private IP + Temporary Port)
  * **Server Socket (Website/Service):** `142.250.190.46 : 443` (Public IP + Permanent Port)

### Types of Ports

| Port Type | Range | Who Uses It | Purpose |
| :--- | :--- | :--- | :--- |
| **Non-Ephemeral (Well-Known)** | `0 – 1,023` | **Servers / Websites** | Permanent, fixed doors so clients always know where to connect (e.g., Port `443` for HTTPS, Port `53` for DNS). |
| **Ephemeral (Dynamic)** | `1,024 – 65,535` | **Clients (Your Device)** | Temporary, random ports opened for a single session and closed immediately after. |

---

## 3. DNS (The Internet's Phonebook)
* **DNS (Domain Name System):** Translates human-friendly domain names (like `google.com`) into computer IP addresses (like `142.250.190.46`).
* **Common Public DNS Servers:** Google (`8.8.8.8`), Cloudflare (`1.1.1.1`).

### How a DNS Lookup Works
1. **Local Cache:** Device checks its own short-term memory for a recent IP match.
2. **Recursive Resolver:** If not found, device sends a query to a DNS resolver (e.g., `8.8.8.8` on **UDP Port 53**).
3. **Server Hierarchy:** Resolver checks **Root Server** → **TLD Server (`.com`)** → **Authoritative Name Server** to get the exact IP.
4. **Connection:** Device receives the IP and connects to the website's server socket (e.g., `142.250.190.46 : 443` via TCP).

### Why DNS Uses UDP Instead of TCP
* **Speed:** UDP skips TCP's 3-way handshake, sending the request in a single fast packet.
* **Small Payload:** Standard DNS questions and answers are tiny (under 512 bytes) and fit in one packet.
* **Exception:** DNS uses **TCP Port 53** only when responses are unusually large (such as server-to-server zone transfers).

---

## 4. Cybersecurity Takeaways
* **Port Monitoring:** Defenders watch for unexpected open ports or traffic on suspicious ports (e.g., Port `4444`) to detect malware.
* **DNS Security:** Attackers use **DNS Spoofing** to redirect users to fake IPs; defenders use DNS filtering to block malicious domains before a connection starts.

## 5. Top 5 Beginner Ports Cheat Sheet

| Port | Service | Protocol | What It Does | Cybersecurity Note |
| :--- | :--- | :--- | :--- | :--- |
| **22** | **SSH** (Secure Shell) | **TCP** | Lets admins log into remote servers and run commands securely. | Common target for brute-force password attacks; always use strong keys. |
| **53** | **DNS** (Domain Name System) | **UDP** (mostly) / **TCP** | Translates website names (like `google.com`) into IP addresses. | Watch for **DNS Spoofing** or malware using DNS tunnels to sneak data out. |
| **67 / 68** | **DHCP** (Dynamic Host Configuration Protocol) | **UDP** | Automatically hands out local IP addresses (like `192.168.1.25`) when a device joins Wi-Fi. | Attackers can set up fake "rogue" DHCP servers to intercept local traffic. |
| **80** | **HTTP** (Web Traffic) | **TCP** | Loads regular, **unencrypted** websites. | Traffic travels in plain text—anyone on the same Wi-Fi can read passwords sent over Port 80. |
| **443** | **HTTPS** (Secure Web Traffic) | **TCP** | Loads **encrypted** websites (the padlock icon in your browser). | Keeps web traffic private, though malware also hides inside Port 443 to blend in with normal traffic. |


# Networking Basics: IPv4, Sockets, Ports, and DNS

## 1. IPv4 Addresses (The Building Address)
* **IPv4 (Internet Protocol version 4):** The standard 4-part numerical address used to identify devices on a network (e.g., `192.168.1.10`).
* **Private IP:** Assigned by your home router to devices inside your local network (e.g., `192.168.x.x` or `10.x.x.x`). Multiple homes can reuse the same private IP, but two devices on the same Wi-Fi cannot.
* **Public IP:** Unique address assigned by your Internet Service Provider (ISP) to your router to communicate on the wider internet.
* **NAT (Network Address Translation):** The process your router uses to swap your device's private IP for your router's public IP when sending traffic out to the internet—and route replies back to the right device using port numbers.

---

## 2. Sockets & How Apps Avoid Mix-Ups
* **Socket:** The complete communication endpoint combining an **IP Address + Protocol + Port Number**.
  * **Client Socket (Your Device):** `10.0.0.1 : 6100` (Device IP + Temporary Port)
  * **Server Socket (Website/Service):** `10.0.0.2 : 5004` (Server IP + Permanent Port)
* **Key Rules:**
  * Total ports available per protocol: **65,536** (numbered `0` through `65,535`).
  * **TCP and UDP ports are completely separate:** `TCP/53` and `UDP/53` are two different doors.
  * **Ports are for communication, not security:** Hiding a service on a different port number does not encrypt data or stop port scanners.

### The 3 Official Port Ranges

| Port Range | Official Name | Permanent or Temporary? | Who Uses It? |
| :--- | :--- | :--- | :--- |
| **`0 – 1,023`** | **Well-Known Ports** | **Permanent** (Non-ephemeral) | Core internet services (e.g., `80` HTTP, `443` HTTPS, `53` DNS, `143`/`993` IMAP). |
| **`1,024 – 49,151`** | **Registered Ports** | **Permanent** (Non-ephemeral) | Specific apps & protocols registered by organizations (e.g., **`5004` for VoIP/RTP**). |
| **`49,152 – 65,535`** | **Dynamic / Ephemeral Ports** | **Temporary** (Ephemeral) | Client devices (your phone or laptop) opening temporary return doors for active tabs or calls. |

---

## 3. Beginner Ports Cheat Sheet (Including Safe vs. Unsafe Pairs)

| Port | Service | Protocol | What It Does | Cybersecurity Note |
| :--- | :--- | :--- | :--- | :--- |
| **22** | **SSH** (Secure Shell) | **TCP** | Lets admins log into remote servers and run commands securely. | Common target for brute-force login attacks; use SSH keys and disable root login. |
| **53** | **DNS** (Domain Name System) | **UDP** (mostly) / **TCP** | Translates website names (like `google.com`) into IP addresses. | Watch for **DNS Spoofing** or malware hiding data inside DNS queries. |
| **67 / 68** | **DHCP** | **UDP** | Automatically assigns local Private IPs when a device joins Wi-Fi (`67` = server, `68` = client). | Attackers can run rogue DHCP servers to intercept local network traffic. |
| **80** | **HTTP** (Web) | **TCP** | Loads regular, **unencrypted** websites. | **Unsafe:** Sends data in plain text; attackers on the same Wi-Fi can read passwords. |
| **443** | **HTTPS** (Secure Web) | **TCP** | Loads **encrypted** websites (TLS/SSL padlock). | **Safe:** Encrypts web traffic, though attackers also hide malware traffic inside Port 443. |
| **143** | **IMAP** (Email Sync) | **TCP** | Syncs email inboxes across multiple devices in **plain text**. | **Unsafe:** Passwords and emails travel unencrypted; replaced by Port `993`. |
| **993** | **IMAPS** (Secure Email Sync) | **TCP** | Syncs email inboxes across multiple devices using **TLS/SSL encryption**. | **Safe:** Modern standard for keeping email synced across phones and laptops. |
| **5004** | **RTP / VoIP** (Internet Voice) | **UDP** | Carries live audio and video packets for internet calls (e.g., WhatsApp, Zoom). | Uses **UDP** for speed so live calls don't lag; must be encrypted to prevent eavesdropping. |

---

## 4. DNS (The Internet's Phonebook)
* **How a DNS Lookup Works:**
  1. **Local Cache:** Device checks its own memory for a recent IP match.
  2. **Recursive Resolver:** Device sends a fast query to a DNS resolver (e.g., `8.8.8.8` on **UDP Port 53**).
  3. **Server Hierarchy:** Resolver checks **Root Server** → **TLD Server (`.com`)** → **Authoritative Name Server** to get the exact IP.
  4. **Connection:** Device connects to the website's server socket (e.g., `142.250.190.46 : 443` via TCP).
* **Why DNS Uses UDP:** Looking up a name is a tiny, single-packet question where speed matters more than TCP's 3-way handshake (DNS only switches to **TCP Port 53** for huge responses like server zone transfers).



