# UTM + Windows 11 ARM Setup Guide (Apple Silicon Mac)

This guide explains how to install **Windows 11 ARM** on an Apple Silicon Mac using **UTM**, and prepare the environment for **SAP GUI** (for ABAP programming courses).  

---

## Table of Contents
1. [Requirements](#requirements)  
2. [Install UTM](#1-install-utm)  
3. [Create a New Virtual Machine](#2-create-a-new-virtual-machine)  
4. [Download Windows 11 ARM ISO](#3-get-windows-11-arm-image)  
5. [Configure VM](#4-configure-the-vm)  
6. [Install Windows](#5-install-windows)  
7. [First Boot Troubleshooting](#6-first-boot--troubleshooting)  
8. [Guest Tools](#7-guest-tools)  
9. [Activation](#8-activation)
10. [Networking Issues](#9-networking-issues)
11. [Next Steps: SAP GUI](#10-next-steps-sap-gui)

---

## Requirements
- Apple Silicon Mac (M1/M2/M3)  
- At least **8 GB RAM** (16 GB recommended)  
- At least **64 GB disk space**  
- UTM app (free, open-source)  
- Stable internet connection (for Windows ISO + SAP GUI downloads)  

---

## 1. Install UTM
- Download: [https://mac.getutm.app](https://mac.getutm.app)  
- Install: open `.dmg`, drag **UTM.app** into Applications.  
- Launch UTM.  


## 2. Create a New Virtual Machine
1. Open UTM → click **Create a New Virtual Machine**.  
2. Choose **Virtualize → Windows**.  
   ⚠️ Do **NOT** choose *Emulate* (too slow).  


## 3. Get Windows 11 ARM Image
- On the ISO setup screen → click **Get Latest Windows 11 for ARM**.  
- UTM will redirect you to **CrystalFetch**, a helper tool that connects to Microsoft’s official servers.  
- Choose your preferred language.  
- Confirm the download. CrystalFetch will generate and fetch the official Windows 11 ARM ISO.  
- Once the download is finished, return to UTM and select the ISO file to continue.   


## 4. Configure the VM
Recommended settings:  
- **CPU**: 4 cores  
- **Memory**: 8192 MB (8 GB, min 4 GB)  
- **Disk**: 64–100 GB (dynamic)  
- Check *Install drivers and SPICE tools* (for display/mouse integration) 


## 5. Install Windows
1. Start the VM → installer will boot.  
2. Product Key: select **“I don’t have a product key”** (or enter if you have one).  
3. Edition: select **Windows 11 Pro** (best features/compatibility).  
4. Disk: choose **Drive 0 Unallocated Space → Next**.  
5. Windows copies files, restarts automatically → proceed with region, keyboard, account.  


## 6. First Boot & Troubleshooting

### Case 1: Stuck at “Start boot option” / `startup.nsh`
- Reason: VM boots from ISO instead of installed disk.  
- Fix: Shut down → Go to Settings → **CD/DVD → remove Windows ISO** (keep only `utm-guest-tools.iso`) → restart.  


### Case 2: Message “It looks like you started an upgrade…”
- Reason: VM still booted from ISO.  
- Fix: Same as case 1. 


### Case 3: Windows desktop loads, activation fails  
- Message: *“Cannot connect to my organisation's activation server.”*  
- Fix: Ignore activation. Windows works fine except:  
  - Watermark “Activate Windows”  
  - No personalization (wallpapers/themes)  
- All SAP functions work without activation.  


## 7. Guest Tools
- If *Install drivers and SPICE tools* was checked, features like auto-resize and mouse integration should already work.
- If not → open `utm-guest-tools.iso` inside Windows and install manually.  


## 8. Activation
- Optional. Not required for SAP.  
- If provided by university:  
  `Settings → System → Activation → Change product key`  


## 9. Networking Issues

Some users may encounter **“No Internet”** inside Windows after installation.
Here are the known solutions (from easiest → advanced):

### Case 1: No Network During Windows Setup

* At the **language selection screen** → press **Shift + F10** to open Command Prompt.
* Enter one of the following (depends on Windows version):

  * `OOBE\BYPASSNRO` → VM will reboot, then you will see *“I don’t have internet”*.
  * or `start ms-cxh:localonly` → skips internet requirement, lets you create a **local account**.
* After installation, install **SPICE Guest Tools** to enable drivers (including network).

### Case 2: No Internet After Windows Desktop Loads

#### Solution 1: Install SPICE Guest Tools

* Make sure **SPICE Guest Tools (utm-guest-tools.iso)** is installed.
* Provides the **Red Hat VirtIO Ethernet Adapter** driver.
* Check in **Device Manager → Network Adapters**:

  * ✅ If you see *Red Hat VirtIO Ethernet Adapter* → driver is installed.
  * ⚠️ If you only see *Unknown Device* (yellow mark) → reinstall Guest Tools manually.

#### Solution 2: Bridged Network Mode (Most Reliable in My Case)

* On your Mac Terminal → run `ifconfig` to find the correct interface (normally `en0` = Wi-Fi).
* In UTM:

  1. Shut down VM.
  2. Go to **UTM → VM → Edit → Network**.
  3. Change **Network Mode** → `Bridged (Advanced)`.
  4. Under *Bridged Interface*, select the interface you found (e.g. `en0`).
  5. Keep **Emulated Network Card = virtio-net-pci**.
* Start VM → open **cmd** → run `ipconfig`.

  * If your VM gets an IP in the same subnet as your Mac (e.g. Mac `192.168.0.12`, VM `192.168.0.20`), networking works (Tip: Both your Mac and VM should share the same subnet — usually the first three parts of the IP, e.g. 192.168.0.xxx.if you don't know how to calculate IP address and subnet just ask master ChatGPT).

#### Solution 3: Change Emulated Network Card (This May Fail)

* Shut down VM → UTM **Settings → Network**.
* Change **Emulated Network Card**: `virtio-net-pci` → `Intel e1000`.
* Windows 11 has built-in Intel e1000 drivers, so it should connect immediately.
* ⚠️ In my case this causes *“Your PC did not start correctly”* → use carefully!

#### Testing Network Inside VM

* Open **Command Prompt** in Windows and test:

  * Ping Internet:

    ```bash
    ping 8.8.8.8
    ```

    If replies succeed → internet works.
  * Test DNS:

    ```bash
    nslookup www.google.com 8.8.8.8
    ```

    If DNS fails but ping works → change DNS:
    `Settings → Network & Internet → Ethernet → Edit DNS` → set manual Preferred DNS: 8.8.8.8 and Alternate DNS: 1.1.1.1.

    If both ping and DNS succeed, your VM networking is fully functional.


## 10. Next Steps: SAP GUI

1. Inside Windows VM → install your university VPN client.
2. Connect VPN → ensures access to campus SAP servers.
3. Download and install **SAP GUI for Windows** (from your university IT portal).
4. Configure SAP connection settings → log in → start ABAP programming.

---

*Maintained by students of Augsburg University of Applied Sciences – 2025*  
