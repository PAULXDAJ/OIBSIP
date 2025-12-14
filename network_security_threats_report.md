**Research Report on Common Network Security Threats:**



Objective :

This report provides a comprehensive analysis of common network security threats, specifically focusing on Denial-of-Service (DoS) attacks, Man-in-the-Middle (MITM) attacks, and Spoofing. The analysis includes a description of each threat's mechanism, potential impact, mitigation strategies, and real-world examples.





1\. **Denial-of-Service (DoS) and Distributed Denial-of-Service (DDoS) Attacks**

A DoS attack is a malicious attempt to disrupt the normal traffic of a targeted server, service, or network by overwhelming it with a flood of internet traffic. A DDoS attack is a form of DoS attack that uses multiple compromised computer systems as sources of attack traffic. These compromised machines form what is known as a botnet.



Mechanism:

DoS:

A single attacker-controlled machine attacks the victim's resources (eg: bandwidth, processor capacity, database connections) with requests, rendering them unavailable to legitimate users.



DDoS:

An attacker commands a botnet to send massive amounts of traffic simultaneously, making it incredibly difficult to block the attack based on source IP address. Common methods include:



Volume-Based Attacks: Sending a huge volume of traffic (eg: UDP flood, ICMP flood).



Protocol Attacks: Exploiting weaknesses in the TCP/IP protocol stack (eg: SYN flood).



Application-Layer Attacks: Targeting specific web application elements with seemingly legitimate requests (eg: HTTP flood).





Impact:

1)Financial Loss: Direct loss of sales/revenue due to service unavailability.



2)Reputation Damage: Eroded customer trust and negative publicity.



3)Operational Disruption: Inability for employees/customers to access critical systems.







Mitigation:



1)Rate Limiting: Capping the number of requests a server will accept over a certain time window.



2)Intrusion Detection/Prevention Systems (IDPS): Identifying and blocking malicious traffic patterns.



3)Traffic Scrubbing Services (DDoS Protection Providers): Diverting all network traffic through a high-capacity filtering center that separates malicious botnet traffic from legitimate user traffic.



4)Load Balancing: Distributing traffic across multiple servers to prevent any single point from becoming overwhelmed.





Real-World Example

GitHub (2018): GitHub was hit with a massive 1.35 Tbps DDoS attack, one of the largest on record at the time. They used a sophisticated traffic scrubbing service to successfully mitigate the attack and remain online.









2\. **Man-in-the-Middle (MITM) Attacks:**

A MITM attack is a form of eavesdropping where an attacker secretly intercepts and relays messages between two parties who believe they are communicating directly with each other. The attacker gains full control of the session, enabling them to steal or manipulate data.



Mechanism



1)Interception: The attacker inserts themselves into the communication path. Common techniques include:



2)ARP Spoofing (Local Networks): Sending false ARP messages to associate the attacker's MAC address with the victim's gateway IP address.



3)DNS Spoofing: Redirecting the victim to a malicious website.



4)SSL/TLS Hijacking: Downgrading the connection security or using rogue certificates to decrypt encrypted traffic.



5)Decryption/Reading: The attacker captures the traffic, decrypts it if necessary (e.g., by presenting a fake certificate to the client), and reads the contents (credentials, financial data).



6)Manipulation: The attacker can modify the relayed information before it reaches the intended recipient.





Impact:



Data Theft: Stealing sensitive information like login credentials, credit card numbers, and proprietary data.



Data Manipulation: Introducing errors or malicious code into a transaction or communication.



Session Hijacking: Taking over an authenticated session to perform actions on behalf of the legitimate user.





Mitigation:



1)Use Strong Encryption (HTTPS/TLS): Ensuring all web traffic is encrypted end-to-end makes eavesdropping difficult.



2)Virtual Private Networks (VPNs): Encrypting all traffic between the client and a trusted server, making MITM attempts against the local network much less effective.



3)Public Key Infrastructure (PKI) and Certificate Pinning: Ensuring the client only trusts a specific, pre-approved cryptographic key/certificate for a given domain, thwarting attacks that use fake certificates.



4)Network Monitoring: Continuously monitoring for suspicious ARP/DNS activity.



Real-World Example

Firesheep (2010): A Firefox extension demonstrated the ease of session hijacking on unencrypted Wi-Fi networks by using packet sniffing to capture session cookies. This highlighted the risk of communicating over public, unsecured networks without encryption.











**3. Spoofing Attacks:**



Spoofing is the act of disguising a communication from an unknown source as being from a known, trusted source. The goal is to trick the recipient (user or system) into accepting, opening, or responding to the communication.



Mechanism :

1)IP Spoofing: An attacker modifies the source IP address in the header of a network packet to impersonate another device. This is often used in DoS/DDoS attacks to hide the attacker's true location.



2)MAC Spoofing: An attacker changes the physical MAC address of their network interface card (NIC) to evade MAC-based access controls or impersonate another device on a local network.



3)Email Spoofing: An attacker forges the sender's address (the "From" field) in an email to make it appear as if it originated from a trusted entity (e.g., a bank or a CEO). This is a core component of phishing attacks.



4)ARP Spoofing: (Also used in MITM attacks) Falsely linking an attacker’s MAC address with a legitimate IP address on the local network.







Impact:

Bypassing Security Controls: Impersonating a trusted host to gain network access.



Phishing/Social Engineering: Tricking users into revealing credentials or transferring money (via email spoofing).



Covering Tracks: Hiding the source of a DoS attack (via IP spoofing).







Mitigation:

1)Ingress Filtering (against IP Spoofing): Routers at the edge of a network should be configured to drop packets arriving from the outside if their source IP address is known to be internal to the network.



2)Email Authentication Protocols: Implementing Sender Policy Framework (SPF), DomainKeys Identified Mail (DKIM), and Domain-based Message Authentication, Reporting, and Conformance (DMARC) to verify the authenticity of an email sender.



3)Anti-Spoofing Tools: Using tools that monitor and validate ARP tables and alert administrators to discrepancies.



4)User Training: Educating users to carefully inspect email headers and URLs for subtle differences before clicking links or providing information (especially important for email spoofing/phishing).





Real-World Example

The "CEO Fraud" or Business Email Compromise (BEC): Attackers use email spoofing to impersonate a company executive (e.g., the CEO) and trick an employee in the finance department into urgently transferring a large sum of money to a fraudulent account. This attack has resulted in billions of dollars in losses globally.



