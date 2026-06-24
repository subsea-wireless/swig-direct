# swig-direct user stories

**Felix / Hydromea**
Here are some user stories on SWiGdirect, from the perspective of LUMA users (based on our understanding what our customers need to do):

Initial setup:
- (ethernet device) Use OEM-provided config app to connect to the device for the first time (either to a pre-defined fixed IP initially, or it needs a workable way for IP discovery). The app will query the device for its name, internal serial number,  firmware version, etc. and will request the currently set values of all parameters, to update the GUI fields accordingly.
- (serial device): as above, but no need for IP discovery, the device is plugged into a serial COM port
- User uses OEM config app to configure the device parameters (e.g. TX power level, bitrate, IP address, gateway, netmask, etc). Generally, new parameter values have immediate effect - except for network/IP settings, and RS232/RS485 mode setting, which will only be applied at after a specific "apply" command is sent, to avoid getting locked out. Parameters are only applied to volatile memory initially (to be able to test, and revert by power-cycling if there is a problem). At the end, the user clicks a button "Save to flash memory", which will send a command to the device to commit the settings to non-volatile flash memory. 
- user uses the OEM config app to monitor telemetry (power consumption, temperature, packet loss statistics, etc.). Values are 'live'  and periodically updated.

Integration: 
- user integrates the SWiGdirect API into their own embedded device, to allow their device to configure and monitor the SWiG device. The connection between the user's device and SWiG device is typically short and direct, e.g. direct RS232 or RS485 connection, or local ethernet on the same local network switch.
- user integrates the SWiGdirect API into their topside control software, to configure and monitor multiple SWiG devices during operation. Connection to the SWiG device may be longer, e.g. via RS232/485 to a TCP-to-serial converter and ethernet network, or ethernet to a subsea switch, via potentially VLANs, firewalls, VPN tunnels, NATs, etc. to the corporate network and the control center. 

Operation:
- user interacts with the customer's control software, or OEM-provided config app, with various installed SWiG devices via IP network, to change settings, monitor status, get live telemetry and packet statistics. 
- customer's subsea device (sensor, logger, ROV, AUV) connects to SWiG device via SWiGdirect protocol to get live telemetry (e.g. signal strength, packet loss statistics), and change settings (e.g. TX power level, switch between active and standby mode). 
- offshore technician temporarily connects SWiG device to their laptop for trouble-shooting and testing (similar to initial setup - changing settings, get live telemetry, via the OEM's config app). The connection may be via a ROV: often, the modem is only temporarily installed on a ROV for a specific job, the ROV may change, the modems are taken to other jobs, they may be rental units. For each job, the "topside" modem has to be mounted and plugged into the ROV, the data connection routed through the ROV system and tether to the control room, to a laptop running the monitoring software. This connection has to be tested each time, to make sure the topside laptop can "talk" to the ROV-mounted modem, and further that a wireless connection can be established to the subsea device (e.d. a gyrobox or pressure monitoring box). 



**Nigel / Imenco**
Some user stories to cover a range of usage:

A service technician connects to a deployed device. They confirm figures of merit for the communications link since the last time they were read, and optionally reset the statistics. The technician needs to understand communications parameters from the device label or vessel records. For serial connection, parameters include port type (RS232 etc) bit rate, framing information. For IP connection, parameters include IP address , UDP or TCP and port number. Also need to know authentication parameters

A remote SWiG device connects to a seabed sensor and read its value. The value will be sent periodically by a device interfacing to the sensor which uses SWiG Direct. A control system on the vessel connects to the vessel modem and periodically requests updates on error rates.

An operator wants to monitor performance of a deployed SWiG device on an autonomous tethered surface platform (e.g. autonomous surface vessel), with connection provided by geosynchronous satellite with associated latency. They would like to minimise power consumption of the SWiG device by controlling power levels, optimising the settings over time by adjusting the power level settings to balance reliability and power usage.

A SWiG modem is connected to the internet through a remote network with protection (firewall etc) designed for protecting standard modern PLCs and control system components on the remote network (which are expected to have design consistent with EU Cyber Resilience Act and similar). The owner needs to connect to it periodically while ensuring that other devices can not readily connect. Authentication / Encryption should be consistent with that provided by a typical modern PLC.

An operator connect over the internet to a SWiG Direct device over a connection established and protected by OpenVPN. The remote OpenVPN connection is provided by a device is running no SWiG specific software. Once connected, the operator has access to all SWiG Direct functionality to control and monitor the wireless device

