<h3>Secure Network Designs</h3>
Bad network designs include:
- Single points of failure: single points of failures become points to be attacked.
- Complex Dependencies: overly complex dependencies hide actual sources of failure behind layers of unnecessary complexity.
- Prioritizing Availability over Confidentiality
- Lack of Documentation and Change Control: Lack of documentation or change control makes it nearly impossible to audit changes that occur.
- Overdependence on Perimeter security: security isn't just on the borders but should also have internal hierarchies to prevent an internalized threat rapidly gaining access to everything.
- Fails to support business workflows
Networks should support business workflows while not making the network unsecure for the sake of ease. The best way of doing this is segmenting networks into logical sections.
- Users need to access the network with an assigned channel and address. The connection should be authenticated and deny unauthorized users and devices.
	- Emails and Mail server/services need to have access both to internal network areas and externally to send and receive emails. Typically these types of systems that need a view of the external world while being secure are put on their own network segment.
	- Boundary devices are useful to segment a network
		- Routers: Routes traffic based on Network Layer (Layer 3). Typically more involved than switches and bundled with other devices.
		- Wireless Access Points: Act as wireless connections to a network. Data Link Layer (Layer 2).
		- Firewalls: Block or allow traffic based on rules. Works at Transport Layer or higher (Layer 3+)
		- Domain Name System Server: hosts name records and performs lookups for traffic going in or out of a network segment Works at the Application Layer (Layer 7).
		- Load Balancers: Distributes traffic to different segments using the Transport Layer (Layer 4)
Routing and Switching Protocols are used to send messages to select targets rather than a wide-area broadcast to all connected devices. Data Link (Layer 2) connections are forwarded to directly connected devices within the same LAN, while Network (Layer 3) includes the ability to forward to another network domain.
- Address Resolution Protocol: matches an IP address to a MAC address
- Internet Protocol: Is the numeric address of a device on a network
- Other Routing Protocols:
	- Border Gateway Protocol: Pathing between ISPs
	- Open Shortest Path First: Routes based on Link state (open/close)
	- Enhanced Interior Gateway Routing Protocol: Evaluates the cost of taking a route and forwards based on those weights.
	- Routing Information Protocol: A protocol that counts hops to determine distance to a destination node
Network Zones are broken up into 3 major groups: Internal, External and Public zones
- Intranet is the internal private network. LANs or VLANs
	- Communication inside an Intranet is referred to as East-West Traffic.
	- Even internal devices should be treated with suspicion; Zero-Trust should be applied to internal traffic as no perimeter is impervious to compromise.
- Extranet is the outward facing devices that are semi-trusted. Business partner networks. Must Authenticate before joining.
	- Extranets sometimes are used as Demilitarized Zones (DMZs) that include services that need connections to the outside world. Servers in a DMZ may be known as bastion hosts and have more restricted functions and configurations to limit damage in the case they are compromised.
		- DMZs may be placed between a router and the internet (Screened subnet), or be connected as a branch from a firewall device (Triple Homed Firewall) that is the boundary between the network and the internet. 
		- Similar ideas can be applied to hosts and small-time networks. Hosts can be set up as DMZ hosts.
	- Communication in and out of a network (or between an Extranet and the wider Internet) is known as North-South Traffic.
- Internet/Guest is an anonymous zone that anyone can get into. Should not be trusted.
<h3>Common Attacks</h3>
Layer 2 (Data Link Layer) attacks tend to focus on information gathering.
- Man in the Middle: Listens for packets and modifies them before they reach their destination.
- MAC Cloning: by listening to packets being sent on a network an attacker may be able to make a packet look like it was sent by an internal or trusted user.
- ARP Poisoning: Attackers claim or "poison" IP addresses in a MAC table because ARP does not have any validation mechanism, merely a "claim it to use it" system via ARP reply packets. The system assumes that a reply can only originate from a valid request at some point, and puts the new data in the table. Once an address has been poisoned, all packets that were to be transmitted to the target are sent to the attacker to be modified or read. 
- MAC Flooding is an attack that exhausts the memory of a Switch by making an absurdly large MAC address table. When a switch is overwhelmed like this, it stops trying to send messages to a specific host and instead sends as a wide area broadcast. This allows attackers to see all packets and network structure.
	- Broadcast Storms are a form of Denial of Service that takes advantage of a network being unable to deliver a message via multicasting. Switches, Hubs and Bridges will forward messages through the network until it can be delivered. However, if the network loops the message may be delivered multiple times, each hop amplifying the number of packets being sent until it overloads the connection. 
		- Spanning Tree Protocol and Bridge Protocol Data Unit Guard are strategies to prevent Broadcast storms.
			- STP organizes devices into a hierarchy to prevent loops from forming. It does this by calculating the cost of a port when it is connected.
				- Bridge Protocol Data Unit Guard is a setting that prevents 'late-joiners' to add themselves as a switch or other network device when mapping a network topology. 
	- MAC addresses can be filtered or limited to certain addresses. This might include a whitelist, or allowing only a certain number of addresses to be added to the port.
	- Systems can use DHCP to track hosts to make sure they aren't attempting to spoof MAC addresses. This is done by inspecting packets related to IP addressing or ARP.
- Ports should have an access control system for network devices. 
	- Network Access Control (NAC) allows administrators to create policies to determine who can access a network and how much access they should have.
	- Port-based NAC is an automated NAC system that uses an [[Chapter 7]]AAA server to authenticate the device attempting to connect to a port.
	- To help determine if a system is following policy a posture assessment may be done on a host. A posture assessment is a health check to ensure that a system is kept up to date in compliance with policy.
		- Assessments are done by agents - software on the client device that do the necessary actions for the authenticating server. Agents may be either persistent or dissolvable (removes themselves after use)
<h3>Wireless Infrastructure</h3>
Wireless Access points need to have confidential connections, ensure integrity of communications and be accessible to authorized users. Common concerns to keep track of:
- Placement: Not only to cover the maximum area per access point, but also to ensure that access points do not interfere with each other.
	- Co-channel interference is when two WAPs use the same frequency and interfere with each other
	- Adjacent channel interference is when WAPs on two different channel interfere with each other when the 20MHz of channel space overlap.
	- Do a site survey to get a heatmap of access locations
- Confidentiality:
	- WiFi Protected Access (WPA) - Iteration on WEP, RC4 but adds Temporal Key Integrity Protocol to improve strength.
		- WPA2 uses 128-bit AES cipher for communication, replacing RC4
			- WPA2 uses a pre-shared key
		- WPA3 is the next version
			- Simultaneous Authentication of Equals replaces 4-way handshake from WPA2 and uses Diffie-Hellman key agreement
			- Enhanced Open
			- Updates cryptographic protocols - replaces AES CCMP with AES Galois Counter Mode Protocol (GCMP)
			- Mandates the use of management protection frames
			- WPA3 uses the same key system, but it changes the authentication method from a secret hash to the 4-way handshake system.
	- Wired Equivalent Privacy (WEP) - Early standard for WiFi security. Uses RC4 stream cipher.
- WAPs may or may not require authentication to access, depending on how it was setup.
	- Open Authentication does not require authentication to access the network, but also transmits data unencrypted.
		- Open Authentication may be paired with a captive portal: connection is automatically redirected to a splash on association with the WAP. The user then authenticates to the provider's network. Think terms and conditions on accessing grocery store internet.
	- Enterprise/IEEE 802.1X Authentication are alternatives to Open/Personal Authentication.
		- Implements Extensible Authentication Protocol (EAP) or Extensible Authentication Protocol over Wireless (EAPoW).
			- EAP is a framework for negotiating authentication mechanisms, rather than an actual system.
				- EAP-TLS is a system using EAP framework to encrypt Transport Layer communications. Uses locally installed certificate to authenticate with server, typically given by a smart card or installed on a Trusted Platform module.
				- Protected Extensible Authentication Protocol (PEAP) only requires a server-side key certificate. The authentication happens on the client side through a secure tunnel/VPN connection using EAP-MS-CHAPv2 or EAP-Generic Token Card.
				- EAP-Tunneled Transport Layer Protection (EAP-TTLS) is like PEAP but can use any other inner authentication method.
				- EAP with Flexible Authentication via Secure Tunnelling (EAP-FAST) does not use a certificate to set up a tunnel but instead uses a Protected Access Credential that is generated for each new user from the master authentication key on the server. This however requires that the PAC needs to be distributed securely, either though a offline solution (storage device) or by key exchange.
		- Uses an AAA server using RADIUS or TACTACS+ as validation.
- Wireless networks have potential vulnerabilities in Rogue Access Points and Evil Twins.
	- Rogue Access Points are Wireless Access Points that are part of a network without authorization. Rogue access points may be unsecure and used to capture credentials or act as a backdoor into the network.
	- Evil Twins are Rogue Access Points that impersonate a legitimate access point.
- Wireless connections are vulnerable to Disassociation/Deauthentication attacks that spoof/repeat existing packets with new headers or values.
- Wireless connections are vulnerable to jamming
<h3>Load Balancing and DDoS protection</h3>
DDoS attacks typically work on flooding a target with SYN or Network Time Protocol (NTP) packets. Some targets can cause knock-on effects - typically critical infrastructure like DNS servers will prevent other devices from being able to access resources that it knows the address to. Attacks that target these underlying infrastructure systems are known as amplification attacks.
- When faced with flooding ISPs will drop packets destined to the target with an ACL or packet blackhole.
	- Blackholes are dead-ends that can't reach any other part of the network. They are useful for isolating hostile traffic and are less computationally expensive than ACLs with high traffic.
	- Blackhole redirects can be triggered by Border Gateway Protocol automatically (Remotely Triggered BlackHoles).
		- Variation of Blackholing is Sinkholes where traffic is routed to another network rather than to a deadend.
- Rather than simply dropping packets, systems can instead distribute requests across multiple pools. A load balancer is used to do this - either at the network layer or the application layer.
	- Load balancer strategies vary. Strategies are also known as schedules. Simple = Round Robin/Queue. More complex methods take into account number of active connections or response time or manual weighting by a human administrator.
		- Sessions might need to be tied to a particular node in a server. Traffic might be tied to source IP or a session affinity (aka ID number) to ensure network traffic goes to the correct node.
		- Applications can use persistence/cookies to ensure that traffic stays to a node.
Embedded systems are also vulnerable to attacks - attacks that target them are known as operational attacks. Think how hacking looks like in anime and TV shows; those are operational attacks.