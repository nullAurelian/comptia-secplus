Physical security follows network security concepts, but in the physical space where the communication packets may be people or machines.
- Locate secure or sensitive zones behind security, as deep into the building as possible to give the most time for an attacker to be detected (defense in depth).
- Use a zone on the outer area of the building to act as a accessible demilitarized zone (reception)
- Place warnings of penalties for unauthorized access of premises (MOTD warnings)
- Entry zones to secure locations should be discrete to allow other noncritical zones to act as honeypots
- Minimize inter-zonal traffic so that unusual activity can be detected, ensure that traffic paths are monitored
- Minimize windows into secure zones
Physical access to secure areas should have some form of lock on them.
- Mechanical locks are the cheapest option
- Electronic locks can use multiple identification methods
	- keycode/keycard/proximity reader
	- biometric
- Physical access ideally only allows one person to enter a doorway at a time
- Physical access to moving devices can be secured using a cable to secure to a rack or other permanent fixture
- Physical access key are still vulnerable to being duplicated, spoofed or stolen
	- Cloning an existing card with no other safeguards such as MFA
	- Skimming/capturing an existing card's data that lacks other safeguards
	- Man-in-the-Middle attack via cable connection such as USB
Make sure that entrances and egresses are monitored with some form of sensor or alarm.
Security and reception personnel should be able to monitor common entrances and egresses from their position, either directly or via CCTV. Visitors without badges or who are moving around without escort should be challenged for authorization. Visitors in general should be logged.
Consider airgapping physical access to devices with an interior enclosure. Direct cables should be monitored, either for a tap or for a cut.
Ensure that the physical devices are kept in an environmentally controlled room (like data storage). 
- Typical A/C for data is set to 20C and 50% humidity with positive air pressure (overpressure)
- Cabling in a server room should be kept insulated from EM interference coming from electrical fixtures like lights. Typically this is below the floor.
- Fire suppression should be kept up to code, with well marked fire exits and smoke detection. Sprinklers may also be used but be aware of what type of suppressant they use or you might damage servers.
	- Dry-pipe: water-based but water is not pushed into the sprinkler until the alarm is triggered
	- Pre-action: water based, pipes fill when alarm is triggered and sprays when heat rises
	- Halon: gas based system, but no longer up to code
	- Clean agent: Gas but environmentally cleaner than Halon. Typical examples include INERGEN (CO2+ Argon + Nitrogen), FM-200/HFC-227 or FE-13. Works by depleting oxygen.
Data destruction needs to be secure. Sanitation of media refers to removal of data from storage medium before the devices are disposed or repurposed. This includes not only memory but also paper records.
- Burning
- Shredding/pulping
- Pulverizing
- Degaussing (apply magnet to disk)
Are all acceptable methods of disposal. 
Specifically for digital storage there are more options such as:
- Overwriting: writing randomized junk data over the portion to be sanitized. This might take one or more passes of overwriting to be properly sanitized.
	- 0 filling: sets all bits in the memory to 0
	- Secure Erase command provided by SATA and SAS. Sets the memory blocks to "empty" so the OS garbage collector will delete the data over time. This is however not telegraphed and the data might be accessed before it is entirely deleted.
	- Self encrypting drives may use an Instant Secure Erase by encrypting the drive using a key and then deleting the key before setting the data to be collected by the garbage collector.