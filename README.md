# OIBSIP
Task 1:
Network Security Task – Nmap Scan and ufw Firewall

This README explains the results obtained from Task 1 (Nmap scan) and Task 2 (UFW firewall configuration) based on the provided screenshots.

Task 1: Nmap Scan Results
Scan Summary:
Target IP: 192.168.56.101
Host Status: Host is up (very low latency)
Network Distance: 0 hops (local network)
Total Ports Scanned: 1000 TCP ports

Key Observations

1)All 1000 scanned TCP ports are in ignored/closed states.
2)Nmap reports:
Not shown: 1000 closed tcp ports (reset)
3)No open ports were discovered.
4)OS detection was attempted, but:
"Too many fingerprints match this host to give specific OS details"

Interpretation
1)The system is reachable but not exposing any TCP services on the default 1000 ports.
2)Closed ports responding with RST packets usually indicate:
3)A firewall is active, or No services are listening on those ports
4)OS fingerprinting failed because the lack of open ports provides insufficient data for accurate detection.

Security Implication
1)From an attacker’s perspective, this host has a low attack surface.
2)Absence of open ports significantly reduces the risk of remote exploitation.




Task 2: UFW Firewall Configuration

Firewall Status
UFW Status: Active and enabled on system startup

Configured Rules
Port / Service	Protocol	Action	Source
SSH (22)	TCP	ALLOW	Anywhere
HTTP (80)	TCP	DENY	Anywhere
SSH (22)	TCP (IPv6)	ALLOW	Anywhere (v6)
HTTP (80)	TCP (IPv6)	DENY	Anywhere (v6)

Commands Used
sudo ufw allow ssh
sudo ufw deny http
sudo ufw enable
sudo ufw status

Interpretation
SSH (port 22) is explicitly allowed to enable secure remote administration.
HTTP (port 80) is denied, preventing unencrypted web access.
Rules are applied to both IPv4 and IPv6, ensuring consistent protection.


Security Benefit
Restricting services using UFW helps enforce the principle of least privilege.
Allowing only essential services minimizes exposure to network-based attacks.



Task 4 Research Report on Common Network Security Threats - Given
and 
Task 6 Research Report on the Importance of Patch Management - Given



Task 7:Vulnerability Scanning with Nikto Results

Scan Summary
Tool Used: Nikto v2.5.0
Target Host: 127.0.0.1
Target Port: 80 (HTTP)

Key Findings
Missing Security Headers:
X-Frame-Options header not present (vulnerable to clickjacking).
X-Content-Type-Options header not set (may allow MIME-type sniffing).


Information Disclosure:
ETag headers may leak inode information (related to CVE-2003-1418).
/server-status endpoint exposed, revealing Apache server details.


HTTP Misconfiguration:
Allowed HTTP methods: GET, POST, OPTIONS, HEAD.


Critical Vulnerabilities Detected:
Arbitrary file read via malformed URLs (e.g., ///etc/hosts).
Multiple PHP backdoor file managers detected in WordPress directories.
Possible remote command execution vulnerability related to D-Link router paths.
Identified web shells capable of executing system commands.


Interpretation

1)The web server is highly vulnerable and appears to be either misconfigured or intentionally vulnerable.
2)Presence of PHP backdoors and web shells indicates a compromised or test environment.
3)These issues could allow attackers to:
    Read sensitive system files
    Execute arbitrary commands
    Fully compromise the server


Recommended Mitigations:
1)Remove malicious PHP files and reinstall WordPress from a trusted source.
2)Disable directory traversal and file inclusion vulnerabilities.
3)Restrict access to /server-status.
4)Add missing HTTP security headers.
5)Regularly scan the server using tools like Nikto and OpenVAS.


Task 8 :Capture Network Traffic with Wireshark

Overview

This document explains the network packets captured in the provided **Wireshark (.pcapng)** file. The capture demonstrates common network communication patterns at different layers of the TCP/IP model, including address resolution, transport-layer handshakes, data transfer, and connection termination.

The purpose of this capture is to understand how packets flow across the network, how protocols interact, and how packet-level evidence can be used for network troubleshooting and security analysis.



Environment

Tool Used: Wireshark
Capture Format: .pcapng
Protocols Observed: ARP, DNS, TCP, UDP, HTTP (if applicable)
Network Type: Local Area Network (LAN)



Packet Breakdown

1. ARP (Address Resolution Protocol)

Purpose:
ARP is used to map an IP address to a MAC address within the local network.

Observed Behavior:
ARP Request: "Who has <IP>? Tell <Source IP>"
ARP Reply: "<IP> is at <MAC address>"

Significance:

Required before any IP-based communication
Helps detect ARP spoofing attacks when abnormal patterns appear



2. DNS (Domain Name System)

Purpose:
DNS resolves domain names into IP addresses.

Observed Behavior:
DNS Query from client to DNS server
DNS Response containing resolved IP address

Significance:
Essential for web access
DNS traffic can be analyzed to detect tunneling or malicious domains


3. TCP – Three-Way Handshake

Purpose:
TCP establishes a reliable connection between two hosts.

Observed Packets:
1. SYN – Client requests connection
2. SYN-ACK – Server acknowledges request
3. ACK – Client confirms connection

Significance:
Confirms reliable session establishment
Missing steps may indicate packet loss or attacks (e.g., SYN flood)



4. Data Transmission (TCP/UDP)

Purpose:
Actual application data is transferred after connection setup.

Observed Behavior:
TCP segments carrying payload data
Sequence and acknowledgment numbers increment correctly

Significance:
Allows inspection of unencrypted protocols (eg: HTTP)
Encrypted traffic (HTTPS) still reveals metadata



5. HTTP (If Present)

Purpose:
Used for web communication between client and server.

Observed Behavior:
 HTTP GET / POST requests
 Server responses (200 OK, 404, etc.)

Significance:
 Demonstrates how web traffic is transmitted in plaintext
 Highlights why HTTPS is required for security



6. Connection Termination

Purpose:
Graceful shutdown of TCP connections.

Observed Packets:
FIN, ACK sequence

Significance:
Ensures all data is received before closing the session



Security Observations

 No malformed packets detected
 Normal handshake and termination observed
 Traffic appears legitimate and well-structured
 

Possible Threats (If Abnormal Patterns Exist):

 Repeated SYN packets → SYN Flood attack
 Multiple ARP replies → ARP Spoofing
 Unusual DNS queries → DNS Tunneling

