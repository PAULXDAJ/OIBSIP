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
