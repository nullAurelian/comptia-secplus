Mobile devices have become more powerful and have thus become targets for attack. People also need these devices to do work.
<h2>Mobile Device Policy</h2>
Where users source their mobile devices for work can be a company policy.
- **Bring Your Own Device**: Employees provide their own devices. Employee devices should meet the requirements of the company according to any policies and agreements, but it will be harder to enforce and secure.
- **Corporate Owned, Business Only**: Devices are provided by the company solely for company purposes.
- **Corporate owned, personally-enabled**: Device is provided and owned by the company, but the user may use it for email and other matters as long as it is within the acceptable use guidelines.
- **Choose Your Own Device**: Device is chosen from a list of models but otherwise the same policy of Corporate Owned, Personally Enabled.
- All these may be used with Virtual Desktops or other image systems to allow quick standup and reimaging for new users. Other cases may be remote desktop to allow for thinner devices via hypervisors over a VPN. This also enables BYOD to be more secure by using a Virtual Desktop client to mechanically segregate business use.
- Another solution may be Enterprise Mobility Management, a type of management software to apply security policies to mobile devices and apps. It is basically an agent that is installed to the device.
	- Mobile Device Management: sets device policies, enables remote resets and wipes
	- Mobile Application Management: sets Application policies, prevents data transfer to personal apps
	- Containerization allows the admin to manage and maintain the portion of a device that connects to the secure network. Isolate apps that need the secure network from ones that don't.
Mobile OS have their own considerations for apps and app security.
- iOS is relatively closed off and limited to iphones. Less wiggle room for devices but potentially more secure.
- Android has a wider scope for possible hardware configurations. More options, but less consistent in quality. Android version 4.3 onwards are based off Security-Enhanced Linux.
- Consider having a method of remote wipe and that data at rest in the device or on external medial has full encryption.
	- In addition to remote wipe, having some form of location services or geolocation tracking to check for potentially anomalous location contexts. Consider restricting access to features based on location (geofencing).
- Be aware of rooting or jailbreaking of devices - accessing a device's (normally) locked root features to bypass security or other restrictions. Methods of doing so are typically not signed. Containerization can help protect sensitive applications from being made vulnerable by the root/jailbreak process.
Mobile devices have their own networks and considerations:
- Typically mobile devices will need to connect to a cellular network or GPS. However cell networks may run into deadzones or be blocked by terrain, while GPS may be jammed in certain rare circumstances.
- Mobile devices typically default to WiFi if possible. This behavior has the usual caveats of public networks, evil twins or other WiFi network attacks.
	- In addition Mobile devices will have their own networks for equipment that is paired to the device (ie Wireless mice or keyboards). The network of items paired to a mobile device is a Personal Area Network (PAN). These should be disabled typically.
	- Mobile devices can act as Wifi access points for each other. This is known as an ad-hoc network, or hotspot or tethering. These connections may bypass network security such as web content filtering or traffic monitoring.
	- Commonly used PAN protocols may have known issues:
		- Bluetooth has vulnerabilities related to it's confidentiality of devices, integrity of connections. 
		- Bluejacking: spam where unsolicited messages are sent and used as a vector for malware
		- Bluesnarfing: exploit to bypass authentication for bluetooth devices to steal information.
-  RFID and Infrared transmission is the encoding and transmission of data via passive tags.
- Near-Field Communication (NFC) is typically used for contactless payments but doesn't provide native encryption of communication.
- SMS/MMS/RCS are message services operated by cell network providers that allow transmission of data.
- Mobile devices may also use microwave radio connections for point-to-point or point-to-multipoint communication.
