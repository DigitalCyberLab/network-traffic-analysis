# DNS Traffic Analysis

## 1. Overview

This investigation focused on capturing and analyzing DNS (Domain Name System) traffic using TShark in an Ubuntu Linux environment.

The objective was to observe DNS queries and responses, identify the network protocols involved, and understand how domain names are resolved into IP addresses.

## 2. Lab Environment

- Operating System: Ubuntu Linux Server
- Virtualization: Oracle VirtualBox
- Network Configuration: Bridged Adapter
- Packet Analysis Tool: TShark
- Network Interface: enp0s3
- Capture Format: PCAPNG

## 3. Investigation Objectives

- Capture DNS network traffic.
- Examine DNS queries and responses.
- Understand the difference between IPv4 and IPv6 DNS records.
- Identify source and destination addresses.
- Inspect captured packets using TShark.

## 4. Methodology

### Step 1: Identify Network Interface

The available network interfaces were identified using:

```bash
tshark -D
```

The primary network interface used for the investigation was `enp0s3`.

### Step 2: Capture DNS Traffic

DNS traffic was captured using:

```bash
sudo tshark -i enp0s3 -f "port 53" -c 20 -w /tmp/dns_capture.pcap
```

A DNS lookup was generated using:

```bash
nslookup example.com
```

Four DNS packets were successfully captured.

### Step 3: Save the Capture

The capture was copied into the project directory:

```bash
sudo cp /tmp/dns_capture.pcap /home/josh/Network_Traffic_Analysis/Captures/
```

File ownership was updated so the project user could access it.

### Step 4: Analyze Captured Packets

The capture was inspected using:

```bash
tshark -r ~/Network_Traffic_Analysis/Captures/dns_capture.pcap
```

An AppArmor restriction initially prevented TShark from reading the capture file. A local AppArmor profile override was configured to grant read-only access to the project capture directory.

AppArmor remained enabled throughout the investigation.

## 5. Packet Analysis Results

Four DNS packets were successfully captured.

| Packet | DNS Record | Description |
|---|---|---|
| 1 | A Query | Requested the IPv4 address of example.com |
| 2 | A Response | Returned two IPv4 addresses |
| 3 | AAAA Query | Requested the IPv6 address of example.com |
| 4 | AAAA Response | Returned two IPv6 addresses |

### DNS Concepts Observed

- **DNS:** Translates domain names into IP addresses.
- **A Record:** Provides an IPv4 address.
- **AAAA Record:** Provides an IPv6 address.
- **DNS Query:** A request sent to a DNS resolver.
- **DNS Response:** The resolver's reply containing the requested records.

## 6. Findings

The investigation successfully demonstrated DNS resolution using both IPv4 and IPv6 record types.

The captured traffic showed:

- DNS queries for `example.com`.
- Successful DNS responses.
- IPv4 address resolution through A records.
- IPv6 address resolution through AAAA records.
- Communication between the system and its DNS resolver.

No suspicious activity was identified in this limited four-packet DNS capture.

## 7. Security Considerations

Packet captures can contain sensitive network information, including IP addresses, MAC addresses, DNS queries, and other identifying metadata.

The capture intended for public GitHub publication was sanitized to reduce the exposure of sensitive information.

## 8. Conclusion

This investigation provided practical experience capturing and analyzing DNS traffic using TShark.

It demonstrated how DNS queries and responses work, how IPv4 and IPv6 records are resolved, and how packet captures can be inspected for network analysis.

The investigation also provided experience troubleshooting Linux file permissions and AppArmor security restrictions.

## 9. Evidence

- `Captures/dns_capture.pcap` — Sanitized DNS packet capture.
- `Documentation/DNS_Traffic_Analysis.md` — DNS investigation documentation.


