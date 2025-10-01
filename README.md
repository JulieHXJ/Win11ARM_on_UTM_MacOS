# 🚀 UTM + Windows 11 ARM + SAP Setup Guide (Apple Silicon Macs)

This guide explains how to:  
1. Install **Windows 11 ARM** on Apple Silicon Macs using **UTM**.  
2. Set up **VPN and SAP GUI** in Windows to prepare for ABAP programming courses.  

It is based on real installation experiences of students at Augsburg University of Applied Sciences (2025).  

---

## 📑 Table of Contents
1. [Part 1: Install Windows 11 ARM on UTM](#part-1-install-windows-11-arm-on-utm)  
   - [1. Install UTM](#1-install-utm)  
   - [2. Create a New Virtual Machine](#2-create-a-new-virtual-machine)  
   - [3. Get Windows 11 ARM Image](#3-get-windows-11-arm-image)  
   - [4. Configure the VM](#4-configure-the-vm)  
   - [5. Install Windows](#5-install-windows)  
   - [6. First Boot & Troubleshooting](#6-first-boot--troubleshooting)  
   - [7. Guest Tools](#7-guest-tools)  
   - [8. Activation](#8-activation)  
2. [Part 2: SAP Environment Setup](#part-2-sap-environment-setup)  
   - [1. Install VPN](#1-install-vpn)  
   - [2. Install SAP GUI](#2-install-sap-gui)  
   - [3. Configure SAP Connection](#3-configure-sap-connection)  
   - [4. Test Login](#4-test-login)  
   - [5. Tips & Troubleshooting](#tips--troubleshooting)  

---

# Part 1: Install Windows 11 ARM on UTM

## 1. Install UTM
- Download: 👉 [https://mac.getutm.app](https://mac.getutm.app)  
- Install: open `.dmg`, drag **UTM.app** to Applications.  

---

## 2. Create a New Virtual Machine
1. Open UTM → click **Create a New Virtual Machine**.  
2. Choose **Virtualize → Windows**.  
   ⚠️ Do **not** choose *Emulate*.  

---

## 3. Get Windows 11 ARM Image
- On ISO setup screen → click **Get → Latest Windows 11 for ARM**.  
- Select language (e.g. English International) → download.  

---

## 4. Configure the VM
Recommended settings:  
- **CPU**: 4 cores  
- **Memory**: 8192 MB (8 GB, min 4 GB)  
- **Disk**: 64–100 GB (dynamic)  
- ✅ Check *Install drivers and SPICE tools*  

---

## 5. Install Windows
1. Start the VM → installer will boot.  
2. Product Key: select **“I don’t have a product key”** (or enter if you have one).  
3. Edition: select **Windows 11 Pro**.  
4. Disk: choose **Drive 0 Unallocated Space → Next**.  
5. Windows will copy files and restart → proceed with region, keyboard, account.  

---

## 6. First Boot & Troubleshooting

### Case 1: Stuck at “Start boot option” / `startup.nsh`
- Reason: VM boots from ISO instead of installed disk.  
- Fix: Shut down → UTM Settings → **CD/DVD → remove Windows ISO** (keep only `utm-guest-tools.iso`) → restart.  

---

### Case 2: Message “It looks like you started an upgrade…”
- Reason: VM still booted from ISO.  
- Fix: Shut down → Settings → **remove Windows ISO** → restart.  
- VM will now boot into installed Windows.  

---

### Case 3: Windows desktop loads, activation fails  
- Message: *“Cannot connect to my organisation's activation server.”*  
- Fix: Ignore activation. Windows works fine except:  
  - Watermark “Activate Windows”  
  - No personalization (wallpapers/themes)  
- All SAP functions work without activation.  

---

## 7. Guest Tools
- If *Install drivers and SPICE tools* was checked, features should work:  
  - Auto-resize display  
  - Smooth mouse integration  
  - Clipboard sharing  
- If not → open `utm-guest-tools.iso` inside Windows and install manually.  

---

## 8. Activation
- Optional. Not required for SAP.  
- If provided by university:  
  `Settings → System → Activation → Change product key`  

---

# Part 2: SAP Environment Setup

## 1. Install VPN
1. Download your university’s VPN client inside Windows (not macOS host).  
   - Common: Cisco AnyConnect, FortiClient, Pulse Secure, OpenVPN.  
2. Install and log in with student credentials.  
3. Once connected → Windows VM is inside campus network.  

---

## 2. Install SAP GUI
1. Download SAP GUI installer from university IT portal.  
2. Run installer with default settings.  
3. After installation → find **SAP Logon** in Start Menu.  

---

## 3. Configure SAP Connection
1. Open **SAP Logon** → add new system.  
   - Application Server: (from university)  
   - System ID (SID): (provided by professor/IT)  
   - Instance Number: usually `00`  
   - Description: e.g. `SAP Training`  
2. Save connection.  

---

## 4. Test Login
1. Connect VPN.  
2. Open SAP Logon → double-click your system.  
3. Enter SAP credentials (student ID / password).  
4. Success → ABAP programming environment ready 🎉.  

---

## 5. Tips & Troubleshooting
- **VPN not working**: check credentials, run as Administrator.  
- **SAP Logon connection fails**: verify VPN and server info with professor.  
- **Fonts/UI broken**: set Windows display scaling to 100%.  
- **Windows not activated**: ignore, not required for SAP GUI.  

---

✍️ *Maintained by students of Augsburg University of Applied Sciences – 2025*  
