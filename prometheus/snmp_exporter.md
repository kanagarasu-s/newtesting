## SNMP Exporter for pfSense

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
## Install snmpwalk package:

snmpwalk comes from the package net-snmp-utils, and it’s asking if you want to install it. You should go ahead and install it so you can run SNMP queries.
```
sudo dnf install net-snmp-utils
```
## Test SNMP access:

```
snmpwalk -v2c -c public 192.168.130.254 1.3.6.1.2.1.1.1.0
```
## Download pfSense MIBs (SSH login must be enabled temporarily):
```
mkdir -p pfmibs
scp admin@192.168.130.254:/usr/share/snmp/mibs/* /usr/share/snmp/pfmibs
```
