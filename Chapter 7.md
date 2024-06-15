Authentication Controls are systems to ensure the user is who they say they are and that they have the permissions to access the resource in the first place. Once a resource has been accessed, the usage should be logged to provide nonrepudiation.
- Identification
- Authentication
	- Check for something that only you can have, know or do. Examples include secret PIN codes, biometrics or physical keys.
	- In addition to the above, authentication can have attributes associated with it. Authentication attributes are non-unique and cannot be used independently but can enhance existing authentication.
		- Somewhere you are
		- Something you can do
		- Something you exhibit
		- Someone you know
- Authorization
- Accounting
Operating Systems have an authentication provider which is used by the user to authenticate before they can access the shell. This is known as a login or logon or sign-in.
- Windows Authentication can be Local or Network or Remote level. Local Sign-in compares a submitted credential to a stored hash in the Security Accounts Manager database in the registry. Network and remote logon use Kerberos but legacy applications might use NT LAN Manager authentication.
- Linux Authentication stores account names in `/etc/passwd` and the password hashes are stored in `/etc/shadow`. Network and remote logins are typically handled by SSH prototcol.
Some systems have a single-sign on; sign in on one device and all connections from that device are authenticated. One example is Kerberos as implemented by Microsoft's Active Directory.
<h3>Kerberos (port 88)</h3>
Kerberos is a single-sign-on network protocol. It is used in Microsoft Active Directory and consists of 3 parts:
- Client/Principal
- Application Server
- Key Distribution Center/Authentication Service
The Principal makes a request to the Authentication Service to get a Ticket that allows it access to the Application Server. Steps:
1. The client requests a Service Ticket from the Ticket Granting Service
	1. Client sends a Ticket Granting Ticket with the server it is trying to access plus an authenticator with time-stamped client ID encrypted with the session key.
	2. Ticket Granter responds with a Service Session Key and a Service Ticket for the session connected to the application server.
2. Client forwards the Service Ticket to the application server.
3. Application Server Decrypts the Ticket to confirm the ticket is legitimate and untampered, then decrypts the authenticator using the service session key.,
	1. Application server may respond with a verification message with the timestamp from the authentication ticket. This is mutual authentication.
4. Application server now responds to the client.
<h3>PAP, CHAP and MS-CHAP</h3>
PAP: Password Authentication Protocol based off plain-text password exchanges
CHAP: Challenge Handshake Authentication Protocol: Basically a password protected TCP handshake. The challenge prevents replay attacks and is repeated periodically during the connection.
- Challenge: server challenges client with random challenge message
- Response: client responds with a hash calculated based on the challenge message and client password
- Verification: Server verifies hash of the given password with the stored value. 
MS-CHAP: CHAP as implemented by Microsoft
<h3>Common Attacks</h3>
- Plaintext: reading unencrypted storage or data that has password information. PAP, basic HTTP/FTP and Telnet are all vulnerable to this in their base state.
- Online: threat attacks the authentication service using commonly used or cracked passwords. These frequently show up as multiple failed login attempts or logins from nonstandard locations.
- Spraying: brute force attacks
	- Brute force attacks attempt to test every possible combination of inputs. More complex algorithms and longer passwords make it more difficult to find a match.
	- Dictionary and Rainbow Table attacks generates hashes of plaintext inputs and attempts to match to a captured hash. Rainbow Tables are pre-computed lists of possible passwords. These can be defeated with password salting to make it harder to generate hashes without knowing what the salt is.
	- Hybrid attacks use a combination of Dictionary and Brute force attacks.
	- Example include Hashcat, L0phtcrack
- Offline: attacker gains access to internal storage for passwords. This shows up as access to these files.
<h3>Password Authentication Strategies</h3>
- Smart Card/Physical 2FA system uses a physical device to act as a requesting client . These can span from Smart Cards to USB keys to Internal Trusted Platform Modules inside computers. Network-level devices are also possible (hardware security module) that can act as a central password key management system/escrow.
	- User presents card to reader and is prompted to enter PIN
	- Inputting the correct PIN authorizes the card's cryptoprocessor to use it's private key to request a ticket from the Ticket Granting System. It then transmits to the request to the Authentication System.
	- The Auth System can decrypt the request because it has a matching public key
	- Auth System responds to the Ticket Granter session key and allows the bearer to use resources.
- Passwords can be stored in USB keys to help authenticate. It can also be stored in a cloud platform to allow access from any enabled device. Authentication can use Extensible Authentication Protocol as a framework for using multiple types of authentication using digital certificates on servers/clients.
	- EAP uses IEEE 802.1X port-based network access control. This means Authentication, Authorization and Accounting architecture.
		- Supplicant: requester of access
		- Network Access Server: network boundary devices (switches, routers and access points). Typically uses RADIUS on port 1813
			- Remote Authentication Dial-in User Service (RADIUS) is a standard of authentication.
				- Supplicant makes a connection with Network Access Server
				- NAS prompts for credentials
				- Supplicant submits credentials.
				- NAS uses credentials and shared secret key  to make an Access Request to the AAA server
				- AAA server decrypts data and verifies data
				- If correct AAA server sends Access-Accept packet
				- NAS allows supplicant to access network
			- An alternate to RADIUS is Terminal Access Controller Access-control System (TACACS+) for dedicated network appliance administration.
				- Uses TCP port 49.
				- All data is encrypted rather than just the authentication data.
				- Authentication, Authorization, Accounting functions are all discrete.
		- AAA server: server that administers access.
- Besides physical keys One-Time-Passwords can be used. OTPs are generated from a hash based on a shared secret an are only used once. OTP generation standards are defined by the Initiative for Open Authentication algorithms (not the same as OAuth! OAuth is Open _Authorization_).
	- HMAC-based One Time Password Algorithm (HOTP): using a shared secret, generates an 8-byte value for both a authenticator and on the system. Shared secret is used with an incrementing counter to generate the one time password of 6-8 digits.
	- Time-based One Time Password Algorithm (TOTP): enhances HOTP with a expiration time for the generated password.
- 2 Factor Authentication uses another account and sends a key to the other account to verify that the user is who they say they are.
- Biometrics target "what you are" for authentication. Despite how strong such systems are, there are problems:
	- Everyone who uses the system must be enrolled
	- The equipment is specialized - sensor modules to read or extract features and convert them into a form readable by computers.
	- False Rejection/Acceptance Rate where the sensor fails to read the biometrics correctly
	- Crossover Error Rate (Combined Rejection/Acceptance cases)
	- Throughput (slow)
	- May be discriminatory or inaccessible to the disabled
	- Can still be fooled by attackers
		- Fingerprints may be copied. This can be solved with a vein detector but doing so adds complexity
		- Facial scans suffer from high failure rates. 
			- Retina scanning is a more accurate variant but again is expensive and has false rejection rates related to diseases such as cataracts.
			- Iris scanning is a similar concept to retina scanning but is vulnerable to high resolution images
		- Voice recognition requires lots of efforts to build an accurate model of a user's voice and is also vulnerable to impersonation.
		- Gait analysis looks for user movement patterns.
			- Signature recognition checks for patterns in signing movement
			- Typing recognition checks for typing patterns (think WW2 radio recognition for radio operators)
	- Continuous authentication requires a user is logged in re-authenticates using another system and logs out automatically if the user leaves. Still in concept/research phase.
<h3>Implementation Guidelines</h3>
- Assess design requirements for Confidentiality, Integrity, Availability. An authentication system that doesn't protect communications, stored data, or locks resources behind an unusable amount of layers is not a good system.
- Determine what form of multifactor authentication works - use something that you are, something you know, or something you have.
	- You are: biometrics
	- You know: PINs, passwords, 2FA
	- You have: Key passes, Password Vaults, 2FA
- Use appropriate protocols or frameworks for your use cases
	- Kerberos for local sign-in with 2FA keypass. Good for Windows/Active Directory
	- 802.1X/Extensible Authentication Protocol/RADIUS for transmission of secure credentials
	- TACACS+ for administration of network system. Good for Cisco
- Be aware of common attack paths for passwords.