# Lab Architecture

![Network Diagram](https://github.com/ashish6t7/Enterprise-SOC-Lab/blob/ebd7366e5e6857080434943988a7d27483116866/Lab-Setup/Setup-Images/01-network-diagram.png)

---

## Overview

This lab simulates a basic enterprise environment with an attacker VM, victim endpoint, and SIEM for centralized log analysis.

---

## Components

| Component | Role | OS/Software | IP Address |
|-----------|------|-------------|------------|
| Host Machine | Splunk SIEM | Windows 11 | 192.168.31.50 (static) |
| Windows VM | Victim Endpoint | Windows 11 | 192.168.31.52 (static) |
| Kali VM | Attacker | Kali Linux | DHCP |

![VirtualBox VM Manager - All Components](./Setup-Images/virtualbox-vms.png)

---

## Network Configuration

**All VMs use Bridged Networking:**
- Allows direct communication between VMs and host
- VMs receive IP addresses from local router (same subnet as host)
- Simulates real enterprise network connectivity

![Network Adapter Configuration](./Setup-Images/Windows11-bridged-networking.png)

---

## Network Topology
```
[Kali VM] ←→ [Bridged Network (Virtual Switch)] ←→ [Windows VM]
                                                        ↓
                                                   (Logs forwarded
                                                    via port 9997)
                                                        ↓
                                                   [Host Splunk]
```

---

## Data Flow

1. **Windows VM generates logs:**
   - Windows Event Logs (Security, System, Application)
   - Sysmon logs (Process creation, Network connections)

2. **Splunk Universal Forwarder collects logs:**
   - Reads Event Viewer logs via WMI (Windows Management Instrumentation)
   - Reads Sysmon logs from Event Viewer

3. **Logs forwarded to Splunk:**
   - Protocol: TCP
   - Port: 9997
   - Destination: 192.168.31.50 (Host)

4. **Analyst queries logs:**
   - Splunk Web Interface: http://localhost:8000
   - Index: `windows`

---

**Next:** [Installation Guide](./02-Installation.md)
