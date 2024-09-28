Forensics is the practice of collecting evidence to a standard that is accepted by the legal system. This means preservation of logs, physical evidence in a manner that shows that the item has not been tampered with.
- Chain of Custody shows that the evidence has been tracked and logged to ensure that it's integrity has not been breached and protects organizations against accusations of modification.
- The forensics report must have the following to be accepted:
	- Performed without bias, only contains conclusions that can be formed form direct analysis
	- Methods must be repeatable by third parties - scientific method applies!
	- Evidence must retain the same state after analysis - nondestructive methods only
- Forensics goes through a process to filter for relevant evidence (e-discovery). Filtering may involve the following:
	- Identification and de-duplication of meta data
	- Index for search for files relevant to the case
		- Tag data for review 
	- Show that evidence collection, distribution and analysis was done without tampering
	- Disclose evidence to the court
In addition to physical or digital evidence having video recordings, live systems and witness interviews are helpful for contextualizing a scene. Recordings of interviews may be used but may also make witnesses more skittish.
The goal is to define a time line of events to show a correlation between the accursed and the actions taken. Actions should use UTC + offset for timestamps.
Complications arise when a BYOD is in place or when devices are not standardized. Devices need to be secured in the case of an incident.
Gathering data, or data acquisition, is time sensitive as data is volatile. Eventually, the evidence is erased by system functions unless it is copied and stored in a nonvolatile storage. From the most volatile sources to the least are:
1. CPU registers and cache memory
2. RAM system memory
3. Storage drives (HDD/SSD/flash memory)
	1. Partitions and file system blocks, unallocated memory
	2. System caches/swap space
	3. Applications caches (ie browser cookies)
	4. General files
4. Logs
5. Physical configurations
6. Archival media and printed documents
Examples of Forensics software:
- EnCase Foresnic suite
- The Forensic Toolkit (FTK) - specific for Windows
- The Sleuth Kit - OSS of command line tools and libraries for disk imaging. Combines with Autopsy for GUI
- WinHex - Tool for live acquisition of memory for Windows. See `memdump` for Linux
- The Volatility Framework as a framework to analyzing system memory
Looks for the following:
- Live data captured while the host is running; live capture gathers the most evidence but is the most visible
- Crash dumps for stack traces; static  data from hosts that have shut down, crashed or become disconnected from the controller is still good but the malware might automatically attempt to remove itself.
- Hibernation Files and Page files/swap space to check for data that overflowed from the RAM
Disk Acquisition is the act of gathering data from non-volatile storage such as HDD/SSD. Disk Acquisition also captures the OS if the boot volume is included. Basically: copy the drive to a new storage for analysis so the original volume can be used as evidence.
- Live acquisition shows the state at time of access because the host is still running
- Static acquisition shows the state at time that the host is disconnected
	- Pulling the plug shows state after disconnecting main power but risks corrupting the data
- In all cases data needs to be non-repudiable:
	- Hash of the data using MD5 of SHA to be used as a checksum
	- Bit-for-bit copy using a imaging utility (ie `dd` or `dcfldd` imaging commands on Linux)
	- Second hash of the copied data
	- A third copy of the data for actual analysis
	- Chain of custody showing that the evidence is stored in a secure, environmentally controlled facility to avoid corruption.
Most other non-disk copy evidence is a result of network traffic logs or recovered data from caches and artifacts. Artifacts are any data type not part of the main data structures (ie Caches, data fragments, firmware). 
Reconstruction of fragment data is known as carving.
Cloud infrastructure is by it's nature destroyed and recreated repeatedly, destroying evidence if it isn't logged. Cloud data is also subject to laws that the provider is basing the servers in.