Steps: Incident response begins well before an actual incident
- Preparation for Incident: build up system resilience, hardening and security posture (policy + procedures)
- Identification of Incident: When a breach occurs, detect and identify what type of incident it is
	- The first person to be notified of an incident is known as the first responder.
- Containment of Incident: Limit spread of incident
- Eradication of Incident: Fix the root cause of the incident
- Recovery from Incident: Repair any systems that were damaged in incident
- Post-Mortem of Incident: Review what occurred, what could be done better
- Repeat
Who responds to an incident? The incident response team! Beyond the engineering side, bring in the following as stakeholders
- Legal
- HR
- Marketing
All stakeholders should follow a plan for secure communication regarding how to craft a response. Such communications should be secure, outside of normal communications channels to avoid interception. This will also need to include external stakeholders.
Have a response plan in place that lists procedures, contacts, resources for various incidents. Typical attacks/common attacker profiles should be prioritized.
Know the attacker Cyber Kill Chain so you can disrupt it.
- Recon: of target for vulnerabilities
- Weaponization: of a known vulnerability
- Delivery: of malware to the target
- Exploitation: once breached into the target via the vulnerability, do thing
	- Installation
	- Command and Control
- Actions
Understand MITRE ATTA&CK
Understand Diamond Model of Intrusion Analysis
- 4 Core features: the 4 aspects of an attack and a confidence (C) score that indicates data accuracy/reliability
	- Adversary
	- Capability
	- Infrastructure
	- Victim
Business Recovery vs Disaster Recovery vs Incident Response and Business Continuity
- Disaster recovery: Disaster recovery includes cases of natural disaster/fire on top of Security Incidents
- Business Recovery: Involves restoration of business after a disaster or incident
- Business Continuity: Involves restoration of operations during an incident including building of resilience for effected servers
- Incident Response: as covered in other chapters
	- Retention policy: after an incident, the actions taken should be logged.
Security and Information Event Management (SIEM) is a system to link logs, actions and activity in a manner that allows for quick readings of a system.
- Correlation between multiple logs, useful for seeing the wider effects of an attack
- Common logging platforms:
	- Syslog: open format that is well known. Uses port UDP 514. Contains a PRI code header that contains timestamp, source host, and tag for process
		- Rsyslog: same format as syslog but uses TCP
		- Syslog-NG: different format but can use TCP and more advanced filter options
	- journalctl: Linux text logging
	- NXlog: log normalizer for Windows, takes logs and converts them to a normalized Windows XML
Check for Metadata: properties of a file regarding how it is created, stored or transmitted. Basically: context.
- File attributes
- Web packet headers
- Email headers
- Call detail records
Data sources
- Protocol Analyzer Output
- Netflow/IPFIX:  a proprietary application that reports network flow to a database.
- sFlow: sampling system that measures traffics at different layers
- Bandwidth Monitor
Containment: Identify... 
- ...what damage has already been done, what more is at risk and in what time frame
- ...what countermeasures are available and how much do they cost/have consequences
- ...what actions will alert the attacker that they have been detected and what evidence needs to be gathered before they can wipe their tracks
Generally containment revolves around isolation of affected components - the key is to balance containment with the ability to analyze the attack since once the attacker realizes they are being isolated they will eject to preserve their secret methods.
- Infected LANs could be rerouted such that no outwards traffic is permitted (black hole)
- Accounts for infected devices can be downgraded for the duration of the attack to prevent unauthorized access
- Variation on isolation is to segment a section of a network that contains an infected host rather than just the host itself. 
	- Becomes a honeypot or sinkhole to allow attacker to receive modified output over the attacker connection.
Eradication and recovery
1. Reconstitute/restore from backup systems
2. Reaudit existing controls - understand how the attacker got in
3. Ensure all affected parties are notified and provided with the tools to fix their own systems
- Consider changing firewall configuration after a breach to cover the path they used. Most of the time this will be a check on incoming data packets. It is important to also include outgoing checks to counter exfiltration.
	- Restrict DNS to known servers or authorized servers
	- Block known "bad" ranges and IP addresses that are not authorized for that network segment.
	- Firewall config makes Data Loss Prevention, Device Management easier
		- Tying access to certificate allows for central control to revoke or update access
- Don't forget to apply security to endpoints - the weakest point in any security chain is the human element
	- Social Engineering
	- Vulnerabilities in configurations
	- Lack of security controls/automated security systems
	- Configuration drift/out of date
	- Weak security configurations
- Combining everything together gets Security Orchestration, Automation and Response (SOAR), typically implemented with a SIEM like Splunk but can be a standalone system,. The goal is to reduce the Mean Time to Respond (MTtR).
	- AI is being used to detect behavior that should trigger a SOAR response. Attacker AI that attempts to work around the detection patterns is adversarial AI. Attacker AI may attempt to add noise to behavior to hide hostile activity against defender systems that rely on known attack patterns.