# Installation Guide

## Prerequisites

- VirtualBox installed
- Windows 11 ISO
- Kali Linux ISO
- Splunk Enterprise (free trial)
- Splunk Universal Forwarder
- sysmon & sysmonconfig-export.xml - Downloaded on the windows 11 VM

## Step 1: VM Setup

### Windows 11 VM
1. Create new VM in VirtualBox
2. Allocate 6 GB RAM, 3 CPU cores
3. Network: Bridged Adapter
4. Install Windows 11

### Kali Linux VM
1. Create new VM
2. Allocate 2.5 GB RAM, 2 CPU cores
3. Network: Bridged Adapter
4. Install Kali Linux

## Step 2: Splunk Installation

### On Host Machine
1. Download Splunk Enterprise
2. Install to - C:\Program Files\Splunk
3. Access web interface: http://localhost:8000
4. Set admin credentials (username & password)

### On Windows VM
1. Download Splunk Universal Forwarder
2. During installation:
   - Receiving Indexer: 192.168.1.50:9997
   - Set admin credentials (username & password)

## Step 3: Sysmon Installation

On Windows VM:
- CMD (admin): **sysmon64.exe -accepteula -i sysmonconfig-export.xml**

---

**Next:** [Configuration Guide](./03-Configuration.md)
