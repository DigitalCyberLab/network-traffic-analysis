# TCP Traffic Analysis

## 1. Overview

This investigation analyzes TCP communication between a MacBook Air administrator workstation and an Ubuntu Server virtual machine. The objective was to capture and examine a TCP connection, identify the three-way handshake, and verify normal connection termination.

## 2. Lab Environment

- **Administrator Workstation:** MacBook Air
- **Server:** Ubuntu Server 26.04.1 LTS
- **Virtualization:** Oracle VirtualBox
- **Network Configuration:** Bridged Adapter
- **Server IP (Sanitized):** 203.0.113.20
- **Client IP (Sanitized):** 198.51.100.10
- **Network Interface:** enp0s3
- **Analysis Tool:** TShark
- **Capture Format:** PCAP

*Note: The IP addresses shown in this document are reserved documentation addresses. They replace the original private IP addresses used in the lab.*

## 3. Objectives

- Capture TCP traffic between the client and server.
- Examine the TCP three-way handshake.
- Identify TCP connection termination.
- Investigate unsuccessful connection attempts.
- Verify firewall behavior and temporary access rules.
- Sanitize the packet capture before public distribution.

## 4. Investigation Methodology

### Initial Connection Test

An initial connection attempt from the MacBook Air to TCP port 8080 on the Ubuntu server timed out.

Packet analysis showed repeated TCP SYN packets without a corresponding SYN-ACK response.

This indicated that the TCP connection could not initially be established.

### Firewall Investigation

The Ubuntu server's UFW firewall was active and configured to deny incoming connections by default. SSH traffic on port 22 was permitted.

A temporary firewall rule was added to allow TCP port 8080 specifically from the MacBook Air's IP address.

### Successful Connection Test

A temporary Netcat listener was started on the Ubuntu server:

```bash
nc -lv 8080
```

A connection test was then performed from the MacBook Air using the sanitized server address as a documentation example:

```bash
nc -vz 203.0.113.20 8080
```

The original lab connection succeeded.

*Note: The sanitized documentation address is illustrative and is not intended to be used to reconnect to the original lab server.*

### Packet Capture

TShark captured the successful TCP communication on interface `enp0s3`.

The resulting capture contained six packets demonstrating the TCP handshake and connection termination.

## 5. Packet Analysis Results

| Packet | TCP Flags | Description |
|---|---|---|
| 1 | SYN | Client initiates connection |
| 2 | SYN-ACK | Server acknowledges request |
| 3 | ACK | Client completes handshake |
| 4 | FIN-ACK | Client begins connection termination |
| 5 | FIN-ACK | Server responds and closes its side |
| 6 | ACK | Client acknowledges server termination |

### Connection Details

- **Client IP (Sanitized):** 198.51.100.10
- **Server IP (Sanitized):** 203.0.113.20
- **Original Client Port:** 49745
- **Server Port:** 8080
- **Total Packets:** 6
- **TCP Handshake:** Successful
- **Connection Termination:** Normal

## 6. Security and Firewall Verification

After testing, the temporary firewall exception for TCP port 8080 was removed.

UFW was checked again to confirm that the temporary rule was no longer present.

The default incoming-deny policy remained active, and SSH access on port 22 remained permitted.

This restored the server's firewall configuration after testing.

## 7. Capture Sanitization

Before uploading the packet capture to GitHub, the original client and server IP addresses were replaced using `tcprewrite`.

The Ethernet addresses were also replaced with generic values.

The sanitized capture was re-examined with TShark to verify that:

- Original private IPv4 addresses were no longer present.
- Replacement addresses were used consistently in both communication directions.
- All six TCP packets remained intact.
- TCP flags and connection sequence were preserved.

The public capture uses reserved documentation addresses:

- **Client:** 198.51.100.10
- **Server:** 203.0.113.20

These addresses are reserved for documentation and examples and are not assigned as ordinary public internet addresses.

## 8. Findings

The investigation demonstrated:

- Initial TCP connection attempts were unsuccessful.
- Firewall restrictions prevented the initial connection.
- A narrowly scoped temporary firewall exception allowed the test connection.
- The TCP three-way handshake completed successfully.
- The connection terminated normally.
- The temporary firewall exception was removed after testing.
- The original firewall configuration was restored.

## 9. Conclusion

This investigation demonstrated practical TCP traffic analysis, packet capture, firewall troubleshooting, and verification of TCP connection establishment and termination.

TShark provided visibility into individual TCP packets and their flags, while UFW was used to investigate and control network access.

The sanitized packet capture provides supporting evidence of successful TCP communication without exposing the original private IP addresses.

## 10. Evidence

- **Sanitized TCP packet capture:** `Captures/tcp_handshake_capture_sanitized_final.pcap`
- **DNS packet capture:** `Captures/dns_capture.pcap`
- **TCP connection overview:** `Screenshots/03_TCP_Connection_Overview.png`
- **TCP three-way handshake:** `Screenshots/04_TCP_Three_Way_Handshake.png`
- **TCP connection termination:** `Screenshots/05_TCP_Connection_Termination.png`
- **Firewall port 8080 allowed:** `Screenshots/06_Firewall_Port_8080_Allowed.png`
- **Final firewall verification:** `Screenshots/07_Firewall_Final_Verification.png`
