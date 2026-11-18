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
