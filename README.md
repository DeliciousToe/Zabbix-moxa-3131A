    Zapytanie zostało przetworzone

MOXA AWK-3131A by SNMP - Zabbix Template

This repository contains a Zabbix template for monitoring MOXA AWK-3131A devices via SNMP. This template provides comprehensive monitoring of various system parameters and network interface statistics, including detailed packet and traffic information.

Features:

- System Information Monitoring: Gathers essential device information like system contact, description, name, location, object ID, and uptime.
- Network Interface Discovery: Automatically discovers network interfaces on the MOXA AWK-3131A device.
- Detailed Network Interface Statistics: Monitors inbound and outbound traffic, unicast, multicast, and broadcast packets, errors, and discards for each discovered interface.
- Interface Status Monitoring: Tracks the administrative and operational status of network interfaces.
- Interface Speed Monitoring: Monitors the current bandwidth of each interface.
- Pre-processing: Uses Zabbix pre-processing steps for accurate data representation (e.g., converting centiseconds to uptime, calculating change per second for rates).
- Configurable Triggers: Provides out-of-the-box triggers for critical events like interface going down, high packet error/discard rates, and low interface speed.
- Visualizations: Includes graph prototypes for network traffic, packet rates, and errors/discards.

Requirements:

- Zabbix Server (version 7.0 or higher recommended)
- MOXA AWK-3131A device with SNMP agent enabled.
- SNMP community string configured on the MOXA device and accessible from the Zabbix server.

Installation:

Download the Template: Download the MOXA AWK-3131A by SNMP.xml file from this repository.

Import into Zabbix:

  - Navigate to Configuration -> Templates in your Zabbix frontend.
  - Click Import in the top right corner.
  - Click Browse and select the MOXA AWK-3131A by SNMP.xml file.
  - Click Import.

Link to Host:

  - Go to Configuration -> Hosts.
  - Select the MOXA AWK-3131A host you wish to monitor, or create a new host.
  - Go to the Templates tab.
  - In the Link new templates section, search for MOXA AWK-3131A by SNMP and select it.
  - Click Add, then click Update on the host configuration page.

Configure SNMP on Host:

  - Ensure the host's SNMP interface is correctly configured (IP address and SNMP community string).
  - If using SNMPv3, configure the credentials accordingly on the host.

Monitored Items:
The template includes the following items for monitoring,

System Information:

  - Number of network interfaces: snmp.get[ifNumber.0]

  - System Contact: snmp.get[sysContact.0]

  - Device description: snmp.get[sysDescr.0]

  - System Location: snmp.get[sysLocation.0]

  - Device name: snmp.get[sysName.0]

  - System Object ID: snmp.get[sysObjectID.0]

  - System OID Last Change: snmp.get[sysORLastChange.0] (converted to uptime)

  - System Services: snmp.get[sysServices.0]

  - Device uptime: snmp.get[sysUpTimeInstance] (converted to uptime)


Network Interface Discovery (via Low-Level Discovery),
For each discovered network interface, the following items are created:

  - Interface {#IFNAME}({#IFALIAS}): Admin status: net.if.admin.status[ifAdminStatus.{#SNMPINDEX}]

  - Interface {#IFNAME}({#IFALIAS}): Inbound broadcast packets: net.if.in.bcast[ifHCInBroadcastPkts.{#SNMPINDEX}] (packets per second)

  - Interface {#IFNAME}({#IFALIAS}): Inbound discards: net.if.in.discards[ifInDiscards.{#SNMPINDEX}] (discards per second)

  - Interface {#IFNAME}({#IFALIAS}): Inbound errors: net.if.in.errors[ifInErrors.{#SNMPINDEX}] (errors per second)

  - Interface {#IFNAME}({#IFALIAS}): Inbound multicast packets: net.if.in.mcast[ifHCInMulticastPkts.{#SNMPINDEX}] (packets per second)

  - Interface {#IFNAME}({#IFALIAS}): Inbound unicast packets: net.if.in.ucast[ifHCInUcastPkts.{#SNMPINDEX}] (packets per second)

  - Interface {#IFNAME}({#IFALIAS}): Inbound traffic: net.if.in[ifHCInOctets.{#SNMPINDEX}] (bytes per second)

  - Interface {#IFNAME}({#IFALIAS}): Last change: net.if.lastchange[ifLastChange.{#SNMPINDEX}] (converted to uptime)

  - Interface {#IFNAME}({#IFALIAS}): MTU: net.if.mtu[ifMtu.{#SNMPINDEX}] (bytes)

  - Interface {#IFNAME}({#IFALIAS}): Outbound broadcast packets: net.if.out.bcast[ifHCOutBroadcastPkts.{#SNMPINDEX}] (packets per second)

  - Interface {#IFNAME}({#IFALIAS}): Outbound discards: net.if.out.discards[ifOutDiscards.{#SNMPINDEX}] (discards per second)

  - Interface {#IFNAME}({#IFALIAS}): Outbound errors: net.if.out.errors[ifOutErrors.{#SNMPINDEX}] (errors per second)

  - Interface {#IFNAME}({#IFALIAS}): Outbound multicast packets: net.if.out.mcast[ifHCOutMulticastPkts.{#SNMPINDEX}] (packets per second)

  - Interface {#IFNAME}({#IFALIAS}): Outbound unicast packets: net.if.out.ucast[ifHCOutUcastPkts.{#SNMPINDEX}] (packets per second)

  - Interface {#IFNAME}({#IFALIAS}): Outbound traffic: net.if.out[ifHCOutOctets.{#SNMPINDEX}] (bytes per second)

  - Interface {#IFNAME}({#IFALIAS}): Physical address: net.if.physaddr[ifPhysAddress.{#SNMPINDEX}]

  - Interface {#IFNAME}({#IFALIAS}): Speed: net.if.speed[ifSpeed.{#SNMPINDEX}] (bits per second)

  - Interface {#IFNAME}({#IFALIAS}): Operational status: net.if.status[ifOperStatus.{#SNMPINDEX}]

  - Interface {#IFNAME}({#IFALIAS}): Type: net.if.type[ifType.{#SNMPINDEX}]

Triggers:
The template includes the following triggers,

System Triggers:

  - System Contact is not set on {HOST.NAME}: Triggers if sysContact.0 is empty or not available for 1 hour (WARNING).

  - System Location is not set on {HOST.NAME}: Triggers if sysLocation.0 is empty or not available for 1 hour (WARNING).

  - System Object ID has changed on {HOST.NAME}: Triggers if sysObjectID.0 changes (INFO).

  - System services have changed on {HOST.NAME}: Triggers if sysServices.0 changes (INFO).

Network Interface Triggers (Prototypes)
For each discovered network interface, the following triggers are created:

  - High inbound broadcast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if inbound broadcast packets exceed 500 pps (WARNING).

  - High inbound multicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if inbound multicast packets exceed 1000 pps (WARNING).

  - High inbound unicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if inbound unicast packets exceed 10000 pps (WARNING).

  - High outbound broadcast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if outbound broadcast packets exceed 500 pps (WARNING).

  - High outbound multicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if outbound multicast packets exceed 1000 pps (WARNING).

  - High outbound unicast packet rate on interface {#IFNAME}({#IFALIAS}): Triggers if outbound unicast packets exceed 10000 pps (WARNING).

  - Interface {#IFNAME}({#IFALIAS}) is down: Triggers if the operational status of the interface is "down" (HIGH).

  - Interface {#IFNAME}({#IFALIAS}) has low speed (current: {ITEM.VALUE}): Triggers if the interface speed is less than 100 Mbps while operational (AVERAGE).

Discovery Rules:
Network interfaces discovery: This rule uses SNMP to discover network interfaces and create associated items, triggers, and graphs.

  SNMP OID: discovery[{#SNMP_OID},1.3.6.1.2.1.2.2.1.2,{#IFALIAS},1.3.6.1.2.1.31.1.1.1.18,{#IFNAME},1.3.6.1.2.1.31.1.1.1.1,{#IFDESCR},1.3.6.1.2.1.2.2.1.2,{#IFTYPE},1.3.6.1.2.1.2.2.1.3,{#IFSPEED},1.3.6.1.2.1.2.2.1.5,{#IFOPERSTATUS},1.3.6.1.2.1.2.2.1.8,{#IFADMINSTATUS},1.3.6.1.2.1.2.2.1.7]
  Key: net.if.discovery
  Delay: 1 hour

Graphs:
The template includes graph prototypes for discovered network interfaces:

  - Interface {#IFNAME}({#IFALIAS}): Broadcast packets: Visualizes inbound and outbound broadcast packets.

  - Interface {#IFNAME}({#IFALIAS}): Errors and discards: Visualizes inbound and outbound errors and discards.

  - Interface {#IFNAME}({#IFALIAS}): Network traffic: Visualizes inbound and outbound network traffic in Bps.

  - Interface {#IFNAME}({#IFALIAS}): Speed: Visualizes the interface speed in bps.

  - Interface {#IFNAME}({#IFALIAS}): Unicast packets: Visualizes inbound and outbound unicast packets.

Value Maps:
The template utilizes the following value maps for better readability of SNMP integer values:

  SNMP interface status (ifAdminStatus): Maps numerical administrative status to "up", "down", "testing".

  SNMP interface status (ifOperStatus): Maps numerical operational status to "up", "down", "testing", "unknown", "dormant", "notPresent", "lowerLayerDown".

  SNMP interface type (ifType): Maps numerical interface types to "other", "ethernetCsmacd", "loopback", "ieee80211".
