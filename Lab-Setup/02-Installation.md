# Installation Guide

## Prerequisites

**Software Downloads:**
- VirtualBox (installed)
- Windows 11 ISO
- Kali Linux ISO
- [Splunk Enterprise (Free Trial)](https://www.splunk.com/en_us/download.html)
- [Splunk Universal Forwarder](https://www.splunk.com/en_us/download/universal-forwarder.html)
- [Sysmon](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon)
- [Sysmon Config (SwiftOnSecurity)](https://github.com/SwiftOnSecurity/sysmon-config)

---

## Step 1: Virtual Machine Setup

### Windows 11 VM

**VM Configuration:**
1. Create new VM in VirtualBox
2. Allocate **6 GB RAM**, **3 CPU cores**
3. Network Adapter: **Bridged Adapter**
4. Install Windows 11 from ISO

**Set Static IP:**
- Open Network Settings → Change adapter options
- IPv4 Properties → Manual IP: `192.168.31.52`

### Kali Linux VM

**VM Configuration:**
1. Create new VM in VirtualBox
2. Allocate **2.5 GB RAM**, **2 CPU cores**
3. Network Adapter: **Bridged Adapter**
4. Install Kali Linux from ISO

**IP Configuration:**
- Use DHCP (automatic)

---

## Step 2: Splunk Installation

### On Host Machine (Windows 11)

1. **Download Splunk Enterprise** (free trial, 60-day license)

2. **Install:**
   - Installation path: `C:\Program Files\Splunk`
   - Accept license agreement

3. **First-time setup:**
   - Access: http://localhost:8000
   - Create admin username and password
   - Complete setup wizard

![Splunk Enterprise Web Interface]([./Setup-Images/Splunk web interface.png](https://github.com/ashish6t7/Enterprise-SOC-Lab/blob/fd88614796fdc55fce3929485c3330d154f53cb9/Lab-Setup/Setup-Images/Splunk%20web%20interface.png))

---

### On Windows VM

1. **Download Splunk Universal Forwarder**

2. **Install with configuration:**
   - During installation, when prompted:
   - **Receiving Indexer:** `192.168.31.50:9997`
   - Set admin username and password

![Universal Forwarder Installation - Receiving Indexer](./Setup-Images/forwarder-installation-indexer.png)

**This configures the forwarder to send logs to your host Splunk instance.**

---

## Step 3: Sysmon Installation

**On Windows VM:**

1. Download Sysmon and SwiftOnSecurity config to `C:\Tools\`

2. **Open CMD as Administrator:**
```cmd
cd C:\Tools
sysmon64.exe -accepteula -i sysmonconfig-export.xml
```

3. **Verify installation:**
```cmd
sc query Sysmon64
```

**Expected output:** `STATE: RUNNING`

![Sysmon Service Running](./Setup-Images/sysmon-service-running.png)

---

## Installation Complete

**What you now have:**
- ✅ Host with Splunk Enterprise installed
- ✅ Windows VM with Universal Forwarder installed
- ✅ Windows VM with Sysmon monitoring installed
- ✅ Kali VM for attack simulation (optional)

---

**Next:** [Configuration Guide](./03-Configuration.md) to set up log forwarding and start collecting data.
