# 4g-lte-router


┌─[mrs@parrot]─[~]
└──╼ ```$adb devices```
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
13a06a2a	device

┌─[mrs@parrot]─[~]
└──╼ $```adb shell getprop ro.product.model
adb shell getprop ro.build.version.release```
msm8916_32_512
4.4.4
┌─[mrs@parrot]─[~]
└──╼ $```adb shell getprop ro.product.manufacturer
adb shell getprop ro.product.brand
adb shell getprop ro.product.name
adb shell getprop ro.product.device
adb shell getprop ro.product.model```
unknown
qcom
msm8916_32_512
msm8916_32_512
msm8916_32_512
┌─[mrs@parrot]─[~]
└──╼ $```adb shell getprop ro.build.display.id
adb shell getprop ro.build.description
adb shell getprop ro.build.fingerprint```
msm8916_32_512-userdebug 4.4.4 KTU84P eng.zhongxingfeng.20240109 test-keys
msm8916_32_512-userdebug 4.4.4 KTU84P eng.zhongxingfeng.20240109 test-keys

┌─[mrs@parrot]─[~]
└──╼ $```adb shell uname -a```
/system/bin/sh: uname: not found
┌─[mrs@parrot]─[~]
└──╼ $```adb shell cat /proc/cpuinfo
adb shell cat /proc/meminfo | head -5```
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
MemTotal:         402336 kB
MemFree:           45968 kB
Buffers:           13012 kB
Cached:           193156 kB
SwapCached:            0 kB
┌─[mrs@parrot]─[~]
└──╼ $

