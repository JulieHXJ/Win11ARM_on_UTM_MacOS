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
10. [Next Steps: SAP GUI](#9-next-steps-sap-gui)  

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
- On ISO setup screen → click **Get → Latest Windows 11 for ARM**.  
- Select language → download.  


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


## 9. Next Steps: SAP GUI
1. Inside Windows VM → install your university VPN client.
2. Connect VPN → ensures access to campus SAP servers.  
3. Download and install **SAP GUI for Windows** (from your university IT portal).  
4. Configure SAP connection settings → log in → start ABAP programming.  

---

*Maintained by students of Augsburg University of Applied Sciences – 2025*  
