High Availability: Availability is typically implemented as Service Level Agreements. This is typically measured in uptime % values.
Downtimes is calculated a sum of maintenance service + unplanned outages

| Availability % | Annual Downtime (hh:mm:ss) |
| -------------- | -------------------------- |
| 99.9999        | 00:00:32                   |
| 99.999         | 00:05:15                   |
| 99.99          | 00:52:34                   |
| 99.9           | 08:45:36                   |
| 99             | 87:36:00                   |
Which means backups! And rotating which servers the users connect to while keeping data backed up for the hardware maintenance intervals. Using virtual machines and replicated data storage allow for scalability and elasticity.
- Scalability is the ability to add more resources to operate in parallel
- Elasticity is the ability to integrate new constraints or resources in real-time
Common redundancies:
- Power supplies: backup generators, uninterruptible power supplies, batteries
- Network infrastructure: multiple Network Interface Cards (teaming), load balancers, backup switches and routers
- Data Storage: Redundant Array of Independent Disks (RAID). Type of RAID refers to the fault tolerance/backup method.
	- Level 1: Mirrored data across one other disk
	- Level 5: parity stripe, data is copied across 3 or more disks with a parity/hash to check against
	- Level 6: Double parity, Level 5 with an additional parity stripe
	- Level 0: Striping without parity. Typically used for Nested RAID.
	- To support RAID systems use Multipath to pipe data to be stored into a bus that writes to multiple disks at the same time.
- Geographical/location: Data replication should be 3-2-1; 3 backups, 2 types of storage media and 1 offline and off site so that a regional disaster cannot knock out all redundancies at once.
	- Backups should replicate on a synchronized basis if possible (write at the same time to all storages). Asynchronous is a standard backup procedure (write to primary, then replicate changes to backups).
	- Backups are governed by retention policies; how long a backup is kept and what are the intervals that new backups are made
	- Backup strategies:
		- Full: record the full storage to backup. Slow to write, but fast to restore
		- Incremental: record a baseline full storage to backup, then create a backup of any new/modified files since the **LAST backup**. Fast to write new increments, but you have to restore all increments.
		- Differential: record a baseline full storage to backup, then create a backup of all new/modified files since **last FULL backup**. 
	- Augmenting backups are Snapshots. Snapshots are designed to get around the limitation that files in use cannot be backed up (ie SQL database). Snapshots are a point-in-time copy of data.
		- Snapshots are generally supported by OS systems (ie Windows Volume Shadow copy Service - VSS) and operate more or less automatically.
		- Image is a snapshot of an OS installation.
	-  Backup media varies:
		- Disk; removable hard disk volumes that can be plugged into a system. Bad at automated backup, but stable.
		- Network Attached Storage (NAS) is a standalone storage server that can be accessed by members on a network. NAS systems are always online systems
		- Tape: very high storage system, even more data dense than disks but very slow in all aspects
		- Storage Area Network (SAN), stores data based on memory blocks rather than files.
When an outage occurs systems and processing will swap to another site. Meanwhile the original site needs to be restored from backups so it can resume activity. Sites have an order of restoration, building a site back up to full capability in a manner that tests components to ensure that they are working.
1. Power delivery
2. Network routing infrastructure
3. Network security infrastructure
4. Critical Network Servers
5. Back-end and middleware applications
6. Front-end applications
7. Workstations and devices
When backing up it is important that the backup also remove artifacts from the disasters (ie malware installed backdoors). Non-persistence is the means of allowing the restoration of data from backup while preventing the persistence of artifacts.
- Revert to known state/Snapshot
- Rollback to known configuration
- Live boot from read-only memory
- Master images (ie gold copy to build from)
- Automated build from template
	- The last two points are a result of good configuration management especially - know what changes have been made, when and by who. 
		- Change Control: method of requesting and approving changes in a controlled manner. Changes may be made reactively or proactively to threats or vulnerabilities. Typically posted along side a RFC to stakeholders.
		- Change management: implementation of changes and plans for revert if an uncaught error is found or the change creates worse problems.
		- Assets, their baseline configuration, configuration management systems can be described using diagram.
		- All assets should be identifiable, follow a standard naming convention so that foreign devices will stick out immediately.
Defense needs to be in depth such that a failure in one control such as vendor, encryption method can be contained. Diversity of tools helps, as does ensuring multiple vendors, encryptions methods and other security controls. The more controls, the more an attacker has to work through.
Disruption is a proactive approach, though not an actual counter attack as those are illegal. Honeypots/nets/files are decoy entities that are designed to look vulnerable and desirable to steal. A honey- lets the attacker show their capabilities such that the defender can build against those attacks without actually being damaged. Honey- systems however still reveal some of the defender's capabilities or organization. 
- Honeypot entities are typically found in DMZ area of a network (like email servers).
- Obfuscation of data such as DNS entries, traffic, ports mimic strategies used by attackers to raise the cost of the attacker to identify and attack an actual system.