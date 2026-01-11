# Lab Architecture

![image alt](https://github.com/ashish6t7/Enterprise-SOC-Lab/blob/ebd7366e5e6857080434943988a7d27483116866/Lab-Setup/Setup-Images/01-network-diagram.png)

## Overview

This lab simulates a basic enterprise environment with an attacker VM, victim endpoint, and SIEM for log analysis.

## Components

| Component | Role | OS/Software | IP Address |
|-----------|------|-------------|------------|
| Host Machine | Splunk SIEM | Windows 11 | 192.168.31.50 (static) |
| Windows VM | Victim Endpoint | Windows 11 | 192.168.31.52 (static)|
| Kali VM | Attacker | Kali Linux | DHCP |

## Network Topology
```
[Kali VM] ←→ [Bridged Network (Virtual Switch)] ←→ [Windows VM]
                                                        ↓
                                                   (Logs forwarded)
                                                        ↓
                                                   [Host Splunk]
```

## Data Flow

1. Windows VM generates logs (Windows Event Logs + Sysmon)
2. Splunk Universal Forwarder collects logs
3. Logs sent to Splunk on host via port 9997
4. Analyst (ME) queries logs in Splunk Web Interface

---

**Next:** [Installation Guide](./02-Installation.md)
