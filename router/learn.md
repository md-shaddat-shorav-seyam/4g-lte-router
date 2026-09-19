# Embedded Android & Linux Router Investigation: The Master Learning Guide

> **Target Device**: Qualcomm Snapdragon 410 (MSM8916) 4G LTE USB Router / MiFi (`13a06a2a`)  
> **Purpose**: A comprehensive educational guide detailing every command, core concept, reverse-engineering methodology, and rationale used to analyze the device from scratch.

---

## Table of Contents
1. [Methodology & Investigation Workflow](#1-methodology--investigation-workflow)
2. [Master Command, Concept & Rationale Reference Table](#2-master-command-concept--rationale-reference-table)
3. [Phase 1: Host-to-Device Discovery & USB Subsystem](#3-phase-1-host-to-device-discovery--usb-subsystem)
4. [Phase 2: Android OS, Shell Privileges & Security Model](#4-phase-2-android-os-shell-privileges--security-model)
5. [Phase 3: Hardware, SoC & Processor Architecture](#5-phase-3-hardware-soc--processor-architecture)
6. [Phase 4: Storage, eMMC & Qualcomm Partition Scheme](#6-phase-4-storage-emmc--qualcomm-partition-scheme)
7. [Phase 5: Networking, Cellular Modem & Radio Architecture](#7-phase-5-networking-cellular-modem--radio-architecture)
8. [Phase 6: Web Management Interface & API Reverse-Engineering](#8-phase-6-web-management-interface--api-reverse-engineering)
9. [Phase 7: Process Forensics & Memory Internals](#9-phase-7-process-forensics--memory-internals)
10. [Hardware Modding & Safe Backup Principles](#10-hardware-modding--safe-backup-principles)
11. [Essential Quick-Reference Cheat Sheet](#11-essential-quick-reference-cheat-sheet)

---

## 1. Methodology & Investigation Workflow

When reverse-engineering an unfamiliar embedded system (such as a 4G/5G USB dongle, smart router, or IoT appliance), follow the **7-Layer Investigation Funnel**:

```
 ┌────────────────────────────────────────────────────────┐
 │ Layer 1: Host Bus Discovery (USB VID:PID, Descriptors) │
 └───────────────────────────┬────────────────────────────┘
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ Layer 2: Debug Interface Access (ADB / Serial / Shell) │
 └───────────────────────────┬────────────────────────────┘
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ Layer 3: Privilege & OS Assessment (UID, SELinux, Root)│
 └───────────────────────────┬────────────────────────────┘
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ Layer 4: Hardware & SoC Probe (CPU, RAM, PMIC, Thermal)│
 └───────────────────────────┬────────────────────────────┘
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ Layer 5: Storage & Partition Mapping (eMMC, GPT, EFS)  │
 └───────────────────────────┬────────────────────────────┘
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ Layer 6: Networking & Radio Probe (Bridge, RIL, Modem) │
 └───────────────────────────┬────────────────────────────┘
                             ▼
 ┌────────────────────────────────────────────────────────┐
 │ Layer 7: Application & Web API Reverse-Engineering     │
 └────────────────────────────────────────────────────────┘
```

---

## 2. Master Command, Concept & Rationale Reference Table

| # | Command | Concept Behind It | Reason & What It Revealed |
| :- | :--- | :--- | :--- |
| **1** | `adb devices -l` | **ADB Device Enumeration**: Queries the ADB server for all connected targets with device product strings. | Identified serial `13a06a2a`, product `msm8916_32_512`, and target architecture. |
| **2** | `adb shell id` | **POSIX Identity & Linux UID**: Determines the user ID, group IDs, and SELinux context of the ADB daemon. | Showed we are `uid=2000(shell)` in context `u:r:shell:s0`. |
| **3** | `adb root` | **ADB Daemon Root Escalation**: Requests `adbd` to restart with root privileges (`uid=0`). | Failed with `error password`, indicating root debugging is locked with a password challenge. |
| **4** | `lsusb -v -d 05c6:90b4` | **USB Composite Gadget Descriptors**: Reads USB endpoint descriptors from Linux host. | Discovered 4 USB interfaces: RNDIS Control, RNDIS Data, Qualcomm Serial SMD, and ADB function. |
| **5** | `adb shell getprop` | **Android System Properties (bionic property service)**: Reads key-value pairs stored in shared memory (`/dev/__properties__`). | Revealed build date (Jan 2024), hardware version (`HW1.3`), gateway IP (`192.168.100.1`), Wi-Fi MAC, and default admin password (`admin`). |
| **6** | `cat /proc/cpuinfo` | **Linux Virtual Filesystem (Procfs)**: Exposes CPU core architecture, implementer, and hardware name. | Proved the chip is a 4-core Cortex-A53 (Part `0xd03`) running in 32-bit `ARMv7` mode. |
| **7** | `cat /proc/meminfo` | **Linux Memory Management Subsystem**: Reports RAM allocation, cache, buffers, and swap. | Confirmed **512 MB physical RAM** (~402 MB available to Linux) + **192 MB zRAM swap**. |
| **8** | `cat /proc/version` | **Linux Kernel Build Metadata**: Compiler version, builder identity, and build timestamp. | `Linux 3.10.28 SMP PREEMPT (gcc 4.7) Tue Jan 9 2024`. |
| **9** | `/sys/devices/soc0/*` | **Qualcomm Sysfs SoC Driver**: Direct hardware register readings exported by the kernel driver. | `soc_id: 206` (Snapdragon 410 MSM8916), PMIC model `65547` (PM8916). |
| **10** | `/sys/block/mmcblk0/device/*` | **eMMC Controller Hardware Registers**: Reads CID (Card ID), CSD, date, and vendor ID. | Showed **8 GB eMMC** (`EH8ED4`, Vendor `0x70`), with serial matching the ADB serial (`0x13a06a2a`). |
| **11** | `ls -l /dev/block/bootdevice/by-name/` | **Qualcomm Boot Device Partition Table**: Symlinks from human-readable names to raw MMC partitions. | Found all **27 partitions** (`modem`, `sbl1`, `aboot`, `boot`, `system`, `persist`, `userdata`). |
| **12** | `cat /proc/partitions` | **Linux Kernel Block Device Registry**: Sector counts and partition numbers for block devices. | Gave exact block sizes for every single partition on the eMMC chip. |
| **13** | `ip a` / `ifconfig` | **Linux Network Stack**: Inspects network interfaces, IP addresses, MACs, and MTUs. | Revealed `bridge1` bridging `wlan0` (Wi-Fi AP) and `rndis0` (USB Ethernet) at `192.168.100.1/24`. |
| **14** | `ip route` | **Kernel Routing Table**: Default routes and subnet scope. | Showed local traffic routing for `192.168.100.0/24`. |
| **15** | `netstat -tuln` | **Active Sockets & Listening Ports**: Checks all open TCP/UDP listening services. | Revealed Web UI on port `8000`, remote ADB on TCP port `10242`, and DNS/DHCP on port `53`/`67`. |
| **16** | `procrank` | **Setuid Root Memory Analysis Tool**: Calculates VSS, RSS, PSS, and USS per process. | Executed as root via SUID permission (`-rwsr-sr-x`), revealing memory footprint of `system_server`, `zygote`, and `com.wowi.nanowebyl`. |
| **17** | `dumpsys iphonesubinfo` | **Android Telephony Framework Service**: Queries `IPhoneSubInfo` Binder interface. | Extracted the active device **IMEI (`862129070795665`)**. |
| **18** | `dumpsys telephony.registry` | **Android Telephony Registry**: Live state of cellular signal, cell tower IDs, and registration. | Confirmed radio was camping for LTE/GSM towers with SIM absent. |
| **19** | `adb forward tcp:8080 tcp:8000` | **ADB Port Forwarding Socket Tunnel**: Maps a local host TCP port to a device port over USB. | Allowed direct HTTP browsing and API testing of the router's web portal from the host PC. |
| **20** | Web JS Inspection (`curl` + Python) | **Frontend Bundle Decompilation**: Analyzes bundled Vue.js scripts (`app.*.js`). | Reverse-engineered the JSON-RPC API protocol (`POST /api/json`), operations (`queryFields`), and session auth. |
| **21** | Web API Query (`POST /api/json`) | **Live API Telemetry Extraction**: Sends authenticated JSON-RPC requests. | Extracted live Wi-Fi SSID (`4G-MIFI-1DF0`), configured Wi-Fi password (`Seyam@12345678`), and LTE bands (`B1, B3, B5`). |

---

## 3. Phase 1: Host-to-Device Discovery & USB Subsystem

### Core Concepts:
1. **USB Composite Devices**: A single physical USB device can present multiple independent functional interfaces to the host OS using **USB Configuration Descriptors**.
2. **Qualcomm USB Gadget Subsystem (`android_usb`)**: The Snapdragon kernel uses the Linux USB Gadget framework to expose:
   - **RNDIS (Remote Network Driver Interface Specification)**: Emulates a virtual Ethernet network card over USB.
   - **SMD / Diagnostic Serial**: Exposes virtual COM ports for AT commands and Qualcomm DIAG protocol.
   - **FunctionFS ADB**: Provides the transport layer for ADB communication.

### Execution & Analysis:
```bash
# Check USB device hierarchy on host:
lsusb -t
# Output shows Bus 001 Port 2: Class=Wireless, Driver=rndis_host (480Mbps)

# Read USB vendor and product ID:
lsusb -v -d 05c6:90b4
```
- **VID `0x05c6`**: Qualcomm Inc.
- **PID `0x90b4`**: Qualcomm Android Composite Device.

---

## 4. Phase 2: Android OS, Shell Privileges & Security Model

### Core Concepts:
1. **Android User Separation**: Android runs under POSIX UID isolation.
   - `uid=0`: `root` (Superuser)
   - `uid=1000`: `system` (Framework services)
   - `uid=2000`: `shell` (ADB shell)
   - `uid=10000+`: `u0_aXX` (Individual sandboxed applications)
2. **SELinux (Security-Enhanced Linux)**:
   - **Enforcing**: Policy violations are blocked.
   - **Permissive**: Policy violations are logged but permitted.
   - Our device runs `ro.boot.selinux=permissive`, which makes modding much easier because operations aren't blocked by MAC (Mandatory Access Control) policies.
3. **Setuid Root Binaries (`SUID`)**:
   - Binaries with `-rwsr-sr-x root root` execute with root privileges regardless of who runs them.
   - We discovered `procrank`, `librank`, `procmem`, and `tcpdump` had SUID root permissions enabled, allowing us to inspect kernel process memory and capture network packets without full root shell access.

---

## 5. Phase 3: Hardware, SoC & Processor Architecture

### Core Concepts:
1. **Qualcomm MSM8916 (Snapdragon 410)**:
   - 4x ARM Cortex-A53 CPU cores.
   - Native 64-bit ARMv8 cores, but running a 32-bit `armeabi-v7a` userland for low memory consumption.
2. **Virtual Filesystem `/sys` (Sysfs)**:
   - `/sys/devices/soc0/` provides direct hardware information written by the Qualcomm SoC driver.
   - `/sys/class/thermal/` exposes TSENS (Thermal Sensor) ADC channels for CPU cores and PMIC.

### Commands Used:
```bash
# Check CPU cores & architecture
adb shell cat /proc/cpuinfo

# Check Qualcomm SoC ID & Platform Version
adb shell "for f in /sys/devices/soc0/*; do echo -n \"\$f: \"; cat \"\$f\"; done"

# Check CPU Clock Frequencies & Governor
adb shell cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
adb shell cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor

# Check Thermal Zones (CPU & PMIC Temperatures)
adb shell "for t in /sys/class/thermal/thermal_zone*; do cat \$t/type; cat \$t/temp; done"
```

---

## 6. Phase 4: Storage, eMMC & Qualcomm Partition Scheme

### Core Concepts:
1. **eMMC (Embedded MultiMediaCard)**:
   - Fixed NAND flash storage with integrated memory controller.
   - Register **CID** (Card Identification) holds manufacturer ID, product name, serial number, and manufacture date.
   - eMMC Name: `EH8ED4`, Size: `7,471,104 KB` (~7.68 GiB / **8 GB**).
2. **Qualcomm Boot Hierarchy & Partition Roles**:
   - **PBL (Primary Boot Loader)**: Burned into ROM inside the SoC.
   - **SBL1 (`mmcblk0p2`)**: Initializes DDR RAM and loads TrustZone/RPM.
   - **RPM (`mmcblk0p6`)**: Resource & Power Management processor firmware.
   - **TZ (`mmcblk0p8`)**: ARM TrustZone / Qualcomm Secure Execution Environment (QSEE).
   - **HYP (`mmcblk0p10`)**: Hypervisor image.
   - **ABOOT (`mmcblk0p4`)**: Little Kernel (LK) bootloader — handles Fastboot and boots the Linux kernel.
   - **MODEM (`mmcblk0p1`)**: Hexagon DSP modem baseband OS (`/firmware`).
   - **MODEMST1 (`mmcblk0p13`) & MODEMST2 (`mmcblk0p14`) & FSG (`mmcblk0p20`)**: EFS / NVRAM partitions storing IMEI, radio calibration, and RF parameters.
   - **PERSIST (`mmcblk0p24`)**: Stores persistent hardware calibration (Wi-Fi MAC, sensor calibration).
   - **BOOT (`mmcblk0p22`)**: Linux Kernel (`zImage`) + RAM disk (`initramfs`).
   - **SYSTEM (`mmcblk0p23`)**: Read-only Android system framework and binaries.
   - **USERDATA (`mmcblk0p27`)**: Read-write app and user storage (**~6.11 GB** free space).

### Locating Partition Nodes:
```bash
# Check all named partition symlinks
adb shell ls -l /dev/block/bootdevice/by-name/

# Read exact sector counts from procfs
adb shell cat /proc/partitions
```

---

## 7. Phase 5: Networking, Cellular Modem & Radio Architecture

### Core Concepts:
1. **Linux Network Bridging (`bridge1`)**:
   - Instead of routing between Wi-Fi and USB, the router creates a Linux software bridge (`bridge1`).
   - `bridge1` binds `wlan0` (Wi-Fi Access Point) and `rndis0` (USB Ethernet).
   - Both Wi-Fi clients and the USB host share the same `192.168.100.0/24` subnet.
2. **Dnsmasq Subsystem**:
   - Lightweight combined DNS forwarder and DHCP server running as a background daemon (`/system/bin/dnsmasq`).
   - Serves IP pool `192.168.100.2` – `192.168.100.254`.
3. **Qualcomm QMI (Qualcomm MSM Interface) & RIL**:
   - Android's `rild` connects to the Hexagon modem subsystem over shared memory character devices (`/dev/smd0`).
   - `netmgrd` configures the `rmnet0` data interfaces when cellular data connects.
4. **Android Dumpsys Telephony Services**:
   - The Binder service `iphonesubinfo` holds the hardware IMEI.
   - `telephony.registry` tracks cell tower reception, MCC/MNC, and signal strength.

### Extracting Radio Information:
```bash
# Query IMEI via Android Service Manager:
adb shell dumpsys iphonesubinfo

# Check network interfaces:
adb shell ip a

# Check active listeners:
adb shell netstat -tuln
```

---

## 8. Phase 6: Web Management Interface & API Reverse-Engineering

### Core Concepts:
1. **NanoHTTPD in Android**:
   - Embedded Java web server packaged inside `/system/priv-app/cpeweb.apk` (`com.wowi.nanowebyl`).
   - Listens on TCP Port `8000`.
2. **ADB Port Forwarding**:
   - Allows your PC to talk to device-internal network sockets without connecting to Wi-Fi.
   ```bash
   adb -s 13a06a2a forward tcp:8080 tcp:8000
   ```
3. **Frontend Bundle Decompilation & API Extraction**:
   - The web interface is a modern single-page Vue.js application.
   - By curling `http://127.0.0.1:8080/` and analyzing `/static/js/app.*.js`, we located the backend RPC endpoint: `POST /api/json`.
4. **JSON-RPC Authentication Flow**:
   - Step 1: Send `{"fid": "login", "username": "admin", "password": "admin"}`.
   - Step 2: Backend returns `{"reply": "ok", "session": "<UUID>"}`.
   - Step 3: Pass `<UUID>` in `Authorization: <UUID>` header and `"sessionId": "<UUID>"` payload to call `queryFields`, `setGW`, `setWifi`, `setApn`, etc.

### Live Query Script (Python Example):
```python
import urllib.request, json

# 1. Login
login_data = json.dumps({"fid": "login", "username": "admin", "password": "admin"}).encode('utf-8')
req = urllib.request.Request("http://127.0.0.1:8080/api/json", data=login_data, headers={"Content-Type": "application/json"})
res = json.loads(urllib.request.urlopen(req).read().decode('utf-8'))
session = res.get("session")

# 2. Query All Device Telemetry
fields_to_query = {
    "sn": "", "imei": "", "mac": "", "ssidName": "", "ssidPassword": "",
    "ipAddress": "", "dhcpFrom": "", "dhcpTo": "", "hardwareVersion": "",
    "systemVersion": "", "basebandVersion": "", "signalStrength": 0, "FreqBand": ""
}
query_payload = json.dumps({"fid": "queryFields", "sessionId": session, "fields": fields_to_query}).encode('utf-8')
req = urllib.request.Request("http://127.0.0.1:8080/api/json", data=query_payload,
                             headers={"Content-Type": "application/json", "Authorization": session})
telemetry = json.loads(urllib.request.urlopen(req).read().decode('utf-8'))
print(json.dumps(telemetry, indent=2))
```
**What this revealed**:
- Configured Wi-Fi SSID: `4G-MIFI-1DF0`
- Configured Wi-Fi Password: `Seyam@12345678`
- Device Serial Number: `10000000E9B427`

---

## 9. Phase 7: Process Forensics & Memory Internals

### Core Concepts:
1. **Memory Metrics on Embedded Linux**:
   - **VSS (Virtual Set Size)**: Total address space allocated.
   - **RSS (Resident Set Size)**: Total physical memory mapped (includes shared libraries).
   - **PSS (Proportional Set Size)**: RSS with shared libraries divided among sharing processes (best metric for true memory weight).
   - **USS (Unique Set Size)**: Private physical memory unique to that process only (what is freed if process is killed).
2. **Remote ADB on TCP**:
   - The device properties `service.adb.tcp.port=10242` and `persist.adb.tcp.port=10242` configure `adbd` to listen on TCP port **10242**.
   - You can connect wirelessly over Wi-Fi without USB:
     ```bash
     adb connect 192.168.100.1:10242
     ```

---

## 10. Hardware Modding & Safe Backup Principles

### ⚠️ Golden Rule of Qualcomm Modding
**Never flash custom ROMs (OpenWrt, Debian, PostmarketOS) before making full bit-for-bit raw backups of your NVRAM/EFS partitions.**

If you erase or corrupt `modemst1`, `modemst2`, `fsg`, or `persist`, you will lose your device's unique radio calibration, Wi-Fi MAC address, and IMEI permanently.

### Complete Backup Procedure:
```bash
# Dump raw images to internal storage:
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/modemst1 of=/data/modemst1.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/modemst2 of=/data/modemst2.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/fsg of=/data/fsg.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/persist of=/data/persist.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/boot of=/data/boot.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/aboot of=/data/aboot.img"

# Pull files safely to your host PC:
adb -s 13a06a2a pull /data/modemst1.img .
adb -s 13a06a2a pull /data/modemst2.img .
adb -s 13a06a2a pull /data/fsg.img .
adb -s 13a06a2a pull /data/persist.img .
adb -s 13a06a2a pull /data/boot.img .
adb -s 13a06a2a pull /data/aboot.img .
```

---

## 11. Essential Quick-Reference Cheat Sheet

| Task | Command |
| :--- | :--- |
| **Open Interactive Shell** | `adb -s 13a06a2a shell` |
| **Forward Web Admin Interface** | `adb -s 13a06a2a forward tcp:8080 tcp:8000` |
| **Connect ADB via Wi-Fi / TCP** | `adb connect 192.168.100.1:10242` |
| **Reboot into Fastboot Bootloader** | `adb -s 13a06a2a reboot bootloader` |
| **Reboot into Emergency Download (EDL 9008)** | `adb -s 13a06a2a reboot edl` |
| **Read Android System Properties** | `adb -s 13a06a2a shell getprop` |
| **Read Hardware SoC ID** | `adb -s 13a06a2a shell cat /sys/devices/soc0/soc_id` |
| **Inspect Running Processes & Memory** | `adb -s 13a06a2a shell procrank` |
| **Check Network Interfaces & IPs** | `adb -s 13a06a2a shell ip a` |
| **Check Listening Ports & Sockets** | `adb -s 13a06a2a shell netstat -tuln` |
| **Inspect eMMC Partitions** | `adb -s 13a06a2a shell ls -la /dev/block/bootdevice/by-name/` |
