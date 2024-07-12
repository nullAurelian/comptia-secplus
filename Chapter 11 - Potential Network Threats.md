1. Allocation for Network Addresses: 
	1. Have to know what addresses will be allocated to effectively snoop/monitor incoming/outgoing traffic. Static addresses should be documented, DHCP servers should have a limited range associated with a network group
		1. Bad DHCP can be used to starve a network by repeatedly requesting a new address via spoofed MAC addresses. Once a server is out of valid addresses, another may take over. If that one is compromised or otherwise rogue, traffic may become exposed or redirected.
2. DNS converts fully qualified domain names to IP addresses - phone book for the internet.
	1. Domains can be hijacked or impersonated using tricks such as common typos or character similarities. Other situations include lapsed registration (registration is required every year) or admin account compromise.
	2. Uniform Resource Locator (URL) redirects are a method to force a DNS to send users to another site. Redirects may send users to a site that phishes with a similar looking name and webpage.
	3. DNS records can be poisoned/fed incorrect information about a URL:IP relation to force a redirect to a fake site.
		1. DNS Security Extensions provide validation for DNS responses. Authoritative/safe servers can create secured data packets for network data. Will have a key system to verify the signature (much like a certificate).
		2. Only accept recursive queries from local hosts (IE do not respond to DNS requests from any host not directly connected to the server). Clients should only ask servers that have been authenticated.
		3. DNS servers typically run Berkley Internet Name Domain (BIND) and have known vulnerabilities.
3. Network Directories lists users, hosts, services (subjects), cloud storages (objects) on a network along with the permissions that the subjects have over objects (roles and permissions).
	1. Most directory services use Lightweight Directory Active Protocol (LDAP: port 389). LDAP is by default plaintext, but can have security layers bound to the server.
	2. Network directories should have a read role for the general users and a read/write for admins.
	3. LDAP should limit access to those on a private network (VPN or locally secured net).
4. Simple Network Management Protocol can be used for network devices to manage multiple devices. SNMP should only be run if the network is using it for all devices. Even if a device doesn't run SNMP but is on a network that does, it will be listed in the SNMP database of other devices.
	1. SNMP tracks traffic stats for other devices for each device. Agents can also be used to trap or log anomalies.
	2. SNMP data can be viewed from a central location using the SNMP monitor, which pulls data from the agents on all the other devices on the network.
	3. Internal SNMP device names are sent in plaintext so SNMP messages should be protected.
5. Application Layer Security
	1. Most communication is based off text transfer/HTTP. HTTP is stateless and plaintext, so lacks the security 
	2. SSL is another legacy transport protocol developed to improve on HTTP.
6. Transport Layer Security (TLS) is a standard for data security at the transport layer. Typically added HTTP to make HTTPS but also can be combined with other protocols (ie to create VPNs).
	1. TLS is implemented with digital certificates; the server is given a certificate by an authority to prove the identity of the server and validate the public/private key. The key is used with TLS to choose supported ciphers and negotiate an encrypted session.
		1. Host-level TLS is used for VPN
	2. TLS is still vulnerable to downgrades that allow backwards  compatibility. Older versions may be vulnerable to more exploits.
7. Any connection to the outside is a potential vector for an attack. Apply secure variants of protocols wherever possible. FTP, Email, Subscription Feeds, VoIP.
	1. In cases where there might not be enough security, an option may be to 'wrap' the protocol in encryption via a VPN tunnel.
	2. VPNs use Transport Layer Security as SSL VPN. SSL requires a listening server to act as the virtual network. Client is authenticated by the server via encrypted tunnel much like a RADIUS server. 
8. Below TLS at the application level is TLS at network level. Internet Protocol Security (IPSec) operates at Network level and does not require an agent like a solution at the Application level. Each host however must be set a policy/authentication method. This is less scalable than application level security.
	1. IPSec uses Authentication Header to perform a hash on an entire packet using a secret key and adds it to a packet to act as a validating system. It does NOT encrypt anything.
	2. IPSec uses Encapsulation Security Payload to provide encryption by adding a header, a trailer and an integrity check value around the data payload itself.
	3. IPSec relies on some form of Key Exchange over the Internet for ensure that there is a common secret key. Internet Key Exchange Protocol handles the authentication and exchange process. When two devices use Internet Key Exchange they form a Security Association.
		1. Phase 1 of IKE is authentication - exchange of certificates issued by a mutually trusted certificate authority.
		2. Phase 2 of IKE is transmission of the ciphers and keys via secure tunnel established in phase 1.
		3. IKE is run via Layer 2 (Data Link) Tunneling
9. VPNs are configured based on how they operate
	1. Split Tunnel vs Full Tunnel refers to how the device connects to the internet while also connected to the VPN. 
		1. Split uses the device's native internet connection and does not route the internet traffic through the VPN
		2. Full connects through the VPN and alters the client's IP and DNS to route through the VPN and/or a proxy server. This is better security but more infrastructure.
	2. Always on VPNs are set up whenever an internet connection over a trusted network is made using cached credentials.
	3. Subtype of VPN is Remote Desktop connections. These typically require a dedicated client app/agent on the device to remote into.
		1. SSH only allows terminal access
		2. Microsoft RDP allows for GUI based control
		3. Virtual Network Computing (VNC) and Teamviewer are alternatives for macOS/Linux
		4. HTML5 allows for client-less connections
	4. Remote Desktop administration can be in-band or out-of-band.
		1. In-band shares bandwidth with normal traffic
		2. Out-of-band uses a dedicated connection separate from traffic for control packets.
		3. Managing remote desktop functions may use Jump servers - basically a linking server in a DMZ of a VPN that acts as a single administration server. Admins connect to the jump server to connect to the application/RDP client. The Jump Server is the single allowed address to use RDP/remote desktop.
	5. Secure SHell (SSH) is a tool for managing systems remotely via command line terminal. SSH is configured using `/etc/ssh/sshd_config`. Can set to use username/password, public key authentication, Kerberos.
Guidelines for implementing secure network protocols:
1. Ensure that network fundamental functions (DHCP/DNS/Directory Access/Time Sync) services are protected and only known sources are used.
2. Have some form of monitoring of the network (ie Simple Network Management Protocol) on the network with logging.
3. Use secure protocols and have a secure system to deploy certificates or shared keys for encryption.
	1. Webservers: HTTPS
	2. Email servers: SMTP, POP3, IMAP
	3. File servers: FTPS, SFTP
	4. Email clients: S/MIME
	5. VoIP gateways and Endpoints: SIPS, SRTP
	6. VPN gateways: TLS VPN, IPSec, L2TP/IPSec
4. Implement out-of-band interfaces or jump servers to isolate management traffic for servers and infrastructure.