Social Engineering and Malware
- Social Engineering uses
	- Familiarity/Persuasion - present request as normal
	- Consensus/Social Proof - present pressure against refusal
	- Authority/Intimidation - 
	- Scarcity/Urgency
- Basically a con-artist/impersonation/imposter game
- Can also get information by using unsecured disposal or following an actually authorized person through the door.
	- Dumpster Diving
	- Tailgating
	- Shoulder Surfing
- Impersonation
	- Phishing
		- Spear Phishing - target based on trait (ie "urgent for X job title")
		- Whaling
	- Vishing
	- Smishing
- Hoaxes were a common attempt to use Urgency
- Credential harvesting - tricking users to input credentials
	- Pharming - redirect user to a compromised/fake page by corrupting routing/DNS lookup
	- Typosquatting - make a fake version that has a typo in the domain
	- Watering hole - attack a commonly used third-party site
- Influence campaign - smears, propaganda, fake news, deepfakes
<h2>Viruses</h2>
- Replicates via file/infector that is on a remote system
- Parasites off local memory and is accessed on boot
- typically uses local script-friendly applications (JVM, PDFs, MS docs etc)
<h3>Worms</h3>
- Replicates from local memory into other devices
- Consumes network bandwidth to replicate
- Typically attempts to achieve persistence to allow repeated attacks or access after reboot
<h2>Potentially Unwanted Programs (PUPS)</h2>
Unwanted/intrusive software that doesn't usually attempt to replicate
<h3>Spyware/Keyloggers</h3>
- Track user activities, does not replicate
- Typically stores data by accessing peripherals or listening for actions for transmission at a later time.
- Adware also follows under these sorts of files
<h3>Trojans</h3>
- Typically backdoors (remote access trojans)
- Can also be used to make botnets or other system to act as slave system for a command and control systems using covert channels.
<h3>Rootkits</h3>
- malware that executes with system privileges.
- most systems attempt to prevent misuse of kernel processes
- can hide inside peripheral storage
<h3>Ransomware, cryptojackers</h3>
- Ransomware: Software that extorts money by encrypting or otherwise locking out computers and then demanding money for return
- Cryptojackers: install a cryptominer on a software to generate wholely or in part cryptocurrency
<h1>Signs of Compromise</h1>
- Antivirus notification trigers
- Sandbox executions/run the code in a sandbox or other contained system to check
- Excessive resource consumption
- Changes in file systems