# Qualcomm Snapdragon 410 (MSM8916) 4G LTE Router / MiFi Device Dossier

> **Device ADB Serial**: `13a06a2a`  
> **Investigation Date**: 2026-09-12  
> **Investigation Host**: `fedora` (Linux)  

---

## 1. Quick Device Overview & Hardware Specifications

| Specification | Value / Detail |
| :--- | :--- |
| **Device Model** | `msm8916_32_512` / `MF601STC` |
| **Custom Project** | `YL_MF601_D` (Hardware Ver: `HW1.3`) |
| **SoC / Chipset** | Qualcomm Snapdragon 410 (`MSM8916`) Quad-core ARM Cortex-A53 |
| **CPU Architecture** | ARMv7-A 32-bit (`armeabi-v7a`, Part `0xd03`, Rev 0) |
| **RAM (Memory)** | **512 MB** LPDDR3 (402,336 kB usable + 192 MB zRAM swap active) |
| **Storage (Flash)** | **8 GB eMMC** (`EH8ED4`, 7.68 GiB / 7,471,104 KB, CID: `7001004548384544340113a06a2a5500`) |
| **Power Management IC (PMIC)** | Qualcomm `PM8916` (`pm8916_tz`) |
| **Wi-Fi Subsystem** | Qualcomm Prima / WCNSS (`WCN3620` / `WCN3660` / `WCN3680`) |
| **Cellular Modem** | Qualcomm MSM8916 LTE Cat4 Baseband (`MF601S-EU 20230102`) |
| **Supported LTE Bands** | **B1** (2100 MHz), **B3** (1800 MHz), **B5** (850 MHz) |
| **SIM Card Slots** | 1x Micro/Nano-SIM slot (Single SIM config `ssss`, SIM hotplug supported) |
| **IMEI (Hardware)** | `862129070795665` (NV IMEI: `000000041775022`) |
| **Serial Number (SN)** | `10000000E9B427` (eMMC Serial: `0x13a06a2a`) |
| **Operating System** | Android 4.4.4 KitKat (API Level 19, `userdebug`, `low_ram` mode) |
| **Kernel Version** | `Linux 3.10.28 SMP PREEMPT (gcc 4.7) Tue Jan 9 17:30:18 CST 2024` |
| **SELinux Mode** | `Permissive` (`ro.boot.selinux=permissive`) |
| **Web Management UI** | Vue.js Single Page App + Android NanoHTTPD (`WEB_V1.0.332#` on port `8000`) |

---

## 2. Wireless & Network Configuration

### Wi-Fi Access Point (AP) Settings
- **SSID**: `4G-MIFI-1DF0` (Default Prefix: `4G-MIFI-`)
- **Wi-Fi Password**: `Seyam@12345678` *(Default factory password was `1234567890`)*
- **Security Mode**: `WPA2_PSK`
- **SSID Broadcast**: Enabled (`true`)
- **Max Connected Users**: `10`
- **Wi-Fi MAC Address**: `5c:a0:01:5b:1d:f0`
- **Wi-Fi Chip Driver**: Qualcomm WCNSS (`wcnss_service`, driver config `/data/misc/wifi/WCNSS_qcom_cfg.ini`)

### Local Network & Gateway Configuration
- **Gateway IP Address**: `192.168.100.1`
- **Subnet Mask**: `255.255.255.0` (`/24`)
- **DHCP Server**: Enabled (`dnsmasq`)
- **DHCP IP Pool**: `192.168.100.2` – `192.168.100.254`
- **DHCP Lease Time**: `3 hours`
- **Bridge Configuration**: `bridge1` interface bridging `wlan0` (Wi-Fi AP) and `rndis0` (USB Ethernet)

### Active Network Interfaces & IP Addresses
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN 
    link/ether 26:ab:a3:96:76:2e brd ff:ff:ff:ff:ff:ff
3: ifb0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN qlen 32
    link/ether 22:69:41:ae:1c:35 brd ff:ff:ff:ff:ff:ff
4: ifb1: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN qlen 32
    link/ether 5a:6a:cc:ad:a4:48 brd ff:ff:ff:ff:ff:ff
5: sit0: <NOARP> mtu 1480 qdisc noop state DOWN 
    link/sit 0.0.0.0 brd 0.0.0.0
6: rmnet0: <UP,LOWER_UP> mtu 2000 qdisc pfifo_fast state UNKNOWN qlen 1000
    link/[530] 
7: rmnet1: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether aa:8e:30:20:76:65 brd ff:ff:ff:ff:ff:ff
8: rmnet2: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether ae:53:29:38:9a:aa brd ff:ff:ff:ff:ff:ff
9: rmnet3: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether ba:74:58:71:3d:32 brd ff:ff:ff:ff:ff:ff
10: rmnet4: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether a6:91:30:c5:bb:be brd ff:ff:ff:ff:ff:ff
11: rmnet5: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether e2:cd:7a:ad:61:d3 brd ff:ff:ff:ff:ff:ff
12: rmnet6: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether 0e:12:4d:f5:e0:92 brd ff:ff:ff:ff:ff:ff
13: rmnet7: <BROADCAST,MULTICAST> mtu 2000 qdisc noop state DOWN qlen 1000
    link/ether e6:c8:d9:b5:e9:c2 brd ff:ff:ff:ff:ff:ff
14: rmnet_data0: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
15: rmnet_data1: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
16: rmnet_data2: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
17: rmnet_data3: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
18: rmnet_data4: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
19: rmnet_data5: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
20: rmnet_data6: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
21: rmnet_data7: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
22: r_rmnet_data0: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
23: r_rmnet_data1: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
24: r_rmnet_data2: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
25: r_rmnet_data3: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
26: r_rmnet_data4: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
27: r_rmnet_data5: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
28: r_rmnet_data6: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
29: r_rmnet_data7: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
30: r_rmnet_data8: <> mtu 1500 qdisc noop state DOWN qlen 1000
    link/[530] 
34: bridge1: <BROADCAST,MULTICAST,ALLMULTI,PROMISC,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP 
    link/ether 02:02:d9:be:de:6d brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.1/24 brd 192.168.100.255 scope global bridge1
       valid_lft forever preferred_lft forever
    inet6 fe80::842a:4cff:feb6:f62d/64 scope link 
       valid_lft forever preferred_lft forever
35: wlan0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc mq master bridge1 state UP qlen 1000
    link/ether 5c:a0:01:5b:1d:f0 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::5ea0:1ff:fe5b:1df0/64 scope link 
       valid_lft forever preferred_lft forever
37: rndis0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master bridge1 state UP qlen 1000
    link/ether 02:02:d9:be:de:6d brd ff:ff:ff:ff:ff:ff
    inet6 fe80::2:d9ff:febe:de6d/64 scope link 
       valid_lft forever preferred_lft forever
```

### Kernel Routing Table
```
192.168.100.0/24 dev bridge1  proto kernel  scope link  src 192.168.100.1
```

---

## 3. Cellular Modem & SIM Subsystem

- **Modem Firmware Version**: `MF601S-EU 20230102` (European regional band firmware)
- **Cellular Network Mode**: `12` (LTE / WCDMA / GSM auto)
- **LTE Frequency Bands**:
  - Band 1 (2100 MHz)
  - Band 3 (1800 MHz)
  - Band 5 (850 MHz)
- **Hardware IMEI**: `862129070795665`
- **NVRAM IMEI**: `000000041775022`
- **SIM Slot Count**: 1
- **Current SIM Status**: `ABSENT` / `invalid` (No SIM card inserted)
- **Radio Interface Layer (RIL)**: `Qualcomm RIL 1.0` (`/system/vendor/lib/libril-qc-qmi-1.so`) via SMD device `/dev/smd0`
- **Qualcomm Telephony Daemons**: `rild`, `qmuxd`, `netmgrd`, `ATFWD-daemon`, `dpmd`

---

## 4. Web Admin Interface & REST API

The device runs an embedded web management portal powered by **NanoHTTPD** inside the Android package `com.wowi.nanowebyl` (`/system/priv-app/cpeweb.apk`).

### Access Details
- **Local Web URL**: `http://192.168.100.1:8000/`
- **Port Forward Access (via ADB)**:
  ```bash
  adb -s 13a06a2a forward tcp:8080 tcp:8000
  # Open in browser: http://127.0.0.1:8080/
  ```
- **Web Admin Login**:
  - **Username**: `admin`
  - **Password**: `admin` (Stored in `persist.web.login.password=admin`)
  - **Default Language**: `en` (English)

### Web API Architecture
The web application communicates via `POST /api/json` using JSON-RPC style payloads:

#### 1. Authentication (`login`)
```json
// Request
POST /api/json
{
  "fid": "login",
  "username": "admin",
  "password": "admin"
}

// Response
{
  "reply": "ok",
  "session": "<uuid-session-token>"
}
```

#### 2. Query Device Telemetry (`queryFields`)
Send with header `Authorization: <session-token>`:
```json
POST /api/json
{
  "fid": "queryFields",
  "sessionId": "<session-token>",
  "fields": {
    "sn": "", "imei": "", "mac": "", "ssidName": "",
    "ssidPassword": "", "ipAddress": "", "dhcpFrom": "",
    "dhcpTo": "", "hardwareVersion": "", "systemVersion": "",
    "basebandVersion": "", "signalStrength": 0, "FreqBand": ""
  }
}
```

#### Current Live API Dump
```json
{
  "dhcpFrom": "192.168.100.2",
  "withMtp": false,
  "ssidMaxUserCount": 10,
  "factoryWifi": 1,
  "simCardState": "invalid",
  "simCardCurrent": 0,
  "ssidBroadcast": true,
  "subnetMask": "255.255.255.0",
  "usbMode": 0,
  "mac": "5c:a0:01:5b:1d:f0",
  "simCardSlotCount": 1,
  "ssidName": "4G-MIFI-1DF0",
  "factory4G": 1,
  "dhcpSwitch": "on",
  "carrier": "",
  "deviceList": [],
  "wanIpAddress": "",
  "netWorkMode": 12,
  "ipAddress": "192.168.100.1",
  "signalStrength": -110,
  "factoryRouter": 5,
  "sn": "10000000E9B427",
  "dhcpTo": "192.168.100.254",
  "imei": "862129070795665",
  "basebandVersion": "MF601S-EU 20230102",
  "ssidPassword": "Seyam@12345678",
  "imeiSwitch": true,
  "internetState": "disconnected",
  "dhcpLeases": "3",
  "wifiApSwitch": "on",
  "FreqBand": [
    {
      "value": "1",
      "label": "B1"
    },
    {
      "value": "3",
      "label": "B3"
    },
    {
      "value": "5",
      "label": "B5"
    }
  ],
  "systemRunTime": 1101,
  "iccId": "",
  "systemVersion": "MF601STC_D_V03_ZX_DD_N_240109",
  "appVersion": "WEB_V1.0.332#",
  "ssidSecureMode": "WPA2_PSK",
  "simBaseInfo": {
    "cellId": 0,
    "lac": 0
  },
  "imsi": "",
  "ethType": "lan",
  "hardwareVersion": "HW1.3"
}
```

#### Available API Functions (`fid`)
- `login`: Authenticate and obtain session token
- `init`: Query initial language and basic parameters
- `queryFields`: Query router parameters and live status
- `setFields`: Update router system parameters
- `setGW`: Update Gateway IP, subnet mask, and DHCP pool settings
- `setWifi`: Update Wi-Fi AP SSID, password, broadcast status, and security mode
- `setApn` / `queryApn` / `deleteApn` / `setDefaultApn`: Cellular APN profile management
- `switchSimCard`: Switch active SIM slot (for multi-SIM hardware)
- `rebootSystem`: Soft reboot the device
- `factoryReset`: Restore factory default settings
- `changePassword`: Update web portal admin password
- `upgradeSystem`: Flash Android system firmware image
- `upgradeWebServer`: Update web portal static files/apk

---

## 5. Storage, eMMC & Partition Layout

The device features an **8 GB eMMC flash chip** (`EH8ED4`) partitioned into 27 standard Qualcomm Android partitions.

### eMMC Chip Details
```

```

### Partition Map (`/proc/partitions`)
```
major minor  #blocks  name

 253        0     196608 zram0
 179        0    7471104 mmcblk0
 179        1      65536 mmcblk0p1
 179        2        512 mmcblk0p2
 179        3        512 mmcblk0p3
 179        4       1024 mmcblk0p4
 179        5       1024 mmcblk0p5
 179        6        512 mmcblk0p6
 179        7        512 mmcblk0p7
 179        8        512 mmcblk0p8
 179        9        512 mmcblk0p9
 179       10        512 mmcblk0p10
 179       11        512 mmcblk0p11
 179       12       1024 mmcblk0p12
 179       13       1536 mmcblk0p13
 179       14       1536 mmcblk0p14
 179       15       1024 mmcblk0p15
 179       16          1 mmcblk0p16
 179       17          8 mmcblk0p17
 179       18      10240 mmcblk0p18
 179       19         32 mmcblk0p19
 179       20       1536 mmcblk0p20
 179       21         16 mmcblk0p21
 179       22      16384 mmcblk0p22
 179       23     819200 mmcblk0p23
 179       24      32768 mmcblk0p24
 179       25     131072 mmcblk0p25
 179       26      16384 mmcblk0p26
 179       27    6257087 mmcblk0p27
 179       32       4096 mmcblk0rpmb
```

### Qualcomm Partition Device Mapping (`/dev/block/bootdevice/by-name/`)
| Partition Name | Block Device | Size | Purpose |
| :--- | :--- | :--- | :--- |
| **`modem`** | `mmcblk0p1` | 64 MB | Qualcomm Baseband / Hexagon DSP Firmware (`/firmware`) |
| **`sbl1`** | `mmcblk0p2` | 512 KB | Secondary Bootloader 1 (Primary) |
| **`sbl1bak`** | `mmcblk0p3` | 512 KB | Secondary Bootloader 1 (Backup) |
| **`aboot`** | `mmcblk0p4` | 1 MB | Little Kernel (LK) Bootloader / Fastboot (Primary) |
| **`abootbak`** | `mmcblk0p5` | 1 MB | Little Kernel (LK) Bootloader (Backup) |
| **`rpm`** | `mmcblk0p6` | 512 KB | Resource & Power Manager Firmware (Primary) |
| **`rpmbak`** | `mmcblk0p7` | 512 KB | Resource & Power Manager Firmware (Backup) |
| **`tz`** | `mmcblk0p8` | 512 KB | ARM TrustZone / QSEE (Primary) |
| **`tzbak`** | `mmcblk0p9` | 512 KB | ARM TrustZone / QSEE (Backup) |
| **`hyp`** | `mmcblk0p10` | 512 KB | Hypervisor (Primary) |
| **`hypbak`** | `mmcblk0p11` | 512 KB | Hypervisor (Backup) |
| **`pad`** | `mmcblk0p12` | 1 MB | Partition alignment padding |
| **`modemst1`** | `mmcblk0p13` | 1.5 MB | Non-Volatile Memory (NVRAM / EFS 1) - Radio/IMEI calibration |
| **`modemst2`** | `mmcblk0p14` | 1.5 MB | Non-Volatile Memory (NVRAM / EFS 2) - Radio/IMEI calibration |
| **`misc`** | `mmcblk0p15` | 1 MB | Bootloader control & recovery flags |
| **`fsc`** | `mmcblk0p16` | 1 KB | File System Cookie |
| **`ssd`** | `mmcblk0p17` | 8 KB | Secure Software Download storage |
| **`splash`** | `mmcblk0p18` | 10 MB | Boot logo splash image |
| **`DDR`** | `mmcblk0p19` | 32 KB | DDR memory training parameters |
| **`fsg`** | `mmcblk0p20` | 1.5 MB | Golden NVRAM backup |
| **`sec`** | `mmcblk0p21` | 16 KB | Security partition |
| **`boot`** | `mmcblk0p22` | 16 MB | Android Kernel (`zImage`) + Initramfs |
| **`system`** | `mmcblk0p23` | 800 MB | Android System Filesystem (Ext4, ro) |
| **`persist`** | `mmcblk0p24` | 32 MB | Persistent calibration & Wi-Fi NVRAM (`WCNSS_qcom_wlan_nv.bin`) |
| **`cache`** | `mmcblk0p25` | 128 MB | Cache Filesystem (Ext4, rw) |
| **`recovery`** | `mmcblk0p26` | 16 MB | Recovery Kernel & Ramdisk |
| **`userdata`** | `mmcblk0p27` | **~6.11 GB** | User Data & Internal Storage (Ext4, rw) |
| **`mmcblk0rpmb`** | Replay Protected Memory Block | 4 MB | Replay-protected hardware key store |

### Active Filesystem Mounts (`df -h` & `mount`)
```
Filesystem               Size     Used     Free   Blksize
/dev                   196.5M   128.0K   196.3M   4096
/sys/fs/cgroup         196.5M    12.0K   196.4M   4096
/mnt/asec              196.5M     0.0K   196.5M   4096
/mnt/obb               196.5M     0.0K   196.5M   4096
/system                774.9M   293.8M   481.1M   4096
/data                    5.8G    20.4M     5.8G   4096
/cache                 122.0M    72.0K   121.9M   4096
/persist                27.5M    88.0K    27.4M   4096
/firmware               64.0M    49.6M    14.4M   16384
/mnt/shell/emulated      5.8G    20.4M     5.8G   4096
/mnt/shell/emulated/0     5.8G    20.4M     5.8G   4096
```

```
rootfs / rootfs ro,relatime 0 0
tmpfs /dev tmpfs rw,seclabel,nosuid,relatime,mode=755 0 0
devpts /dev/pts devpts rw,seclabel,relatime,mode=600 0 0
proc /proc proc rw,relatime 0 0
sysfs /sys sysfs rw,seclabel,relatime 0 0
selinuxfs /sys/fs/selinux selinuxfs rw,relatime 0 0
debugfs /sys/kernel/debug debugfs rw,relatime 0 0
none /acct cgroup rw,relatime,cpuacct 0 0
none /sys/fs/cgroup tmpfs rw,seclabel,relatime,mode=750,gid=1000 0 0
tmpfs /mnt/asec tmpfs rw,seclabel,relatime,mode=755,gid=1000 0 0
tmpfs /mnt/obb tmpfs rw,seclabel,relatime,mode=755,gid=1000 0 0
none /dev/cpuctl cgroup rw,relatime,cpu 0 0
adb /dev/usb-ffs/adb functionfs rw,relatime 0 0
/dev/block/bootdevice/by-name/system /system ext4 ro,seclabel,relatime,discard,data=ordered 0 0
/dev/block/bootdevice/by-name/userdata /data ext4 rw,seclabel,nosuid,nodev,relatime,discard,noauto_da_alloc,data=ordered 0 0
/dev/block/bootdevice/by-name/cache /cache ext4 rw,seclabel,nosuid,nodev,relatime,data=ordered 0 0
/dev/block/bootdevice/by-name/persist /persist ext4 rw,seclabel,nosuid,nodev,relatime,data=ordered 0 0
/dev/block/bootdevice/by-name/modem /firmware vfat ro,relatime,uid=1000,gid=1000,fmask=0337,dmask=0227,codepage=437,iocharset=iso8859-1,shortname=lower,errors=remount-ro 0 0
/dev/fuse /mnt/shell/emulated fuse rw,nosuid,nodev,relatime,user_id=1023,group_id=1023,default_permissions,allow_other 0 0
/dev/fuse /mnt/shell/emulated/0 fuse rw,nosuid,nodev,relatime,user_id=1023,group_id=1023,default_permissions,allow_other 0 0
```

---

## 6. USB Subsystem & Debugging Ports

### Host USB Device Descriptors
- **USB Vendor ID / Product ID**: `05c6:90b4` (Qualcomm, Inc. Android)
- **USB Speed**: High Speed (480 Mbps)
- **Host Driver**: `rndis_host` (USB Network), `usbfs` (ADB)

### USB Composite Endpoints
1. **Interface 0 & 1**: `RNDIS Communications Control` & `RNDIS Ethernet Data` (USB Tethering)
2. **Interface 2**: Qualcomm Serial SMD / Modem Diagnostic Port
3. **Interface 3**: Android Debug Bridge (ADB) Interface

### ADB Access Methods
- **USB ADB**: Directly via USB serial `13a06a2a`
  ```bash
  adb -s 13a06a2a shell
  ```
- **Network / Wi-Fi ADB**: The device listens for ADB connections over TCP port **`10242`**:
  ```bash
  adb connect 192.168.100.1:10242
  ```

### Listening Network Ports (`netstat -tuln`)
```
Proto Recv-Q Send-Q Local Address          Foreign Address        State
 tcp       0      0 0.0.0.0:10242          0.0.0.0:*              LISTEN
 tcp       0      0 127.0.0.1:53           0.0.0.0:*              LISTEN
 tcp       0      0 192.168.100.1:53       0.0.0.0:*              LISTEN
 tcp       0      0 127.0.0.1:40488        127.0.0.1:8000         TIME_WAIT
 udp       0      0 127.0.0.1:53           0.0.0.0:*              CLOSE
 udp       0      0 192.168.100.1:53       0.0.0.0:*              CLOSE
 udp       0      0 0.0.0.0:67             0.0.0.0:*              CLOSE
tcp6       0      0 :::8000                :::*                   LISTEN
tcp6       0      0 ::ffff:127.0.0.1:8000  ::ffff:127.0.0.1:40489 TIME_WAIT
udp6       0      0 :::54321               :::*                   CLOSE
```
- **Port `8000` (TCP)**: Web Management HTTP Interface (`com.wowi.nanowebyl`)
- **Port `10242` (TCP)**: Wireless / Remote ADB daemon (`adbd`)
- **Port `53` (TCP/UDP)**: Local DNS resolver (`dnsmasq`)
- **Port `67` (UDP)**: Local DHCP server (`dnsmasq`)
- **Port `54321` (UDP)**: Proprietary discovery service

---

## 7. SoC, CPU & Hardware Sensors

### Qualcomm SoC Information (`/sys/devices/soc0/*`)
```

```

### CPU Information (`/proc/cpuinfo`)
```
processor	: 0
model name	: ARMv7 Processor rev 0 (v7l)
BogoMIPS	: 38.40
Features	: swp half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 evtstrm 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 0

processor	: 1
model name	: ARMv7 Processor rev 0 (v7l)
BogoMIPS	: 38.40
Features	: swp half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 evtstrm 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 0

processor	: 2
model name	: ARMv7 Processor rev 0 (v7l)
BogoMIPS	: 38.40
Features	: swp half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 evtstrm 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 0

processor	: 3
model name	: ARMv7 Processor rev 0 (v7l)
BogoMIPS	: 38.40
Features	: swp half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 evtstrm 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xd03
CPU revision	: 0

Hardware	: Qualcomm Technologies, Inc MSM8916
Revision	: 0000
Serial		: 0000000000000000
Processor	: ARMv7 Processor rev 0 (v7l)
```

### Memory Details (`/proc/meminfo`)
```
MemTotal:         402336 kB
MemFree:           56804 kB
Buffers:            5856 kB
Cached:           189724 kB
SwapCached:            0 kB
Active:            96448 kB
Inactive:         175204 kB
Active(anon):      76108 kB
Inactive(anon):      176 kB
Active(file):      20340 kB
Inactive(file):   175028 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:        196604 kB
SwapFree:         196604 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:         76120 kB
Mapped:            56920 kB
Shmem:               232 kB
Slab:              40252 kB
SReclaimable:      18564 kB
SUnreclaim:        21688 kB
KernelStack:        4584 kB
PageTables:         4660 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      397772 kB
Committed_AS:    4349216 kB
VmallocTotal:     499712 kB
VmallocUsed:       51056 kB
VmallocChunk:     310300 kB
```

### Thermal Zones & Temperature Sensors
```
:  = 
:  = 
:  = 
:  = 
:  = 
:  = 
:  = 
:  =
```
- **CPU Cores (`tsens_tz_sensor0` – `sensor5`)**: ~43°C – 48°C (Normal operating temperature)
- **Qualcomm PM8916 PMIC (`pm8916_tz`)**: ~60.3°C

---

## 8. Process & Memory Breakdown (`procrank`)

```
PID       Vss      Rss      Pss      Uss  cmdline
  788   392860K   37980K   16744K   13308K  system_server
  198   319620K   41568K   16150K   10896K  zygote
  995   349496K   32620K   13383K   10832K  com.wowi.nanowebyl
  862   343472K   29060K    9261K    6588K  com.android.systemui
  980   348520K   26324K    7915K    6072K  com.android.phone
  197    34384K   10576K    7422K    6532K  /system/bin/surfaceflinger
  939   333600K   23576K    5857K    4352K  android.process.acore
  956   338516K   24800K    5819K    4140K  com.android.inputmethod.latin
  200    29472K    9196K    5774K    4844K  /system/bin/mediaserver
  930   330600K   22548K    4759K    3216K  android.process.media
  196    29812K    7268K    4460K    3996K  /system/bin/rild
 1216   335168K   19984K    3682K    2432K  com.android.settings
 1254   330452K   20224K    3297K    2024K  com.android.providers.calendar
  971   331736K   18496K    2474K    1328K  com.qualcomm.telephony
 1029   329752K   17860K    2252K    1152K  com.android.printspooler
 1361   328588K   17840K    2129K    1028K  com.qualcomm.datamonitor
 1111   330620K   17376K    2012K     972K  com.qualcomm.qcrilmsgtunnel
 1010   328500K   17192K    1884K     828K  com.qualcomm.display
 1348   328692K   16840K    1852K     812K  com.qualcomm.atuner
 1070   330564K   16940K    1808K     776K  com.android.smspush
  199    11024K    3612K    1306K     956K  /system/bin/drmserver
 1592     1904K    1384K    1153K    1148K  procrank
  257     9832K    2000K    1023K     924K  /system/bin/netmgrd
  251     8048K    2592K     824K     600K  /system/bin/audiod
  209    34388K    1544K     716K     668K  /system/bin/thermal-engine
  194    11232K    1684K     714K     620K  /system/bin/netd
  237     6508K    1764K     662K     568K  /system/bin/dpmd
 1377     2732K    1332K     596K     528K  /system/bin/hostapd
    1      804K     660K     529K     448K  /init
  203     5272K    1424K     512K     412K  /system/bin/qcom-system-daemon
  234     5164K    1248K     486K     444K  /system/bin/qmuxd
  188     4748K    1200K     486K     428K  /system/bin/vold
  243     8276K    1544K     485K     416K  /system/bin/ATFWD-daemon
  202     3656K    1364K     475K     412K  /system/bin/keystore
  195     1512K    1012K     442K     416K  /system/bin/debuggerd
  254     4008K    1336K     435K     368K  /system/bin/wcnss_service
  250     7924K    1276K     424K     376K  /system/bin/time_daemon
  206     3568K    1064K     385K     344K  /system/bin/ptt_socket_app
  235     1412K     812K     346K     332K  /system/bin/sh
  190     2492K     828K     291K     264K  /system/bin/rfs_access
 1331     1328K     772K     277K     260K  /system/bin/dnsmasq
  276     6428K     832K     277K     252K  /system/bin/rmt_storage
 1189     6516K     836K     269K     252K  /system/bin/mpdecision
  263     6712K     752K     261K     148K  /system/bin/qseecomd
  147      612K     336K     256K     180K  /sbin/ueventd
 1404     5624K     252K     224K     224K  /sbin/adbd
  246     2772K     692K     217K     204K  /system/bin/sdcard
  201     1288K     708K     215K     200K  /system/bin/installd
  340     1356K     748K     199K     180K  /system/bin/vm_bms
  208     1220K     648K     176K     164K  /system/bin/qrngd
  193     2480K     832K     168K      60K  /system/bin/qseecomd
  187     1348K     632K     158K     124K  /system/bin/servicemanager
  186     1432K     148K     144K     144K  /sbin/healthd
                           ------   ------  ------
                          134090K   99192K  TOTAL

RAM: 402336K total, 55680K free, 5856K buffers, 189724K cached, 232K shmem, 40276K slab
```

---

## 9. Flashing, Backup & Linux / OpenWrt Porting Notes

### Why this device is ideal for modding:
1. **SoC Support**: The Qualcomm **Snapdragon 410 (MSM8916)** is one of the best-supported ARM64/ARM32 SoCs in the mainline Linux kernel (Linux 5.x / 6.x) via the **Open-Stick** / **handsome_hacker** community projects.
2. **Flash Size**: Unlike standard 4GB sticks, this unit is equipped with an **8GB eMMC flash chip** (leaving >6GB for rootfs), making it capable of running **Debian**, **Alpine Linux**, **OpenWrt**, or **postmarketOS** with Docker / Podman containers.
3. **SELinux Permissive**: Bootloader boots in permissive mode (`ro.boot.selinux=permissive`).
4. **ADB & Fastboot Access**: ADB is unlocked out of the box with root tools (`procrank`, `tcpdump`, `librank` setuid root).

### Essential Backup Commands (Run Before Flashing)
Before flashing custom firmware, backup critical radio calibration (EFS/NVRAM) partitions:

```bash
# 1. Backup Modem & NVRAM partitions (CRITICAL FOR IMEI / BASEBAND)
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/modemst1 of=/data/modemst1.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/modemst2 of=/data/modemst2.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/fsg of=/data/fsg.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/persist of=/data/persist.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/boot of=/data/boot.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/recovery of=/data/recovery.img"
adb -s 13a06a2a shell "dd if=/dev/block/bootdevice/by-name/aboot of=/data/aboot.img"

# 2. Pull all backups to local PC
adb -s 13a06a2a pull /data/modemst1.img .
adb -s 13a06a2a pull /data/modemst2.img .
adb -s 13a06a2a pull /data/fsg.img .
adb -s 13a06a2a pull /data/persist.img .
adb -s 13a06a2a pull /data/boot.img .
adb -s 13a06a2a pull /data/recovery.img .
adb -s 13a06a2a pull /data/aboot.img .
```

### Booting into Fastboot / EDL Mode
- **Fastboot Mode**:
  ```bash
  adb -s 13a06a2a reboot bootloader
  ```
- **Qualcomm 9008 EDL (Emergency Download) Mode**:
  ```bash
  adb -s 13a06a2a reboot edl
  ```

---

## 10. Complete Android System Properties (`getprop`)

<details>
<summary>Click to expand all system properties</summary>

```ini
[DEVICE_PROVISIONED]: [1]
[audio.offload.buffer.size.kb]: [32]
[audio.offload.gapless.enabled]: [false]
[av.offload.enable]: [true]
[config.disable_atlas]: [true]
[dalvik.vm.heapgrowthlimit]: [48m]
[dalvik.vm.heapmaxfree]: [2m]
[dalvik.vm.heapminfree]: [512k]
[dalvik.vm.heapsize]: [128m]
[dalvik.vm.heapstartsize]: [5m]
[dalvik.vm.heaptargetutilization]: [0.75]
[dalvik.vm.lockprof.threshold]: [500]
[dalvik.vm.stack-trace-file]: [/data/anr/traces.txt]
[debug.composition.type]: [c2d]
[debug.egl.hw]: [1]
[debug.force_rtl]: [0]
[debug.hwc.fakevsync]: [0]
[debug.mdpcomp.logs]: [0]
[debug.sf.hw]: [1]
[dev.bootcomplete]: [1]
[dev.pm.dyn_samplingrate]: [1]
[dolby.audio.sink.info]: [speaker]
[gsm.current.phone-type]: [1]
[gsm.network.type]: [Unknown]
[gsm.operator.alpha]: []
[gsm.operator.iso-country]: []
[gsm.operator.isroaming]: [false]
[gsm.operator.numeric]: []
[gsm.sim.operator.iso-country]: []
[gsm.sim.state]: [ABSENT]
[gsm.version.baseband]: [MF601S-EU 20230102]
[gsm.version.ril-impl]: [Qualcomm RIL 1.0]
[init.svc.adbd]: [running]
[init.svc.atfwd]: [running]
[init.svc.audiod]: [running]
[init.svc.bootanim]: [stopped]
[init.svc.carrier_switcher]: [stopped]
[init.svc.cnd]: [stopped]
[init.svc.config-video]: [stopped]
[init.svc.config-zram]: [stopped]
[init.svc.config_bluetooth]: [stopped]
[init.svc.console]: [running]
[init.svc.debuggerd]: [running]
[init.svc.dpmd]: [running]
[init.svc.drm]: [running]
[init.svc.healthd]: [running]
[init.svc.installd]: [running]
[init.svc.irsc_util]: [stopped]
[init.svc.keystore]: [running]
[init.svc.media]: [running]
[init.svc.mpdecision]: [running]
[init.svc.netd]: [running]
[init.svc.netmgrd]: [running]
[init.svc.p2p_supplicant]: [stopped]
[init.svc.ptt_socket_app]: [running]
[init.svc.qcom-c_core-sh]: [stopped]
[init.svc.qcom-c_main-sh]: [stopped]
[init.svc.qcom-post-boot]: [stopped]
[init.svc.qcom-sh]: [stopped]
[init.svc.qcom-usb-sh]: [stopped]
[init.svc.qcomsysd]: [running]
[init.svc.qmuxd]: [running]
[init.svc.qrngd]: [running]
[init.svc.qrngp]: [stopped]
[init.svc.qseecomd]: [running]
[init.svc.rfs_access]: [running]
[init.svc.ril-daemon]: [running]
[init.svc.rmt_storage]: [running]
[init.svc.sdcard]: [running]
[init.svc.servicemanager]: [running]
[init.svc.ssr_setup]: [stopped]
[init.svc.surfaceflinger]: [running]
[init.svc.thermal-engine]: [running]
[init.svc.time_daemon]: [running]
[init.svc.ueventd]: [running]
[init.svc.usb_uicc_daemon]: [stopped]
[init.svc.usb_uicc_enable]: [stopped]
[init.svc.vm_bms]: [running]
[init.svc.vold]: [running]
[init.svc.wcnss-service]: [running]
[init.svc.zygote]: [running]
[keyguard.no_require_sim]: [true]
[media.aac_51_output_enabled]: [false]
[media.stagefright.enable-aac]: [false]
[media.stagefright.enable-fma2dp]: [false]
[media.stagefright.enable-http]: [false]
[media.stagefright.enable-player]: [false]
[media.stagefright.enable-qcp]: [false]
[media.stagefright.enable-scan]: [false]
[media.swhevccodectype]: [1]
[mm.enable.qcom_parser]: [3407871]
[mmp.enable.3g2]: [false]
[net.bt.name]: [Android]
[net.change]: [net.qtaguid_enabled]
[net.hostname]: [android-f52020ab1d17d8b5]
[net.qtaguid_enabled]: [1]
[net.tcp.buffersize.default]: [4096,87380,110208,4096,16384,110208]
[net.tcp.buffersize.edge]: [4093,26280,35040,4096,16384,35040]
[net.tcp.buffersize.evdo]: [4094,87380,262144,4096,16384,262144]
[net.tcp.buffersize.gprs]: [4092,8760,11680,4096,8760,11680]
[net.tcp.buffersize.hsdpa]: [4094,87380,1220608,4096,16384,1220608]
[net.tcp.buffersize.hspa]: [4094,87380,1220608,4096,16384,1220608]
[net.tcp.buffersize.hspap]: [4094,87380,1220608,4096,16384,1220608]
[net.tcp.buffersize.hsupa]: [4094,87380,1220608,4096,16384,1220608]
[net.tcp.buffersize.lte]: [524288,1048576,2097152,262144,524288,1048576]
[net.tcp.buffersize.umts]: [4094,87380,110208,4096,16384,110208]
[net.tcp.buffersize.wifi]: [524288,2097152,4194304,262144,524288,1048576]
[net.tcp.default_init_rwnd]: [60]
[net.tcp.delack.default]: [1]
[net.tcp.delack.lte]: [8]
[net.tcp.usercfg.default]: [0]
[net.tcp.usercfg.lte]: [1]
[net.tcp.usercfg.wifi]: [1]
[persist.adb.tcp.port]: [10242]
[persist.audio.fluence.speaker]: [false]
[persist.audio.fluence.voicecall]: [false]
[persist.audio.fluence.voicerec]: [false]
[persist.build.cust.led.group]: [LED_D_GROUP]
[persist.camera.capture.animate]: [1]
[persist.camera.preview.size]: [0]
[persist.camera.qcom.misc]: [0]
[persist.camera.tintless]: [enable]
[persist.camera.tn.disable]: [0]
[persist.cne.feature]: [4]
[persist.cpe.gw.dhcp.end]: [192.168.100.254]
[persist.cpe.gw.dhcp.leasetime]: [3h]
[persist.cpe.gw.dhcp.start]: [192.168.100.2]
[persist.cpe.gw.dhcp.type]: [dhcp]
[persist.cpe.gw.eth.type]: [lan]
[persist.cpe.gw.ip]: [192.168.100.1]
[persist.cpe.gw.netmask]: [255.255.255.0]
[persist.cpe.wifi.pword]: [1234567890]
[persist.cpe.wifi.ssid]: [4G-MIFI-]
[persist.data.netmgrd.qos.enable]: [true]
[persist.debug.wfd.enable]: [0]
[persist.demo.hdmirotationlock]: [false]
[persist.dpm.feature]: [3]
[persist.elink.sim.count]: [1]
[persist.env.c.phone.matchnum]: [11]
[persist.fuse_sdcard]: [true]
[persist.gps.qc_nlp_in_use]: [1]
[persist.hwc.mdpcomp.enable]: [true]
[persist.loc.nlp_name]: [com.qualcomm.services.location]
[persist.radio.VT_ENABLE]: [1]
[persist.radio.VT_HYBRID_ENABLE]: [1]
[persist.radio.adb_log_on]: [0]
[persist.radio.airplane_mode_on]: [0]
[persist.radio.apm_sim_not_pwdn]: [1]
[persist.radio.calls.on.ims]: [true]
[persist.radio.csvt.enabled]: [false]
[persist.radio.custom_ecc]: [1]
[persist.radio.dsdx]: [true]
[persist.radio.eons.enabled]: [false]
[persist.radio.ignore_dom_time]: [5]
[persist.radio.jbims]: [1]
[persist.radio.lte_vrte_ltd]: [1]
[persist.radio.mt_sms_ack]: [20]
[persist.radio.multisim.config]: [ssss]
[persist.radio.network_feature]: [8]
[persist.radio.nitz_lons_0_0]: [RYZE]
[persist.radio.nitz_lons_1_0]: []
[persist.radio.nitz_lons_2_0]: []
[persist.radio.nitz_lons_3_0]: []
[persist.radio.nitz_plmn_0]: [470 03]
[persist.radio.nitz_sons_0_0]: [RYZE]
[persist.radio.nitz_sons_1_0]: []
[persist.radio.nitz_sons_2_0]: []
[persist.radio.nitz_sons_3_0]: []
[persist.radio.rat_on]: [combine]
[persist.radio.restore_mode_pref]: [1]
[persist.rild.nitz_long_ons_0]: []
[persist.rild.nitz_long_ons_1]: []
[persist.rild.nitz_long_ons_2]: []
[persist.rild.nitz_long_ons_3]: []
[persist.rild.nitz_plmn]: []
[persist.rild.nitz_short_ons_0]: []
[persist.rild.nitz_short_ons_1]: []
[persist.rild.nitz_short_ons_2]: []
[persist.rild.nitz_short_ons_3]: []
[persist.sys.dalvik.vm.lib]: [libdvm.so]
[persist.sys.logkit.ctrlcode]: [1]
[persist.sys.profiler_ms]: [0]
[persist.sys.silent]: [1]
[persist.sys.ssr.restart_level]: [modem]
[persist.sys.strict_op_enable]: [false]
[persist.sys.timezone]: [Asia/Dhaka]
[persist.sys.usb.config.extra]: [serial_smd]
[persist.sys.usb.config]: [diag,serial_smd,rmnet_bam,adb]
[persist.sys.whitelist]: [/system/etc/whitelist_appops.xml]
[persist.telephony.oosisdc]: [false]
[persist.timed.enable]: [true]
[persist.ufi.card.plug]: [yes]
[persist.ufi.collect.sim]: []
[persist.ufi.freq.band]: []
[persist.ufi.ft.haveeth]: [0]
[persist.ufi.ft.only_sn]: [0]
[persist.ufi.ft.server]: [NONE]
[persist.ufi.ft.simsw]: [0]
[persist.ufi.ft.simsw_pw]: [0]
[persist.ufi.ft.simswitchpword]: [zx]
[persist.ufi.ft.weblogo]: [NORMAL]
[persist.ufi.ft.withmtp]: [0]
[persist.ufi.ft.write_imei]: [1]
[persist.ufi.name.imei.suffix]: [no]
[persist.ufi.nosignal.reboot]: [no]
[persist.ufi.oem.name]: [ZX]
[persist.ufi.ping.router]: []
[persist.ufi.qhyl.light]: []
[persist.ufi.qhyl.switchsim]: []
[persist.ufi.signal.check]: [yes]
[persist.ufi.sim.pooling]: [no]
[persist.ufi.sim.prior]: [DD]
[persist.ufi.sn.auth.service]: [1]
[persist.ufi.test.light]: [yes]
[persist.ufi.wifi.light]: [yes]
[persist.web.default.lang]: [en]
[persist.web.login.password]: [admin]
[persist.wlan.imei.fromnv]: [000000041775022]
[persist.wlan.mac.fromnv]: [5c:a0:01:5b:1d:f0]
[persist.ykm.light.ctrl]: []
[ril.ecclist]: [911,*911,#911,112,000,08,110,999,118,119]
[ril.qcril_pre_init_lock_held]: [0]
[ril.subscription.types]: [NV,RUIM]
[rild.libargs]: [-d /dev/smd0]
[rild.libpath]: [/system/vendor/lib/libril-qc-qmi-1.so]
[ro.alarm_boot]: [false]
[ro.allow.mock.location]: [0]
[ro.baseband]: [msm]
[ro.bluetooth.dun]: [true]
[ro.bluetooth.hfp.ver]: [1.6]
[ro.bluetooth.sap]: [true]
[ro.board.platform]: [msm8916]
[ro.boot.baseband]: [msm]
[ro.boot.bootdevice]: [7824900.sdhci]
[ro.boot.console]: [ttyHSL0]
[ro.boot.emmc]: [true]
[ro.boot.hardware]: [qcom]
[ro.boot.selinux]: [permissive]
[ro.boot.serialno]: [13a06a2a]
[ro.bootloader]: [unknown]
[ro.bootmode]: [unknown]
[ro.build.characteristics]: [default]
[ro.build.cust_proj]: [YL_MF601_D]
[ro.build.date.utc]: [1704792440]
[ro.build.date]: [2024年 01月 09日 星期二 17:27:20 CST]
[ro.build.description]: [msm8916_32_512-userdebug 4.4.4 KTU84P eng.zhongxingfeng.20240109 test-keys]
[ro.build.display.id]: [msm8916_32_512-userdebug 4.4.4 KTU84P eng.zhongxingfeng.20240109 test-keys]
[ro.build.factory]: [no]
[ro.build.host]: [elinksrv3]
[ro.build.hw.version]: [HW1.3]
[ro.build.id]: [KTU84P]
[ro.build.lcd_direction]: [LCD_GH]
[ro.build.lcd_type]: [128X128]
[ro.build.model_type]: [MF601STC]
[ro.build.product]: [msm8916_32_512]
[ro.build.sw.custom.version]: [MF601STC_D_V03_ZX_DD_N_240109]
[ro.build.tags]: [test-keys]
[ro.build.type]: [userdebug]
[ro.build.user]: [zhongxingfeng]
[ro.build.version.codename]: [REL]
[ro.build.version.incremental]: [eng.zhongxingfeng.20240109]
[ro.build.version.release]: [4.4.4]
[ro.build.version.sdk]: [19]
[ro.carrier]: [unknown]
[ro.com.android.dataroaming]: [true]
[ro.com.android.dateformat]: [MM-dd-yyyy]
[ro.config.alarm_alert]: [Alarm_Classic.ogg]
[ro.config.low_ram]: [true]
[ro.config.notification_sound]: [pixiedust.ogg]
[ro.config.pppoe_enable]: [1]
[ro.config.ringtone]: [Ring_Synth_04.ogg]
[ro.config.zram]: [true]
[ro.crypto.state]: [unencrypted]
[ro.debuggable]: [1]
[ro.factorytest]: [0]
[ro.fm.transmitter]: [false]
[ro.gps.agps_provider]: [1]
[ro.hardware]: [qcom]
[ro.min_freq_0]: [800000]
[ro.opengles.version]: [196608]
[ro.pip.gated]: [0]
[ro.product.board]: [msm8916]
[ro.product.brand]: [qcom]
[ro.product.cpu.abi2]: [armeabi]
[ro.product.cpu.abi]: [armeabi-v7a]
[ro.product.device]: [msm8916_32_512]
[ro.product.locale.language]: [en]
[ro.product.locale.region]: [US]
[ro.product.manufacturer]: [unknown]
[ro.product.model]: [msm8916_32_512]
[ro.product.name]: [msm8916_32_512]
[ro.qc.sdk.audio.fluencetype]: [none]
[ro.qc.sdk.audio.ssr]: [false]
[ro.qualcomm.bluetooth.ftp]: [true]
[ro.qualcomm.bluetooth.hfp]: [true]
[ro.qualcomm.bluetooth.hsp]: [true]
[ro.qualcomm.bluetooth.map]: [true]
[ro.qualcomm.bluetooth.nap]: [true]
[ro.qualcomm.bluetooth.opp]: [true]
[ro.qualcomm.bluetooth.pbap]: [true]
[ro.qualcomm.bt.hci_transport]: [smd]
[ro.qualcomm.cabl]: [0]
[ro.revision]: [0]
[ro.ril.svdo]: [false]
[ro.ril.svlte1x]: [false]
[ro.runtime.firstboot]: [1207188027]
[ro.secure]: [1]
[ro.serialno]: [13a06a2a]
[ro.sf.lcd_density]: [114]
[ro.sys.fw.bg_apps_limit]: [16]
[ro.sys.usb.default.config]: [diag,serial_smd,rmnet_bam,adb]
[ro.telephony.call_ring.multiple]: [false]
[ro.telephony.default_cdma_sub]: [0]
[ro.telephony.default_network]: [12]
[ro.use_data_netmgrd]: [true]
[ro.vendor.extension_library]: [/vendor/lib/libqc-opt.so]
[ro.wifi.channels]: []
[service.adb.tcp.port]: [10242]
[service.bootanim.exit]: [1]
[swe.tile.height]: [128]
[swe.tile.maxtile]: [128]
[swe.tile.width]: [128]
[sys.boot_completed]: [1]
[sys.keymaster.loaded]: [true]
[sys.listeners.registered]: [true]
[sys.settings_global_version]: [3]
[sys.sysctl.extra_free_kbytes]: [204]
[sys.usb.config]: [rndis,serial_smd,adb]
[sys.usb.rps_mask]: [0]
[sys.usb.state]: [rndis,adb]
[sys.usb.tethering]: [true]
[telephony.lteOnCdmaDevice]: [1]
[tunnel.audio.encode]: [false]
[usb_uicc.enabled]: [0]
[usb_uicc.loading]: [1]
[use.voice.path.for.pcm.voip]: [false]
[vidc.enc.narrow.searchrange]: [1]
[vold.post_fs_data_done]: [1]
[wifi.interface]: [wlan0]
[wlan.driver.ath]: [0]
[wlan.driver.config]: [/data/misc/wifi/WCNSS_qcom_cfg.ini]
[wlan.driver.status]: [ok]
```

</details>
