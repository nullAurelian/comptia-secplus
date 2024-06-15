Identity is tied to accounts. Authentication is important for ensuring the integrity of an account and access to an account should be locked behind credentials. Communication should be encrypted as well.
- Certificates and Smart Cards: Using public key infrastructure to ensure that the authenticity of a document from an account is assured by a third-party certificate issuer.
- Tokens: Basically a ticket, tokens are issued by a single issuer and accepted by other partnered systems. This is faster than authenticating for each network that a user attempts to connect to.
- Identity Provider: a service that provides user accounts and processes authentication requests. It is an enhanced token system, as the created identity is valid for other partnered systems.
<h3>Onboarding and Offboarding</h3>
- Background check determines if a person who they say they are and not hiding illegal or risky activity. Some are done internally and others use third parties.
- Onboarding is the process of setting up all necessary accounts for a new user to do their job. This can be either new hires or contractors.
	- Secure transmission of credentials
	- Asset allocation
	- Training/policy
- Non-disclosure agreement assure confidentiality
- Offboarding ensures a graceful exit from the company and should cleanly shut off access from all accounts associated with that employee/contractor.
	- Accounts should be disabled
	- Keys should be returned
	- Employee-owned devices should be wiped
<h3>Personnel Policies, Identities and Account Types</h3>
- Separation of Duties prevent a single person being a bottleneck or having complete control over a process.
- Least Privilege users should only have the permissions they need to do the work they do.
	- Permissions may be set at individual or group levels. Group privileges are a method of centralizing permissions for administration. Users get access based on which groups they belong to.
	- Least privilege should also extend to administrator accounts - they should NOT be used under normal circumstances, instead having users with elevated privileges to their domains. Superusers should ONLY be used in cases of disaster recovery.
	- Service accounts are accounts used by scheduled processes or applications and should not be used by normal users. They should have privileges as required to run their processes or applications.
		- System service account is the Windows OS account and runs before the user logs on
		- Local Service accounts works like a normal user but is limited to local device only
		- Network Service works like a normal user but can use the computer's identity when accessing network resources (think sudo'd at network level).
	- SHARED ACCOUNTS ARE RISKY as they break non-repudiation/auditing rules.
- Job Rotation/Rotation of Duties
- Mandatory Vacation gives space for IT to audit a user and should be at least 1 week a year.
- Ensure strong passwords via policy and add some for of authentication measure
	- Guest accounts are a possible vector of attack due to lack of passwords by default
<h3>Accounts</h3>
- Accounts are defined by a unique security identifier (SID) and associated with a profile. 
	- Profiles include a home directory, fields to define identity (name, contact info, groups, etc).
	- Given access permissions for files and other network resources. May be assigned directly or inherited via security groups.
		- Group access policies can be configured via Group Policy Objects in Active Directory. 
	- Account permissions shouldn't be left at an elevated level, rather they should be able to grant elevated permissions temporarily. Doing so should leave an Audit trail.
	- Accounts need to have their actions logged for non-repudiation in audits. This can also be used to detect intrusions or attempted intrusions. Audit the following:
		- Account login and management
		- Process creation
		- Object Access
		- Changes to Audit policy
		- Changes to system security and integrity
	- Accounts with too many suspicious activities within a period of time should be timed out. Suspicious activities include failed logins, account expiration, unusual usage time.
- Should have policies to enforce security
	- Password Length: minimum or maximum lengths
	- Password Complexity: character types
	- Password Aging/Expiration date: force updates of passwords periodically
	- Password Reuse and history: prevent users from reusing old passwords consecutively
	- Location restrictions (Geofencing) is a tool to prevent suspicious activity based on access location. A login in Malaysia is suspicious for a company that only works in the US.
		- IP address restrictions may require users to only login from IPs associated with a region.
		- Some systems provide location services to detect where a user is via cell towers or GPS
	- Time of day restrictions can work to prevent suspicious logins based on standard work hours. 
		- May also check for impossible situations (login from New York followed by a login from China within 1 hour.)
- Accounts should be held accountable to use policies - Acceptable Use Policy, Code of Conduct, Social Media Analysis, Clean Desk and Use of Personal Devices.
	- Acceptable Use Policy
	- Code of Conduct: rules of behavior and professional standards. Prevent attacks that result of connecting company devices to outside social networks or emails.
	- Social Media Analysis
	- Clean Desk: Do not leave sensitive documents or devices open to be read
	- Use of Personal Devices: Personal devices may be a vector for attacks.
<h3>Access Controls</h3>
- Access control Types
	- Discretionary Access Control: Individually allow or deny access to a resource through an access control list/whitelist. Very flexible but weak to insider threats and compromised accounts. Examples include sudo.
	- Role-based Access Control: A set of roles are defined and then applied to accounts. Only the system owner can change roles and assign them to users. Examples include security groups.
	- Mandatory Access Control: requires that objects and subjects are granted a clearance level aka label that must be met for a user to access a resource. These labels are non-discretionary and cannot be changed by the user the level is assigned to.
	- Attribute-Based Access Control: grants access based on contextual attributes including current OS, IP addresses, presence of updated patches.
	- Rules-Based Access Control can be any of the above types where access control policies are determined by system-enforced rules ie automated rather than assigned by a person. Basically, access to any resource in the system is Conditional to what the system is looking for.
		- Temporary elevation typically uses Conditional Access, where the user must complete some form of authentication to gain elevated permissions. 
		- To protect a system from users making significant changes, the privileged mode will be put under Privileged Access Management (think sudo). Privileged users can change how a system works and can log on to network systems remotely and should be checked to make sure they aren't abused.
			- AUDIT YOUR PRIVILEGED USERS ALWAYS
- Know the file-level access controls. Windows has configs for this, Linux uses `RWX` settings. (Read/Write/Execute in that order)
	- change with `chmod ${RWX} ${filename}` 
- Directory Services are the primary means of managing user privilege and authorization settings in an enterprise network. An example of this is LDAP (Light Weight Active Directory)
- Some systems are Federated. Federated systems trust each other and more importantly trusts the accounts other members of the Federation create. Federated systems are important for Cloud-based networks as they might not support Kerberos or Active Directory/LDAP.
	- Identity Providers and Attestation are the main concepts of a Federated network. 
		- Identity Providers, as the name suggests, provides and provisions the Identity a user/principal uses within a network. The IdP authenticates the user with a token or certificate.
		- The resource the user can use the token/certificate to ensure that a user is authentic. This is Attestation.
			- To communicate between members of the Federated system Security Assertions Markup Language (SAML) is used to attest. Communication is established using HTTP/HTTPS and the Simple Object Access Protocol (REST/SOAP).
			- RESTful API typically use Open Authentication(OAuth) to share information of a user between sites. Basically, a token that authorizes a user - however it does NOT authenticate.
				- Uses JSON web tokens to store data.
			- OpenID Connect is an authentication protocol that can be used in conjunction with OAuth.