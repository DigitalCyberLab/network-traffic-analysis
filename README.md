# Network Traffic Analysis and Intrusion Detection

## Project Overview

This project focuses on capturing, monitoring, and analyzing network traffic using Wireshark and TShark in an Ubuntu Linux environment.

The goal is to develop practical cybersecurity skills by inspecting network packets, understanding common network protocols, identifying unusual traffic patterns, and investigating potential security threats.

## Project Objectives

- Capture and analyze network traffic.
- Understand TCP/IP communication.
- Examine DNS and TCP network protocols.
- Identify unusual network activity and investigate network communications.
- Test firewall rules and observe their impact on network connectivity.
- Document analysis findings and testing results.

## Tools and Technologies

- Ubuntu Linux Server
- Wireshark / TShark
- VirtualBox
- Netcat (nc)
- UFW Firewall
- TCP/IP Networking

## Lab Environment

- Virtualized Ubuntu Linux Server
- Bridged network adapter
- MacBook Air administrator workstation
- Command-line packet capture and analysis
- Authorized home network traffic

## Activities and Investigations

### 1. DNS Traffic Analysis
- Captured DNS queries and responses using TShark.
- Examined A and AAAA DNS records.
- Identified DNS query and response information.
- Analyzed DNS packet details and resolved IP addresses.

### 2. TCP Traffic Analysis
- Captured TCP communication between the administrator workstation and Ubuntu server.
- Investigated unsuccessful connection attempts caused by firewall restrictions.
- Temporarily modified firewall rules to permit testing.
- Captured and analyzed the TCP three-way handshake.
- Examined TCP connection termination using FIN and ACK flags.

### 3. Firewall Testing and Verification
- Inspected UFW firewall status and configuration.
- Tested the effect of firewall restrictions on incoming TCP connections.
- Temporarily allowed port 8080 for testing.
- Removed the temporary firewall rule after testing.
- Verified that the firewall returned to its original configuration.

### 4. Packet Capture Sanitization
- Sanitized packet captures before publishing them.
- Replaced original network IP addresses and MAC addresses in the TCP capture.
- Used sanitized packet information for public-facing analysis and documentation.

## Findings and Results

- Successfully captured and analyzed DNS queries and responses.
- Identified DNS A and AAAA records for example.com.
- Observed a successful TCP three-way handshake consisting of SYN, SYN-ACK, and ACK packets.
- Identified the TCP connection termination sequence using FIN-ACK and ACK packets.
- Confirmed that firewall restrictions initially prevented incoming connections on port 8080.
- Verified that temporarily allowing port 8080 permitted the TCP connection.
- Confirmed that the firewall was restored to its original configuration after testing, with incoming traffic denied by default and SSH access permitted.

## Screenshots and Documentation

The repository includes:

- Sanitized packet captures.
- DNS traffic analysis documentation.
- TCP traffic analysis documentation.
- Seven screenshots documenting packet analysis, TCP communication, and firewall verification.

## Skills Demonstrated

- Network traffic analysis
- Packet inspection
- DNS investigation
- TCP/IP fundamentals
- TCP handshake and termination analysis
- Linux command-line administration
- Firewall configuration and verification
- Network troubleshooting
- Packet capture sanitization
- Technical documentation
