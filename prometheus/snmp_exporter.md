SNMP Exporter for pfSense
=========================

This guide focuses on customizing the snmp_exporter configuration for pfSense.
Prerequisites
Before starting, ensure the following:
Enable SNMP service with modules on your pfSense host.
```
Enabled modules:
MibII
PF
Host Resources
UCD
```
snmpwalk comes from the package net-snmp-utils, and it’s asking if you want to install it. You should go ahead and install it so you can run SNMP queries.
```
sudo dnf install net-snmp-utils
```
