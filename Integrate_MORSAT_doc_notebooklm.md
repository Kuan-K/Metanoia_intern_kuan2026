readme.md

# 📚 MOSART Documentation Portal

Welcome to the unified documentation hub for MOSART and the Cobra SoC Platform.

---

## 🛠 MOSART SDK

### 📖 [MOSART Introduction](mosart-introduction.md)
Overview of the MOSART open-source SDK, architecture, and objectives.

### 🚀 Quick Start Guides
- [MOSART Yocto Build Quick Start](mosart-cobra-yocto-quickstart.md)
  A quick guide to building a bootable Yocto image for the Cobra EVB.
- [MOSART Yocto Quick Sanity Test](mosart-cobra-yocto-quick-sanity-check.md)
  A quick guide to performing sanity tests on the Cobra EVB.

### ⚙️ [MOSART Yocto Guide](mosart-yocto.md)
Yocto layers, recipes, build configuration, and image creation.

### 🏗️ [MOSART Platform Software](mosart-platform.md)
MOSART platform software design and architecture.

---

## 🧩 Cobra SoC Platform

### 🐍 [Cobra SoC Overview](cobra-soc-overview.md)
Architecture, subsystem descriptions, processing blocks, and hardware integration.

### 🚧 Cobra SoC Development Public Documentation
Coming Soon!

---

# 📜 License

Licensed under the Apache License 2.0. See the
[LICENSE](LICENSE) file for details.

# ™️ Trademark

[MOSART™](TRADEMARK.md) is a trademark of Metanoia Communications Inc.



[MOSART Documentation Portal Home](README.md)

<details>
<summary><strong>Table of Contents</strong></summary>

- [1. Introduction](#1-introduction)
- [2. Key Features](#2-key-features)
- [3. Major Subsystems Summary](#3-major-subsystems-summary)
- [4. Software Architecture](#4-software-architecture)
- [5. O-RU System Integration](#5-o-ru-system-integration)
- [6. Boot Flow](#6-boot-flow)
- [7. Timing & Synchronization](#7-timing--synchronization)
- [8. RFIC Integration (Yucca)](#8-rfic-integration-yucca)
- [9. Application Use Cases](#9-application-use-cases)
- [10. Summary](#10-summary)

</details>

# Cobra SoC Overview
*Metanoia MT2824 — 5G O-RU Digital Front-End System-on-Chip*

---

## 1. Introduction
The **Metanoia Cobra™ MT2824 SoC** is a next-generation, fully software-programmable 5G/B5G/6G Digital Front-End (DFE) System-on-Chip designed to enable highly flexible, cost-efficient, and standards-compliant **O-RAN Radio Units (RUs)**. Built on a scalable, software-defined architecture, Cobra supports **O-RAN split 7.2x**, disaggregated small-cell platforms, and advanced SDR research and development environments.

Cobra integrates the entire O-RU signal-processing chain—including fronthaul transport, low-PHY acceleration, digital predistortion (DPD), timing and synchronization, calibration workflows, and system management—into a compact, low-power SoC optimized for commercial deployment.

At its core, Cobra incorporates a heterogeneous compute subsystem composed of **six Cadence B20 DSP vector processors**, **five Cadence LX7 real-time controllers**, and a **dual-core RISC-V RV64 processor complex**. This architecture is purpose-built for deterministic, high-throughput radio processing. Complementing this compute fabric, Cobra integrates an **LPDDR4 memory controller** and a **dual-lane 25G network subsystem** capable of handling O-RAN S-Plane, M-Plane, and eCPRI (CU-Plane) traffic with real-time, low-latency guarantees. Through its high-speed SerDes interface, Cobra ingests packets from external SFP+ modules and routes them to the network engine and the **Metanoia Radio Acceleration Subsystem (MRAS)** for real-time baseband and radio processing.

The SoC also provides a rich set of peripheral interfaces—including **LVDS, I²C, QSPI, SPI, UART, GPIO, USB, SD/eMMC, and NOR flash**—ensuring seamless integration with RFICs, analog front-end modules, board-level control components, and storage devices.

---

## 2. Key Features
### 2.1 Processing Architecture
- Dual-core **RISC-V AX45MP** (64-bit, MMU)
- **5× Cadence LX7** RTOS cores
- **6× Cadence B20 DSPs** for low-PHY & DFE
- **2× DPD Inline Accelerators**
- Integrated **AFE** subsystem with ADC/DAC and PVT sensors

### 2.2 O-RAN Fronthaul Support
- Dual 10G/25G SerDes
- eCPRI encapsulation/decapsulation
- O-RAN eCPRI Split 7.2x Section Types 0/1/3
- Dynamic & static compression (8/12-bit)
- Timing windows compliant with O-RAN fronthaul profiles

### 2.3 Memory & Storage
- LPDDR4 memory controller
- eMMC/SD, QSPI NOR
- Internal SRAM/TCM memories

### 2.4 Peripheral Subsystems
- I2C, SPI, UART, USB2.0
- GPIO, GNSS, PTP
- LVDS RF control interface

---

## 3. Major Subsystems Summary
Major subsystems:
- **RISC-V CPU complex**
- **DSP vector processor complex**
- **LX7 RTOS subsystem**
- **Network Interface Subsystem (NIS)**: MAC/PCS, MACSec
- **DFE subsystem**: filters, compression, CFR, DPD
- **AFE IQ Bridge (IQB)**
- **Memory subsystem**
- **Boot/security subsystem**

---

## 4. Software Architecture
### 4.1 Operating System and Build Systems
The Cobra platform is built on a modern, flexible, and scalable Linux-based environment that supports multiple embedded build systems and secure boot mechanisms. The software stack includes:

#### 4.1.1 Linux Kernel
- **Linux Kernel 6.1 LTS or newer**
- Long-term–supported kernel with optimized drivers for Cobra SoC (DFE, MRAS, AFE, SerDes, peripherals)
- Supports upstream alignment for long-term maintainability

#### 4.1.2 Yocto Project (Primary Build System)
- **Yocto Project 5.0 (Kirkstone)**
- Officially supported and recommended for production firmware images
- Provides reproducible builds, package management, and long-term BSP integration

#### 4.1.3 Buildroot (Optional)
- [Metanoia Buildroot](mosart-buildroot.md) - Lightweight alternative build system for minimal root filesystem creation
- Ideal for rapid prototyping, testing, or constrained deployments

#### 4.1.4 Raspberry Pi Build Environment (Optional)
- External SBC-based environment used for early-stage development and evaluation
- Supports cross-development workflows when hardware access is limited

#### 4.1.5 Boot Chain and Secure Boot
- **OpenSBI**: RISC-V Supervisor Mode initialization and runtime services
- **U-Boot**: Secondary bootloader supporting kernel loading, flashing, and diagnostics
- [MTF (Metanoia Trusted Firmware)](cobra-mtf.md):
  - Implements secure boot
  - Validates ROTPK and authenticates early-stage boot components
  - Provides platform root of trust


### 4.2 Management and Time Synchronization Software

#### Overview
The Management and Time Synchronization Software in the Cobra O-RU architecture provides the management services needed for:
- O-RAN M-Plane configuration  
- Time synchronization (PTP/GNSS/holdover)  
- Notifications, Fault Management, and Performance reporting  
- NETCONF transport and YANG data modeling  
- Integration between Sysrepo datastore and internal RU subsystems  

It coordinates:
- NETCONF/YANG  
- mplaned  
- SysrepoHook  
- RU Manager  
- MRAS timing subsystem  

#### 4.2.1 Functional Responsibilities

##### Configuration Management
- Receives NETCONF edit-config  
- Validates via YANG  
- Updates internal configuration tree  
- Propagates changes to MRAS and system backend

##### Time Synchronization Management
Manages:
- PTP  
- GNSS  
- Holdover  
- DFET alignment  
- Timing state machine  

##### Fault & Performance Management
- Fault/Alarm collection  
- Performance KPI counters  
- M-Plane alarm notifications  

#### 4.2.2 Software Components

##### mplaned
Main M-Plane monitoring background daemon.

##### SysrepoHook
Central dispatcher for YANG updates.

##### O-RAN Module Plugins
Implements handlers, RPC callbacks, and operational providers.

#### 4.2.3 Time Synchronization Workflow

##### Configuration Flow
1. DU sends edit-config  
2. Netopeer2 → Sysrepo  
3. SysrepoHook triggers plugin  
4. Plugin validates and updates RU Manager  
5. RU Manager applies PTP/GNSS/holdover/DFET  
6. Updates returned to YANG operational  

##### Operational Monitoring Flow
- RU Manager collects PPS stability, jitter, GNSS lock  
- MRAS provides timing counters  
- SysrepoHook publishes operational data  

#### 4.2.4 NETCONF/YANG Interfaces

##### Synchronization Nodes
- sync-source  
- ptp-profile  
- clock-class  
- time-of-day  
- gnss-status  
- sync-state  

##### Alarms
- GNSS lost  
- PTP unlocked  
- PPS errors  

#### 4.2.5 Integration with RU Manager / MRAS
M-Plane config → SysrepoHook → RU Manager → MRAS Timing/DFET/Clock Synthesizer.

#### 4.2.6 Standards Compliance
Implements O-RAN WG4 Time-Sync and related synchronization requirements.


### 4.3 **MRAS** Data/Radio Processing Software
- Low PHY (FFT/iFFT, DMRS, PRACH)
- Filters, compression
- DPD/CFR

### 4.4 IPC Between Linux & MRAS
- OpenAMP messaging
- Shared memory MIB

---

## 5. O-RU System Integration
### 5.1 M-Plane
- Startup Configuration and Zero Touch Provisioning (ZTP)
- SW mgmt
- Fault/Performance mgmt
- O-RAN YANG models compliant

### 5.2 S-Plane
- IEEE 1588v2 PTP (Class B capable)
- GNSS fallback
- DFE timer alignment

### 5.3 C/U Planes
- Real-time software defined radio processing
- Header parsing
- Low-PHY compute
- Window alignment & eAxC separation

---

## 6. Boot Flow
1. [MTF (Metanoia Trusted Firmware)](cobra-mtf.md)
2. SPL (DDR init and initial system setup)
3. U-Boot
4. Linux Kernel
5. Platform drivers
6. RootFS init
7. MRAS/DSP boot
8. RU Manager starts
9. Calibration
10. O-RU ready

---

## 7. Timing & Synchronization
- DFE Timer (DFET) for deterministic timing
- GNSS/1588v2 support
- SyncE option
- 3GPP frame alignment

---

## 8. RFIC Integration (Yucca)
- LVDS-based control
- Supports 2x2 TDD/FDD
- FR1 and FR2 IF support
- Calibrations:
  - LO leakage
  - IQ imbalance
  - DC offset
  - Filter bandwidth
  - PA bias/DPD

---

## 9. Application Use Cases
### 9.1 FR1
- 2T2R to 16T16R O-RUs
- RedCap radios

### 9.2 FR2
- 2T2R / 4T4R mmWave RUs
- External mmWave FE integration

### 9.3 Small Cell / Femto
- Cost-optimized 2T2R
- Enterprise/indoor deployments

---

## 10. Summary
Cobra MT2824 is a **high-integration SDR SoC** optimized for O-RU deployments requiring:
- High compute performance
- Software-defined flexibility
- Low power & high integration
- 3GPP/O-RAN compliance

It substantially reduces time-to-market and supports a scalable architectural roadmap that enables smooth progression from 5G deployments toward B5G and 6G technologies.


<details>
<summary><strong>Table of Contents</strong></summary>

- [MOSART Cobra SoC Quick Sanity Validation Guide](#mosart-cobra-soc-quick-sanity-validation-guide)
  - [Standalone RU Validation](#standalone-ru-validation)
  - [Expected Duration](#expected-duration)
  - [Environment Assumptions](#environment-assumptions)
  - [What This Verifies](#what-this-verifies)
    - [Linux Platform Health](#linux-platform-health)
    - [M-Plane Startup](#m-plane-startup)
    - [Verify O-RU Readiness](#verify-o-ru-readiness)
    - [DSP / Baseband Readiness](#dsp--baseband-readiness)
  - [Detailed Quick Instructions](#detailed-quick-instructions)
    - [Test Actions](#test-actions)
    - [Board Setup](#board-setup)
    - [Power-On Flow and Linux Console Login](#power-on-flow-and-linux-console-login)
    - [Update RU Manager Configuration for Quick Sanity Test](#update-ru-manager-configuration-for-quick-sanity-test)
    - [Check MRAS Running Time Status](#check-mras-running-time-status)
  - [Common Issues](#common-issues)
  - [Next Steps / Further Validation](#next-steps--further-validation)

</details>

# MOSART Cobra SoC Quick Sanity Validation Guide

## Standalone RU Validation

This document describes a basic standalone Radio Unit (RU) validation
procedure intended to verify that the software image, hardware
platform, and DSP processing pipeline are operating correctly.

This procedure validates basic software, DSP, and platform readiness
only and is not intended to replace full interoperability,
performance, RF OTA, or carrier certification testing.

The scope focuses on quick sanity testing of the MOSART software stack
and Cobra SoC evaluation platform, including successful boot,
firmware loading, DSP initialization, RF subsystem readiness, and
basic platform health checks.

This validation flow is intended for initial platform bring-up,
development verification, and software image sanity confirmation.

For comprehensive end-to-end (E2E) system testing — including CU/DU
integration, UE interoperability, O-RAN fronthaul validation, PTP
server setup, synchronization verification, and performance
evaluation — please contact:

https://metanoia-comm.com/contact/

## Expected Duration

Typical execution time for this quick sanity validation is
approximately 5–10 minutes.

## Environment Assumptions

- No DU traffic connected
- No UE attached
- No S-Plane and no PTP master

## What This Verifies

### Linux Platform Health

- Confirms successful boot flow and that the operating system is up and stable.
- Allows the use of standard Linux utilities to inspect and validate the software stack.

### M-Plane Startup

- Verifies successful M-Plane initialization and control flow.

### Verify O-RU Readiness

- Verifies that the MRAS and DSP images are successfully loaded and running.

### DSP / Baseband Readiness

- Confirms that the DSP and baseband processing are running.
- Verifies that the O-RU is in a ready state and waiting for traffic.
- Indicates readiness for live DL/UL traffic once external entities are connected.

# Detailed Quick Instructions

## Test Actions

- Connect all required cables to the Cobra EVB board and insert the SD card containing the Cobra software image.
- Configure the board jumpers correctly and set the boot mode to SD.
- Power on the board.
- Log in to the Linux console via the UART terminal.
- Start the RU Manager.
- Bring the RU to the **Active** state.
- Display DSP CU-Plane traffic status via the Linux console.

## Board Setup

Connect all required cables to the Cobra EVB, as shown below:

![Cabling to Cobra EVB](cobra-evb-console-eth-power-connection.jpg)

Ethernet network connectivity is optional for this standalone sanity
validation flow.

Locate the boot source switch on the board and configure it to boot
from the SD card.

Refer to [Cobra MTF Boot Source Pinstrap](cobra-mtf.md#cobra-soc-boot-sources-and-cobra-evb-bootstrap-pins)
for details.

- **Boot from SD:** `01`

The switch configuration should appear as follows:

![Boot From SD](boot-from-sd-setting.jpeg)

## Power-On Flow and Linux Console Login

Connect to the Cobra EVB console using **minicom**, **tio**, or another terminal utility.

For example, assuming the UART is connected to `/dev/ttyUSB1` on the
host machine, run:

```bash
sudo minicom -D /dev/ttyUSB1
```

**Note**: The default serial console settings should work. You may verify them in the minicom serial port settings screen:
```
    | A -    Serial Device      : /dev/ttyUSB1                              |                                   
    | B - Lockfile Location     : /var/lock                                 |                                   
    | C -   Callin Program      :                                           |                                   
    | D -  Callout Program      :                                           |                                   
    | E -    Bps/Par/Bits       : 115200 8N1                                |                                   
    | F - Hardware Flow Control : No                                        |                                   
    | G - Software Flow Control : No                                        |                                   
    | H -     RS485 Enable      : No                                        |                                   
    | I -   RS485 Rts On Send   : No                                        |                                   
    | J -  RS485 Rts After Send : No                                        |                                   
    | K -  RS485 Rx During Tx   : No                                        |                                   
    | L -  RS485 Terminate Bus  : No                                        |                                   
    | M - RS485 Delay Rts Before: 0                                         |                                   
    | N - RS485 Delay Rts After : 0                                         |                                   
    |                                                                       |                                   
    |    Change which setting?                    
```

If the board is set up correctly, the UART console will prompt for login.
Log in using the username root and the default password 12345, as shown below.

```
U-Boot SPL 2023.01 (Jan 02 2026 - 07:13:31 +0000)
Device ID: SHUTTLE (0x28240000)
Chip ID 0000
Board ID: 10
DDRPHY: Training has run successfully (firmware complete)
DDRPHY: Training has run successfully (firmware complete)
Trying to boot from MMC1

OpenSBI v1.2
   ____                    _____ ____ _____
  / __ \                  / ____|  _ \_   _|
 | |  | |_ __   ___ _ __ | (___ | |_) || |
 | |  | | '_ \ / _ \ '_ \ \___ \|  _ < | |
 | |__| | |_) |  __/ | | |____) | |_) || |_
  \____/| .__/ \___|_| |_|_____/|____/_____|
        | |
        |_|

Platform Name             : Metanoia MT58xx Cobra EVB board
Platform Features         : medeleg
Platform HART Count       : 2
Platform IPI Device       : andes_plicsw
Platform Timer Device     : andes_plmt @ 20000000Hz
Platform Console Device   : uart8250
Platform HSM Device       : ---
Platform PMU Device       : andes_pmu
Platform Reboot Device    : mta58xx
Platform Shutdown Device  : ---
Firmware Base             : 0x80000000
Firmware Size             : 244 KB
Runtime SBI Version       : 1.0

Domain0 Name              : root
Domain0 Boot HART         : 0
Domain0 HARTs             : 0*,1*
Domain0 Region00          : 0x0000000080000000-0x000000008003ffff ()
Domain0 Region01          : 0x000000000c400000-0x000000000c7fffff (I,R)
Domain0 Region02          : 0x000000000c800000-0x000000000cbfffff (I)
Domain0 Region03          : 0x0000000000000000-0xffffffffffffffff (R,W,X)
Domain0 Next Address      : 0x0000000081200000
Domain0 Next Arg1         : 0x0000000081100000
Domain0 Next Mode         : S-mode
Domain0 SysReset          : yes

Boot HART ID              : 0
Boot HART Domain          : root
Boot HART Priv Version    : v1.11
Boot HART Base ISA        : rv64imafdcnx
Boot HART ISA Extensions  : none
Boot HART PMP Count       : 32
Boot HART PMP Granularity : 8
Boot HART PMP Address Bits: 36
Boot HART MHPM Count      : 4
Boot HART MHPM Bits       : 64
Boot HART MIDELEG         : 0x0000000000000222
Boot HART MEDELEG         : 0x000000000000b109


U-Boot 2023.01 (Jan 02 2026 - 07:13:31 +0000)

DRAM:  Overwrite PLL clock 900000000 for MT28XX(0)
2 GiB (effective 4 GiB)
Core:  40 devices, 22 uclasses, devicetree: board
WDT:   Not starting wdt@10090000
Flash: 0 Bytes
MMC:   mmc@4100000: 0
Loading Environment from MMC... OK
In:    serial@100e0000
Out:   serial@100e0000
Err:   serial@100e0000
Net:   eth0: ethernet@12100000, eth1: ethernet@12120000
Hit any key to stop autoboot:  3  2  1  0 
switch to partitions #0, OK
mmc0 is current device
mmc_ready: check MMC dev 0 0
switch to partitions #0, OK
mmc0 is current device
MMC ready
get_kern0: kernel0 partition info
kernel0: start=8000, size=10000
Use kernel0, rootdev=/dev/mmcblk0p5
load_imgs: fit_addr=0x83000000, start=8000, size=10000
mmc_ready: check MMC dev 0 0
switch to partitions #0, OK
mmc0 is current device
MMC ready

MMC read: dev # 0, block # 32768, count 65536 ... 65536 blocks read: OK
mmc read OK
## Loading kernel from FIT Image at 83000000 ...
   Using 'conf-mt58xx-cobra-evb.dtb' configuration
   Trying 'kernel-1' kernel subimage
     Description:  Linux kernel
     Type:         Kernel Image
     Compression:  gzip compressed
     Data Start:   0x830000e4
     Data Size:    5265325 Bytes = 5 MiB
     Architecture: RISC-V
     OS:           Linux
     Load Address: 0x82000000
     Entry Point:  0x82000000
     Hash algo:    sha256
     Hash value:   ea230dcec552eddcec989db7e2c3f6c848284ee90a70d272eed4bf3020d389a8
   Verifying Hash Integrity ... sha256+ OK
## Loading fdt from FIT Image at 83000000 ...
   Using 'conf-mt58xx-cobra-evb.dtb' configuration
   Trying 'fdt-mt58xx-cobra-evb.dtb' fdt subimage
     Description:  Flattened Device Tree blob
     Type:         Flat Device Tree
     Compression:  uncompressed
     Data Start:   0x835059ac
     Data Size:    22931 Bytes = 22.4 KiB
     Architecture: RISC-V
     Load Address: 0x68010000
     Hash algo:    sha256
     Hash value:   1e85b58f93780cd74080819a37017009b53888156f2c37235ca46262c48b8afd
   Verifying Hash Integrity ... sha256+ OK
   Loading fdt from 0x835059ac to 0x68010000
   Booting using the fdt blob at 0x68010000
Working FDT set to 68010000
   Uncompressing Kernel Image
   Loading Device Tree to 0000000083ff7000, end 0000000083fff992 ... OK
Working FDT set to 83ff7000
Overwrite PLL clock 900000000 for MT28XX(0)

Starting kernel ...
.....

[   25.620096] IPv6: ADDRCONF(NETDEV_CHANGE): eth0: link becomes ready

Cobra-SDK 1.0.0 1767769208 mt58xx-cobra-evb ttyS0

mt58xx-cobra-evb login: 
Password: 
```

- **NOTE 1:** A few lines of garbled characters may appear immediately
after power-on due to a minor UART configuration mismatch on the
current evaluation board. This is a known issue. There are
workaround fixes but they are not recommended at this time. The UART
baud rate on the current EVB is initially set to 96000 during
- **Note 2:** The `"......"`  in the above log output indicates content
intentionally omitted for readability.

## Update RU Manager Configuration for Quick Sanity Test

The following settings disable calibration dependencies and external
timing lock requirements to simplify standalone platform validation.

Before modifying the configuration, create a backup copy:
```bash
cp /etc/rumanager.conf /etc/rumanager.conf.backup
```

Disable DPD and PTP clock re-adjustment to simplify the setup for a
quick sanity test.

For full end-to-end (E2E) testing — including 5GC, CU/DU, PTP server,
and UE interoperability — please contact Metanoia support for
additional configuration guidance.

Follow the steps below to update rumanager.conf, then restart the RU
Manager and MRAS services:

```bash
root@mt58xx-cobra-evb:~# sed -i 's/"cali_cfg": *"[^"]*"/"cali_cfg": "0x3f"/' /etc/rumanager.conf
root@mt58xx-cobra-evb:~# sed -i 's/"skip_lock":[[:space:]]*\(true\|false\)/"skip_lock": true/' /etc/rumanager.conf
root@mt58xx-cobra-evb:~# systemctl stop rumanager
root@mt58xx-cobra-evb:~# systemctl stop mras
[   57.001714] remoteproc remoteproc0: powering up mras
[   57.266662] remoteproc remoteproc0: Booting fw image rproc-mras-fw, size 1338173
[   57.274679] remoteproc remoteproc0: Loading resource table from FW file
[   57.287220] remoteproc remoteproc0: metanoia_rproc_elf_load_segments: rsc_table from priv table
[   57.300370] remoteproc remoteproc0: Skip loading resource table from FW file
[   57.307555] remoteproc remoteproc0: Skip loading resource table from FW file
[   57.314635] remoteproc remoteproc0: Skip loading resource table from FW file
[   57.322195] remoteproc remoteproc0: metanoia_rproc_start
[   57.437781] rproc-virtio rproc-virtio.0.auto: assigned reserved memory node vdev0buffer@90008000
[   57.448167] virtio_rpmsg_bus virtio0: rpmsg host is online
[   57.453871] rproc-virtio rproc-virtio.0.auto: registered virtio0 (type 7)
[   57.460854] remoteproc remoteproc0: remote processor mras is now up
[   57.483195] virtio_rpmsg_bus virtio0: creating channel rpmsg-tty addr 0x400
[   57.490988] virtio_rpmsg_bus virtio0: creating channel rpmsg-raw addr 0x401
[   57.498774] virtio_rpmsg_bus virtio0: creating channel rpmsg-raw addr 0x402
root@mt58xx-cobra-evb:~# 
root@mt58xx-cobra-evb:~# 
root@mt58xx-cobra-evb:~# systemctl start rumanager
```

## Check MRAS Running Time Status

You may use the DSP console to monitor DSP/MRAS running status, or
simply monitor through the Linux console by running:

```bash
root@mt58xx-cobra-evb:~# cat /dev/dsp-console >> dsp-console.log &
[1] 557
root@mt58xx-cobra-evb:~# tail -f dsp-console.log
```

The console will display a prolog followed by a table of CU-Plane
traffic statistics. The display refreshes every few seconds.

Without live traffic connected, the counters are expected to remain
zero. This is normal behavior during standalone sanity validation.

```bash
                       |      Port#0     |      Port#1     |      Port#2     |      Port#3     |
-----------------------+-----------------+-----------------+-----------------+-----------------+
DL CPlane Total        |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL CPlane OnTime       |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL CPlane Early        |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL CPlane Late         |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL CPlane SeqId        |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL UPlane Total        |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL UPlane OnTime       |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL UPlane Early        |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL UPlane Late         |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
DL UPlane SeqId        |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
-----------------------+-----------------+-----------------+-----------------+-----------------+
DL RF / fine Gain (dB) |      0 /  -0.00 |      0 /  -0.00 |      0 /  -0.00 |      0 /  -0.00 |
DL Avg / Max dBFS (dB) |              NA |              NA |              NA |              NA |
DL Estimate Power(dBm) |              NA |              NA |              NA |              NA |
-----------------------+-----------------+-----------------+-----------------+-----------------+
UL PUSCH CPlane Total  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PUSCH CPlane OnTime |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PUSCH CPlane Early  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PUSCH CPlane Late   |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PUSCH CPlane SeqId  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PUSCH UPlane Total  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
-----------------------+-----------------+-----------------+-----------------+-----------------+
UL PRACH CPlane Total  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PRACH CPlane OnTime |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PRACH CPlane Early  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PRACH CPlane Late   |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PRACH CPlane SeqId  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
UL PRACH UPlane Total  |      0x00000000 |      0x00000000 |      0x00000000 |      0x00000000 |
-----------------------+-----------------+-----------------+-----------------+-----------------+
UL RF Gain             |            0x34 |            0x34 |            0x34 |            0x34 |
UL Avg / Max dBFS (dB) |              NA |              NA |              NA |              NA |
UL Estimate Power(dBm) |              NA |              NA |              NA |              NA |
UL RSSI Power(dBm)     |              NA |              NA |              NA |              NA |
FW: rproc-mras-fw-3.0.0.26010711200, Showtime 9 seconds
```
The above status table indicates successful standalone RU
initialization and that the platform is operating normally for
standalone validation.

# Common Issues

No UART Output
- Verify boot source switch settings
- Verify UART cable connection
- Verify correct UART device node on the host machine

DSP Console Not Updating
- Verify the MRAS service is running
- Verify DSP firmware loaded successfully
- Verify the RU Manager service is active

Board Fails to Boot from SD
- Verify the SD card image was flashed correctly
- Verify SD boot pinstrap configuration
- Re-seat or replace the SD card if necessary

# Next Steps / Further Validation

## A typical E2E test setup includes:

- DU
- PTP server
- UE
- O-RAN fronthaul connectivity
- Synchronization validation
- DL/UL traffic generation and verification

Full end-to-end (E2E) testing and commercial deployment support
should be coordinated with Metanoia.

For additional assistance, advanced integration guidance, or
commercial support, please contact:

https://metanoia-comm.com/contact/



[MOSART Documentation Portal Home](README.md)

# MOSART Cobra SoC Yocto – Quick Start Guide

> **Purpose**: Get a reference Cobra SoC Yocto image built and ready as quickly as possible.
>
> **Audience**: Developers, partners, and integrators evaluating or bringing up MOSART on Cobra SoC.

---

## 1. What This Guide Covers

This quick start guide walks you through the following by a working example build:
- Setting up the supported build environment
- Building a reference MOSART Yocto image for Cobra SoC
- Understanding where outputs are generated

It intentionally avoids advanced customization, debugging, and internal implementation details. For full documentation, refer to the **MOSART Cobra SoC Yocto Guide**.

---

## 2. Prerequisites

### 2.1 Host Requirements

- Linux host (Ubuntu 20.04 / 22.04 recommended)
  - Having at least 130 GB storage for full build tree with all caches and logs.
- Docker installed and running
- Internet access or access to local mirrors (if provided)

For example:
```bash
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 24.04.3 LTS
Release:        24.04
Codename:       noble

$ docker --version
Docker version 28.1.1, build 4eba377

$ ssh -T git@gitlab.com
Welcome to GitLab
```

---

## 3. Get the Source

Clone the official MOSART Yocto BSP repository:

```bash
git -c protocol.file.allow=always clone \
  --recurse-submodules \
  -b mosart-main \
  git@gitlab.com:metanoia-comm/mosart/public/meta-metanoia.git
```

If you are cloning the source from GitHub, please use:

```
git clone https://github.com/metanoia-comm-mosart/meta-metanoia.git
```

After cloning, please run the recipe_update_github_uri.sh script to
update the recipe SRC_URI entries so they point to the corresponding
GitHub repositories:

```
./recipe_update_github_uri.sh
```

---

## 4. Build the Docker Environment

MOSART provides a Docker-based build environment to ensure reproducibility.

```bash
cd meta-metanoia
docker build \
  --build-arg HOST_UID=$(id -u) \
  --build-arg HOST_GID=$(id -g) \
  -t mosart-cobra-yocto-build .
```

Run the container:

```bash
$ docker run --rm -it \
  -v ${PWD}:/home/metanoia/workspace \
  -v "$HOME/.ssh:/home/metanoia/.ssh" \
  mosart-cobra-yocto-build bash
$ ssh -T git@gitlab.com
Welcome to GitLab
$

```

---

## 5. Initialize the Yocto Build Environment

Inside the Docker container:

```bash
$ cd workspace
. oe-init-build-env
~/workspace/build$ 

```

This creates (or reuses) the default `build/` directory.

---

## 6. Build the Reference Image

Build the default MOSART reference image:

```bash
$ export BB_ENV_PASSTHROUGH_ADDITIONS="USE_MOSART"
$ export USE_MOSART=1
$ time bitbake -DD dev-image  > build-evb-log-`date +%s`.txt 2>&1
real    41m23.110s
user    3m16.084s
sys     1m41.935s
```

---

## 7. Locate Build Outputs

After a successful build, the cobra-evb images are available under:

```
build/tmp/deploy/images/mt58xx-cobra-evb/
```

Typical artifacts include:
- `fitImage` (kernel + DTB)
- Root filesystem images (`.squashfs`, `.cpio.gz`, `.full.img`)
- U-Boot and SPL binaries

---

## Flash the image to SD card

Example - assume you have a SD card slot connected to /dev/sda on your Linux host. Then you can run dd as
```bash
cd meta-metanoia/build/tmp/deploy/images/mt58xx-cobra-evb
sudo dd if=dev-image-mt58xx-cobra-evb.rootfs-20260106035900.full.img of=/dev/sda bs=4M status=progress conv=fsync
sync
```

After the SD is successfully flashed, plug it into the SD slot on your Cobra EVB and check the boot source jumpers are properly set for SD. Power on you should see the boot message from the UART console.
```bash
.......
U-Boot SPL 2023.01 (Nov 05 2025 - 03:18:50 +0000)
Device ID: SHUTTLE (0x28240000)
.......
mt58xx-cobra-evb login: root
Password: 
root@mt58xx-cobra-evb:~# ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether f2:de:7a:78:7f:d4 brd ff:ff:ff:ff:ff:ff
    inet 192.168.9.99/24 brd 192.168.9.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet 172.16.0.103/24 metric 1024 brd 172.16.0.255 scope global dynamic eth0
       valid_lft 86373sec preferred_lft 86373sec
    inet6 2000::c4/64 scope global 
       valid_lft forever preferred_lft forever
3: eth1: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc mq state DOWN group default qlen 1000
    link/ether 5a:6f:cf:94:23:40 brd ff:ff:ff:ff:ff:ff
4: sit0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
    link/sit 0.0.0.0 brd 0.0.0.0
root@mt58xx-cobra-evb:~#
root@mt58xx-cobra-evb:~# lsb_release -a
LSB Version:    n/a
Distributor ID: metanoia
Description:    Cobra-SDK 2026.01.06-04:09:12
Release:        2026.01.06-04:09:12
Codename:       cobra

root@mt58xx-cobra-evb:~# systemctl list-units --type=service
  UNIT                                     LOAD   ACTIVE SUB     DESCRIPTION                                    
  accutime.service                         loaded active exited  AccuTime
  board-info.service                       loaded active exited  Board-Info
  busybox-syslog.service                   loaded active running System Logging Service
  cobra-init.service                       loaded active exited  Cobra INIT
  dbus.service                             loaded active running D-Bus System Message Bus
  getty@tty1.service                       loaded active running Getty on tty1
  mpbe-ptp-eventd.service                  loaded active running Metanoia M-Plane Backend PTP Event Daemon
  mpbe.service                             loaded active exited  Metanoia M-Plane Backend
  mpbed.service                            loaded active running Metanoia M-Plane Backend Daemon
  mpbed@openamp.service                    loaded active running Metanoia M-Plane Backend Daemon of openamp
  rf-board.service                         loaded active exited  RF-Board control
  serial-getty@ttyS0.service               loaded active running Serial Getty on ttyS0
  skyworks.service                         loaded active exited  Skyworks
  sshdgenkeys.service                      loaded active exited  OpenSSH Key Generation
  sysstat.service                          loaded active exited  Resets System Activity Logs
  systemd-journal-flush.service            loaded active exited  Flush Journal to Persistent Storage
  systemd-journald.service                 loaded active running Journal Service
  systemd-logind.service                   loaded active running User Login Management
  systemd-network-generator.service        loaded active exited  Generate network units from Kernel command line
  systemd-networkd.service                 loaded active running Network Configuration
  systemd-random-seed.service              loaded active exited  Load/Save OS Random Seed
  systemd-remount-fs.service               loaded active exited  Remount Root and Kernel File Systems
  systemd-resolved.service                 loaded active running Network Name Resolution
  systemd-sysctl.service                   loaded active exited  Apply Kernel Variables
  systemd-tmpfiles-setup-dev-early.service loaded active exited  Create Static Device Nodes in /dev gracefully
  systemd-tmpfiles-setup-dev.service       loaded active exited  Create Static Device Nodes in /dev
  systemd-tmpfiles-setup.service           loaded active exited  Create Volatile Files and Directories
  systemd-udev-trigger.service             loaded active exited  Coldplug All udev Devices
  systemd-udevd.service                    loaded active running Rule-based Manager for Device Events and Files
  systemd-update-utmp.service              loaded active exited  Record System Boot/Shutdown in UTMP
  systemd-user-sessions.service            loaded active exited  Permit User Sessions
  systemd-userdbd.service                  loaded active running User Database Manager
  systemd-vconsole-setup.service           loaded active exited  Virtual Console Setup
  ts-saver.service                         loaded active exited  load timestamp
  user-runtime-dir@0.service               loaded active exited  User Runtime Directory /run/user/0
  user@0.service                           loaded active running User Manager for UID 0

Legend: LOAD   -> Reflects whether the unit definition was properly loaded.
        ACTIVE -> The high-level unit activation state, i.e. generalization of SUB.
        SUB    -> The low-level unit activation state, values depend on unit type.

36 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
root@mt58xx-cobra-evb:~# 

```

## 9. Next Steps

From here, you may:
- Add user-space packages via Yocto recipes
- Customize kernel configuration using supported mechanisms
- Start and deploy 5G O-RU applications (Not covered by the generic MOSART document, please consult Metanoia official documentation)

For advanced workflows, customization guidelines, and support boundaries, refer to the full **MOSART Cobra SoC Yocto Guide**.

---

## 10. Support Notes

- This quick start demonstrates a **reference build to bring-up the Linux platform** provided by Metanoia.
- Customizations beyond documented extension points are outside MOSART support scope.
- Always track MOSART and Cobra SDK versions for reproducibility.

---


# MOSART Introduction

<details>
<summary><strong>Table of Contents</strong></summary>

- [Key Features](#key-features)
- [Objectives](#objectives)
- [Architecture Overview](#architecture-overview)
- [Open-Source Vision](#open-source-vision)
- [Project Status](#project-status)
- [Roadmap](#roadmap)
  - [Areas Under Evaluation](#areas-under-evaluation)
    - [Linux-to-DSP Management Framework](#linux-to-dsp-management-framework)
    - [Alternative Build System Support](#alternative-build-system-support)
    - [RTOS Support on DSP Processors](#rtos-support-on-dsp-processors)
    - [DFE Common Libraries](#dfe-common-libraries)
    - [Open DSP Demonstration Platform](#open-dsp-demonstration-platform)
  - [Longer-Term Direction](#longer-term-direction)
    - [Open CPU and DSP Platform](#open-cpu-and-dsp-platform)
  - [Additional Information](#additional-information)
- [Legal Notices](#legal-notices)
  - [Open-Source Licensing](#open-source-licensing)
  - [Trademark Notice](#trademark-notice)
  - [Reference Platform Disclaimer](#reference-platform-disclaimer)

</details>

MOSART™ (Metanoia Open-Source Advanced Radio Technology) is an
open-source software-defined radio (SDR) platform and development SDK
designed for modern wireless infrastructure targeting current and
future AI-RAN systems and beyond.

MOSART is initially demonstrated on Metanoia’s Cobra SoC platform,
which serves as the primary reference implementation platform for the
project. The platform provides a cost-efficient, production-oriented
reference environment for developing and evaluating current and
next-generation wireless communication solutions, especially systems
aligned with 3GPP and O-RAN architectures.

MOSART is designed to support future AI-assisted radio optimization,
edge inference workloads, intelligent RAN orchestration frameworks,
and evolving AI-RAN architectures for B5G and 6G wireless systems.

The MOSART SDK integrates the essential software components required
for embedded Linux systems, real-time radio processing, platform
management, hardware abstraction, and O-RAN interfaces into a unified
and reproducible development environment. It is intended to support
developers, researchers, customers, and ecosystem partners working on
B5G/6G wireless technologies, Open RAN infrastructure, SDR
experimentation, and embedded networking systems.

MOSART encourages open collaboration, interoperability, and
upstream-friendly development across the wireless ecosystem.

## Key Features

- Open-source SDR platform
- O-RAN-aligned software stack
- Yocto-based SDK and development environment
- Portable architecture adaptable to other build systems such as Buildroot
- Modular repository and software architecture
- Real-time DSP and radio processing integration
- Linux-based embedded wireless platform
- Cobra SoC reference implementation platform
- Production-oriented wireless infrastructure integration examples

## Objectives

The primary objectives of MOSART are:

- Provide an open and accessible SDR platform for wireless innovation
- Enable rapid prototyping and evaluation of AI-RAN and O-RAN systems
- Simplify integration between hardware, firmware, Linux, and radio software stacks
- Offer a reproducible Yocto-based SDK and development environment
  while remaining portable to other build systems such as Buildroot
- Support collaboration between industry, academia, and ecosystem partners
- Demonstrate production-oriented embedded wireless system integration

## Architecture Overview

MOSART is built on a modular architecture demonstrated on the O-RAN
WG7 Whitebox-oriented Cobra SoC evaluation platform. The platform
combines general-purpose processing, DSP acceleration, RF control,
synchronization, timing, and high-speed networking into a unified SDR
system architecture.

Major software and platform components include:

- Linux kernel and device drivers
- OpenSBI and U-Boot boot stack
- Yocto-based embedded Linux distribution
- DSP and radio firmware integration
- Hardware abstraction and board support packages
- O-RAN software interfaces and management components
- RF configuration and synchronization support
- Ethernet fronthaul and networking integration
- Platform APIs and management utilities

The modular repository structure allows components to be independently
maintained, extended, customized, and upstreamed where appropriate.

## Open-Source Vision

MOSART aims to bridge the gap between research-oriented SDR platforms
and production-oriented wireless infrastructure development. By
combining open-source software methodologies with practical platform
integration, MOSART provides a foundation for long-term ecosystem
collaboration, innovation, and future wireless experimentation.

Public documentation, source repositories, development guides, and
reference demonstrations will continue to expand as the project
evolves.

## Project Status

MOSART is an evolving open-source reference platform. The initial
public repositories and documentation are intended to support
development, evaluation, integration, and ecosystem collaboration.
Feature availability, hardware support, performance characteristics,
and deployment readiness may vary by repository, branch, platform
configuration, and release stage.

## Roadmap

MOSART is intended to evolve progressively from an open reference
implementation for O-RAN O-RU development into a broader
software-defined radio (SDR) platform supporting wireless
infrastructure innovation, AI-RAN research, and advanced radio system
development.

The following areas are currently being evaluated and explored as part
of the ongoing evolution of the MOSART ecosystem.

### Areas Under Evaluation

#### Linux-to-DSP Management Framework

- Further enhance OpenAMP-based communication and management
  capabilities between Linux and DSP subsystems.
- Explore APIs for provisioning, monitoring, control, and firmware
  lifecycle management of DSP applications.
- Simplify integration between application software and real-time
  processing components.

#### Alternative Build System Support

- Investigate support for build systems beyond Yocto, including
  Buildroot and other embedded Linux environments.
- Improve portability and flexibility across different development
  workflows.

#### RTOS Support on DSP Processors

- Evaluate support for real-time operating systems such as FreeRTOS
  and Zephyr on Cobra DSP subsystems.
- Facilitate development of real-time applications and platform
  customization.

#### DFE Common Libraries

- Develop reusable Digital Front-End (DFE) software components.
- Provide common building blocks that may simplify development of
  radio signal processing applications.

#### Open DSP Demonstration Platform

- Provide DSP-focused demonstration examples and reference
  applications.
- Illustrate software development workflows on Cobra SoC DSP
  processors.
- Support experimentation, education, and evaluation of customized
  radio processing techniques.

### Longer-Term Direction

#### Open CPU and DSP Platform

- Explore broader openness and extensibility across CPU and DSP
  software environments while continuing to support customized and
  proprietary deployments where appropriate.
- Enable greater flexibility for Linux, DSP, AI, and radio processing
  applications.
- Support research, experimentation, and ecosystem collaboration
  related to SDR, AI-RAN, and future wireless technologies.

### Additional Information

MOSART will continue to evolve through open-source development and
ecosystem collaboration. Some Cobra SoC platform capabilities,
reference implementations, and deployment-specific features may be
documented or released separately from the core MOSART project.

For information regarding Cobra SoC-specific capabilities,
customizations, evaluation programs, commercial support, or other
advanced development opportunities, please contact Metanoia
Communications.

Roadmap items are provided for informational purposes only and are
subject to change as project priorities, community contributions,
technology developments, and ecosystem requirements evolve.

## Legal Notices

### Open-Source Licensing

Unless otherwise specified, MOSART repositories and software
components are released under the open-source licenses documented
within their respective repositories. The applicable license for each
repository is defined by the LICENSE file and accompanying notices in
that repository.

Third-party software components may remain subject to their original
upstream licenses and terms.

### Trademark Notice

MOSART™ (Metanoia Open-Source Advanced Radio Technology), Cobra™, and
related names, logos, and branding are trademarks or registered
trademarks of Metanoia Communications Inc. or their respective owners.
All third-party trademarks are the property of their respective
owners.

Use of the MOSART name, logo, or branding does not grant endorsement,
certification, or official partnership status unless explicitly
authorized by Metanoia.

### Reference Platform Disclaimer

The MOSART platform software framework and reference deployment
examples described in this document are provided for development,
evaluation, integration, and educational purposes.

Commercial deployment architectures, regulatory compliance,
performance validation, security hardening, and production lifecycle
management remain deployment-specific responsibilities unless
explicitly documented otherwise.



[MOSART Documentation Portal Home](README.md)

<details>
<summary><strong>Table of Contents</strong></summary>

- [MOSART Platform Software](#mosart-platform-software)
  - [Overview](#overview)
  - [Document Version Information](#document-version-information)
  - [Reference Platform Architecture](#reference-platform-architecture)
  - [Intended Audience and Prerequisites](#intended-audience-and-prerequisites)
  - [Topics Included](#topics-included)
  - [MOSART Cobra EVB SD/eMMC Storage Layout](#mosart-cobra-evb-sdemmc-storage-layout)
    - [Storage Image Layout](#storage-image-layout)
    - [Functional Notes](#functional-notes)
      - [Bootloader Regions](#bootloader-regions)
      - [Kernel A/B Scheme](#kernel-ab-scheme)
      - [Data Partitions](#data-partitions)
  - [Boot Flow and Platform Initialization](#boot-flow-and-platform-initialization)
  - [MTF Firmware and GPT Image Generation](#mtf-firmware-and-gpt-image-generation)
  - [Device Tree Integration](#device-tree-integration)
  - [U-Boot Environment Management](#u-boot-environment-management)
  - [Flashing and Deployment Workflows](#flashing-and-deployment-workflows)
  - [Yocto Image Integration and Build Configuration](#yocto-image-integration-and-build-configuration)
  - [DSP Firmware and PHY Integration](#dsp-firmware-and-phy-integration)
  - [MRAS Initialization and Platform Services](#mras-initialization-and-platform-services)
  - [System API and Management Frameworks](#system-api-and-management-frameworks)
  - [SFP Module Support and Management Utilities](#sfp-module-support-and-management-utilities)
  - [Other Platform Software Related Topics](#other-platform-software-related-topics)
  - [Frequently Asked Questions (FAQ)](#frequently-asked-questions-faq)
  - [Additional References](#additional-references)
</details>

# MOSART Platform Software

## Overview

The MOSART Platform Software provides a reference boot, storage,
platform initialization, and system integration framework for Cobra
SoC–based platforms.

The platform supports reproducible Yocto-based builds, modular
software integration, and deployment-oriented system architectures
suitable for wireless infrastructure and SDR applications.

MOSART is designed as an extensible open platform framework that
enables developers, researchers, ecosystem partners, and system
integrators to customize and deploy Cobra SoC platforms for
deployment-specific applications including O-RAN and AI-RAN systems.

## Document Version Information

| Item | Value |
|------|-------|
| Document | MOSART Platform Software |
| Platform | Cobra SoC |
| Reference Build | MOSART Yocto Reference Platform |
| Status | Public Preview |
| Last Updated | 2026-05-23 |

---


MOSART should be viewed as a reference BSP and integration
framework rather than a fixed end-product software stack.

MOSART leverages upstream open-source projects whenever practical
while maintaining platform-specific integration layers separately to
improve long-term maintainability and upstream alignment.

This document focuses on platform software integration and deployment
concepts rather than low-level PHY or DSP implementation details.

Unless otherwise stated, examples in this document are based on the
MOSART Yocto reference implementation running on the Cobra EVB
platform.


## Reference Platform Architecture

The following diagram illustrates the high-level MOSART platform
software architecture on Cobra SoC platforms.

```text
Applications / O-RAN Services / User Applications
                    |
Platform Services / Management Frameworks
(mpapi, rumanager, sysrepo, oran-mplane)
                    |
Linux Root Filesystem / Yocto Integration
                    |
Linux Kernel (linux-metanoia)
                    |
OpenSBI / U-Boot / MTF
                    |
Cobra SoC Hardware Platform
```

The architecture shown above represents a reference integration model.
Deployment-specific software stacks and hardware integration layers
may vary depending on customer requirements and deployment
architectures.

---


## Intended Audience and Prerequisites

This document is intended for:

- Platform developers
- System integrators
- Embedded Linux developers
- Wireless infrastructure engineers
- O-RAN and SDR platform developers
- Advanced users evaluating MOSART and Cobra SoC platforms

Readers are expected to have basic familiarity with:

- Embedded Linux systems
- Yocto Project workflows
- Bootloader concepts
- Device Tree concepts
- Storage partitioning and deployment workflows

---

## Topics Included

- [Boot Flow and Platform Initialization](#boot-flow-and-platform-initialization)
- [MTF Firmware and GPT Image Generation](#mtf-firmware-and-gpt-image-generation)
- [Storage Layout and Partitioning](#mosart-cobra-evb-sdemmc-storage-layout)
- [Device Tree Integration](#device-tree-integration)
- [U-Boot Environment Management](#u-boot-environment-management)
- [Flashing and Deployment Workflows](#flashing-and-deployment-workflows)
- [Yocto Image Integration and Build Configuration](#yocto-image-integration-and-build-configuration)
- [DSP Firmware and PHY Integration](#dsp-firmware-and-phy-integration)
- [MRAS Initialization and Platform Services](#mras-initialization-and-platform-services)
- [System API and Management Frameworks](#system-api-and-management-frameworks)
- [SFP Module Support and Management Utilities](#sfp-module-support-and-management-utilities)
- [Other Platform Software Related Topics](#other-platform-software-related-topics)

> **Note:**  
> The topics and subsections described in this document may be
> expanded, refined, or updated over time as MOSART platform
> development on Cobra SoC hardware continues to evolve.
>
> Additional implementation details, deployment workflows, platform
> integration examples, debugging procedures, and development process
> documentation may be added progressively as the MOSART ecosystem,
> software stack, and reference platforms mature.

---

## MOSART Cobra EVB SD/eMMC Storage Layout

### Storage Image Layout

The following storage layout represents a reference deployment
example for a **4GB eMMC** or **4GB SD** storage device used on the
Cobra EVB platform.

Actual deployment layouts may vary depending on product
requirements, redundancy policies, update strategies, and available
storage capacity.

> **Important:**  
> The storage layout shown below is provided as a reference example
> only. Commercial deployments may use different partition sizes,
> redundancy models, filesystems, or upgrade strategies.

> **Note:**  
> The MOSART Bootrom MTF understands **GPT format only**.  
> Regions outside standard GPT-managed partitions may be used by early
> boot firmware and next-stage bootloader components according to the
> platform boot architecture.

In the example layout below, **SPL-1** and **SPL-2** both reference a
shared **U-Boot** bootloader image for convenience. In a full U-Boot
A/B design, each SPL may have its own U-Boot image to enable complete
redundancy across both SPL and U-Boot components.

Here, **SPL** refers to **U-Boot SPL** (Secondary Program Loader).

| Region # | Type | Size | Content | Notes / Purpose |
|-----------|------|------|---------|----------------|
| **Region 1 - 3** | RAW (Boot Region) | 3 MiB | **GPT Image** | GPT table and FIP blobs for DTB, SPL, and OpenSBI images |
| **Region 4** | RAW (Boot Region) | 13 MiB | **U-Boot+ENV** | U-Boot and U-Boot environment |
| **Region 5** | RAW (Partition-3) | 32 MiB | **Kernel0** | Kernel (slot A) |
| **Region 6** | RAW (Partition-4) | 32 MiB | **Kernel1** | Kernel (slot B) |
| **Region 7** | SquashFS (Partition-5) | 128 MiB | **RootFS0** | Root filesystem (slot A) |
| **Region 8** | SquashFS (Partition-6) | 128 MiB | **RootFS1** | Root filesystem (slot B) |
| **Region 9** | EXT4 (Partition-7) | 1 GiB | **Permanent Data** | Persistent configs, calibration, logs, RU/DU DB |
| **Region 10** | EXT4 (Partition-8) | 2 GiB | **User Data** | Operator/user data |

> **Note:** For details in **Region 1–3**, see [Cobra GPT Image Layout and Generation - COMING SOON!](cobra-mtf.md#cobra-gpt-image-layout-and-generation)

---

### Functional Notes

#### Bootloader Regions
- **SPL1 / SPL2**: Redundant first-stage loaders.
- **DTB1 / DTB2**: Redundant device trees corresponding to SPL copies.
- **U-Boot + ENV**: Bootloader and environment stored in RAW space.  
  *Two copies may exist for full A/B redundancy.*

#### Kernel A/B Scheme
- **Kernel0 + RootFS0** → Primary boot slot A  
- **Kernel1 + RootFS1** → Secondary boot slot B  
This layout enables deployment-specific A/B upgrade workflows,
rollback protection strategies, and high-availability software update
mechanisms.

#### Data Partitions
- **Permanent Data (EXT4, 1 GiB)**  
  Used for calibration, persistent configs, logs, O-RU/O-DU databases.

- **User Data (EXT4, 2 GiB)**  
  Stores downloaded packages, operator files, applications, and user configurations.

---

> **Reference Platform Note:**  
> The following sections describe the MOSART reference implementation
> and documented integration model for Cobra SoC platforms.
>
> Deployment-specific customization, vendor extensions,
> customer-owned modifications, and proprietary integrations may vary
> depending on operational requirements and deployment architecture.
>
> Some interfaces, workflows, and deployment models described in this
> document may evolve as the MOSART platform continues to mature.

---

## Boot Flow and Platform Initialization

This section describes the MOSART reference boot flow on Cobra
SoC–based platforms, including Bootrom behavior, MTF loading,
OpenSBI, U-Boot initialization, Linux kernel loading, and root
filesystem startup.

Representative topics include:

- Bootrom initialization sequence
- GPT image loading flow
- MTF firmware initialization
- OpenSBI handoff
- U-Boot initialization and boot scripts
- Linux kernel startup
- Root filesystem mounting and system initialization
- Recovery and fallback boot behavior

---

## MTF Firmware and GPT Image Generation

This section describes the MOSART MTF firmware framework and GPT image
generation workflow used by the Cobra SoC platform.

Representative topics include:

- GPT image layout generation
- MTF firmware packaging
- SPL and DTB integration
- OpenSBI image integration
- Boot image redundancy models
- Image signing and deployment considerations
- Reference image generation workflows

---

## Device Tree Integration

This section describes Device Tree usage within the MOSART platform
software framework.

Representative topics include:

- Cobra SoC Device Tree hierarchy
- Board-specific DTS organization
- Peripheral enablement
- RF and platform hardware configuration
- Device Tree overlays
- Customer-specific platform extensions
- DTS integration within Yocto builds

---

## U-Boot Environment Management

This section describes the reference U-Boot environment configuration
used on MOSART Cobra SoC platforms.

Representative topics include:

- Environment variable organization
- Boot slot selection
- A/B boot handling
- Recovery boot logic
- Boot script execution
- Storage boot target selection
- Update and rollback behavior

---

## Flashing and Deployment Workflows

This section describes reference workflows for flashing and deploying
MOSART software images onto Cobra SoC platforms.

Representative topics include:

- SD card image deployment
- eMMC flashing workflows
- Recovery image usage
- GPT image flashing
- Kernel and rootfs updates
- Field upgrade workflows
- Manufacturing deployment considerations

---

## Yocto Image Integration and Build Configuration

This section describes how MOSART platform software components are
integrated into the Yocto build environment.

Representative topics include:

- Yocto image recipes
- BSP integration
- Package groups
- Root filesystem customization
- Build configuration fragments
- Deployment image generation
- SDK and release integration

---

## DSP Firmware and PHY Integration

This section describes DSP firmware integration and deployment models
within the MOSART platform framework.

Representative topics include:

- DSP firmware loading
- PHY integration architecture
- Vendor-specific PHY support
- DSP binary deployment
- Firmware packaging
- Runtime firmware initialization
- Deployment-specific PHY integration considerations

---

## MRAS Initialization and Platform Services

This section describes MRAS initialization and low-level platform
service integration within MOSART.

Representative topics include:

- Platform initialization services
- System startup sequencing
- Hardware initialization helpers
- Platform monitoring services
- Runtime management integration
- Deployment-specific service extensions

---

## System API and Management Frameworks

This section describes MOSART platform management frameworks and
system APIs.

Representative topics include:

- MPAPI framework
- RU management integration
- Sysrepo integration
- O-RAN M-Plane interfaces
- Platform management APIs
- Runtime configuration management
- Service orchestration frameworks

---

## SFP Module Support and Management Utilities

This section describes SFP transceiver integration and management
support within the MOSART framework.

Representative topics include:

- SFP EEPROM access
- Optical module monitoring
- Link status management
- Platform utility integration
- Deployment-specific optical module support
- Diagnostics and monitoring workflows

---

## Other Platform Software Related Topics

Additional platform software topics may include:

- Platform debugging workflows
- Recovery and rescue environments
- Manufacturing utilities
- Platform validation tools
- Secure boot integration
- High-availability deployment models
- CI/CD integration workflows
- Future platform software extensions

---

## Frequently Asked Questions (FAQ)

### Is the storage layout fixed for all deployments?

No. The layouts described in this document are reference deployment
examples. Commercial deployments may use different partition sizes,
redundancy models, storage devices, filesystems, or upgrade
strategies.

### Does MOSART support build systems other than Yocto?

Yes. MOSART officially supports Yocto and also has ports for other
platform environments including Buildroot. Additional deployment-
specific environments may also be supported.

### Are secure boot and production key management included?

Security hardening, secure boot policy, key provisioning, verified
boot, and production credential management are deployment-specific
responsibilities unless explicitly documented otherwise.

### Are all MOSART components open source?

Unless otherwise specified, MOSART repositories are released under
open-source licenses documented within each repository. Some
deployment-specific vendor components may remain proprietary.

---

## Additional References

Additional MOSART platform documentation may include:

- MOSART Cobra SoC Yocto Guide
- MOSART Architecture Documentation
- MOSART Boot Flow Documentation
- MOSART Device Tree Documentation
- MOSART GPT and MTF Documentation
- MOSART Platform Bring-Up Guides

Future documentation updates may expand these areas as MOSART platform
development continues to evolve.

---

## Legal Notices

### Open-Source Licensing

Unless otherwise specified, MOSART repositories and software
components are released under the open-source licenses documented
within their respective repositories.

Third-party software components may remain subject to their original
upstream licenses and terms.

### Trademark Notice

MOSART™ (Metanoia Open-Source Advanced Radio Technology), Cobra™, and
related names, logos, and branding are trademarks or registered
trademarks of Metanoia Communications Inc. or their respective owners.

Use of the MOSART name, logo, or branding does not grant endorsement,
certification, or official partnership status unless explicitly
authorized by Metanoia.

### Reference Platform Disclaimer

The MOSART platform software framework and reference deployment
examples described in this document are provided for development,
evaluation, integration, and educational purposes.

Commercial deployment architectures, regulatory compliance,
performance validation, security hardening, and production lifecycle
management remain deployment-specific responsibilities unless
explicitly documented otherwise.



[MOSART Documentation Portal Home](README.md)

# MOSART Cobra SoC Yocto Guide

> **Audience**: Partners, system integrators, and advanced users
>    building Linux images on Metanoia Cobra SoC using MOSART.
>
> **Scope**: This document describes the *supported* Yocto build
    workflow, configuration model, and extension points for Cobra SoC
    within the MOSART framework. It intentionally omits internal
    infrastructure details and non-supported customization paths.

This document focuses on the Linux system layer built using the
**Yocto Project**, an open-source and community-driven framework for
creating reproducible and customizable embedded Linux distributions
tailored to specific hardware platforms and system requirements.

The **MOSART** open platform is intentionally designed to remain
portable and extensible, enabling future support for alternative build
systems such as Buildroot, OpenWrt, and other open-source or
proprietary environments. Developers, partners, and contributors are
encouraged to explore the MOSART documentation portal and participate
in the MOSART ecosystem through collaboration and contributions.

MOSART provides a reference integration framework and reference
deployment architecture. Production deployment architectures may vary
depending on customer system requirements, carrier specifications, and
hardware integration choices.

MOSART leverages upstream open-source projects whenever practical and
maintains platform-specific integration layers separately to improve
long-term maintainability and upstream alignment.

Security hardening, secure boot policy, key provisioning, and
production credential management are deployment-specific
responsibilities unless explicitly documented otherwise.

The MOSART Yocto environment should be considered a reference BSP and
integration framework rather than a fixed end-product software stack.

> **Note 1:** This document describes a specific reference Yocto build
> for a 5G O-RU based on the MOSART open platform. Throughout the
> remainder of this document, this reference platform may be referred
> to as **MOSART-XG**, or simply **MOSART**, depending on context.

> **Note 2:** If you are familiar with Yocto, you may jump directly to
> [MOSART Cobra Yocto Build Quick Start](mosart-cobra-yocto-quickstart.md).

> **Note 3:** This document focuses specifically on MOSART running on
> Cobra SoC–based hardware platforms and the associated reference
> Yocto integration environment.
>
> Throughout this document, the term **MOSART** may refer
> specifically to the MOSART software platform as integrated and
> validated on Cobra SoC hardware unless otherwise explicitly stated.

## Table of Contents

- [MOSART Cobra SoC Yocto Guide](#mosart-cobra-soc-yocto-guide)
- [1. MOSART Yocto Context](#1-mosart-yocto-context)
- [2. Supported Yocto Model](#2-supported-yocto-model)
- [3. Layer and Responsibility Boundaries](#3-layer-and-responsibility-boundaries)
- [4. Hardware Targets](#4-hardware-targets)
- [5. Build Environment](#5-build-environment)
  - [5.1 Host Requirements](#51-host-requirements)
  - [5.2 Repository Checkout](#52-repository-checkout)
- [6. Image Build Workflow](#6-image-build-workflow)
  - [6.1 Initialize Build Environment](#61-initialize-build-environment)
  - [6.2 Build Reference Image](#62-build-reference-image)
  - [6.3 Build Output Structure](#63-build-output-structure)
- [7. Kernel and Bootloader Updates](#7-kernel-and-bootloader-updates)
  - [7.1 Kernel](#71-kernel)
  - [7.2 U-Boot](#72-u-boot)
- [8. Root Filesystem Customization](#8-root-filesystem-customization)
  - [8.1 Adding Packages](#81-adding-packages)
  - [8.2 Initramfs Images](#82-initramfs-images)
- [9. Supported Development Workflow (devtool)](#9-supported-development-workflow-devtool)
- [10. Upgrade Strategy](#10-upgrade-strategy)
- [11. Version Identification](#11-version-identification)
- [12. Debug and Bring-Up](#12-debug-and-bring-up)
- [13. What Is Not Covered](#13-what-is-not-covered)
- [14. Summary](#14-summary)

---

## 1. MOSART Yocto Context

The **MOSART** Cobra Yocto environment is a reference build and integration
framework for Metanoia’s open platform built around the Cobra SoC. It
defines:

- A **reference system architecture** for 7.2x O-RU deployments

- A **supported Yocto-based software stack**, including bootloader,
  Linux kernel, root filesystem, platform services, and development
  tooling

- Clear **responsibility boundaries** between MOSART core components,
  vendor-maintained modules, and customer-specific integrations

- A reproducible and maintainable Linux system software environment
  intended for platform bring-up, development, validation, and
  deployment

- A modular integration model that allows deployment-specific
  customization of proprietary components such as PHY layers,
  synchronization hardware, RF front-end devices, power amplifiers
  (PAs), and other vendor-specific subsystems outside the MOSART core
  platform scope

Within MOSART:

- Third-party PHY and DSP software layers may remain vendor-maintained
  and externally integrated depending on deployment requirements.

- The Yocto-based MOSART environment is intended to deliver a
  reproducible, maintainable, and supportable Linux system software
  stack for the Cobra SoC platform.

- Proprietary customer-specific integrations and customizations —
  including vendor-specific PHY implementations, timing and
  synchronization hardware, RF front-end components, power amplifiers
  (PAs), and other specialized hardware or software modules — remain
  deployment-dependent choices outside the scope of the MOSART core
  platform.

---

## 2. Supported Yocto Model

The Cobra SoC platform uses a **Poky-based Yocto Project**
distribution with dedicated BSP and integration layers.

Core layers include:

- **meta-metanoia** – Cobra SoC BSP, platform integration, and MOSART
  reference system layer

The Yocto environment is designed to:

- Enable reproducible and repeatable Linux image builds

- Support controlled customization through Yocto recipes, layers,
  configuration fragments, and overlays

- Preserve upgrade compatibility across multiple software releases and
  deployment generations

- Provide a maintainable and supportable Linux system software stack
  for development, validation, and deployment workflows

- Support modular integration of deployment-specific components and
  proprietary vendor extensions outside the MOSART core platform scope

---

## 3. Layer and Responsibility Boundaries

Within the MOSART framework, the core Linux platform, BSP, and system
integration layers are maintained as the reference open platform,
while deployment-specific proprietary integrations remain under vendor
or customer responsibility.

### Documented Extension Points

Documented extension points refer to supported customization
mechanisms explicitly defined by MOSART, including but not limited to:

- Yocto recipes and `.bbappend` files in customer-owned layers
- Device Tree overlays and documented DTS hooks
- Kernel configuration fragments and approved patch mechanisms
- User-space applications, services, and startup scripts
- Image-level package selection and root filesystem composition

These mechanisms are intended to provide controlled extensibility
while preserving maintainability, upgrade compatibility, and support
coverage across MOSART software releases.

### What Is *Not* a Documented Extension Point

Equally important, the following actions are **not** considered
documented extension points within the MOSART framework:

- Direct modification of platform-owned BSP recipes
- Forking or rewriting core logic within `meta-metanoia`
- Undocumented changes to the Linux kernel, bootloader, or firmware
- Modifying the boot flow or partition layout outside published and
  supported interfaces

While such changes may function technically, they fall outside the
defined MOSART support scope and are not guaranteed to remain
compatible across future software releases.

Deployment-specific proprietary integrations — including vendor PHY
implementations, synchronization hardware, RF front-end devices, power
amplifiers (PAs), and other specialized hardware or software modules
— remain customer or vendor responsibilities outside the MOSART core
platform scope.

### MOSART Architecture

The MOSART architecture is designed as a modular, extensible software
platform centered around the Cobra SoC ecosystem.
The current
reference architecture consists of the following major repositories
and software components.

The repository structure shown below represents the current reference
MOSART integration architecture and may evolve across future software
releases.

```text
mosart
├── ddrfw            # DDR training and initialization firmware
├── dspfw            # DSP firmware and radio processing binaries
├── gnss-module      # GNSS synchronization and timing integration
├── linux            # Linux kernel with Cobra SoC BSP support
├── meta-metanoia    # Core Yocto BSP and platform integration layer
├── metanoia-base    # Common platform utilities and base components
├── meta-rf          # RF-related Yocto integration layer
├── meta-sysrepo     # Sysrepo and management framework integration
├── mosart-docs      # MOSART and Cobra SoC public and reference documentation
├── mpapi            # Metanoia platform API framework
├── mras-init        # MRAS initialization and startup utilities
├── opensbi          # OpenSBI firmware and platform support
├── oran-mplane      # O-RAN M-Plane management components
├── ruboard          # Board support utilities and platform tools
├── rumanager        # Radio Unit management framework
├── sfp-module       # SFP transceiver management components
└── u-boot           # U-Boot bootloader with Cobra platform support
```

Unless otherwise specified, MOSART repositories are released under
open-source licenses documented within each repository.

The MOSART repository structure is intentionally modular to enable:

- Independent component maintenance and versioning
- Flexible deployment-specific integration
- Controlled customization through documented extension mechanisms
- Reproducible software builds and release management
- Long-term maintainability across multiple software generations
- Future extensibility for additional hardware platforms, software
  modules, and deployment environments

Additional proprietary, customer-specific, or vendor-maintained
components may be integrated into deployment environments depending on
system architecture and operational requirements.


## 4. Hardware Targets

The MOSART Cobra Yocto platform supports multiple hardware targets and
deployment profiles through machine configurations, Device Tree
separation, and modular BSP integration.

Current reference hardware targets include:

- **Cobra EVB (Evaluation Board)**  
  Primary reference platform for software development, platform
  bring-up, validation, debugging, and integration workflows.

- **O-RAN WG7 Compliant O-RU Whitebox Platforms**  
  Third-party O-RU whitebox hardware platforms based on the Cobra SoC
  and aligned with O-RAN WG7 hardware specifications.

The MOSART framework is designed to support long-term platform
maintainability and deployment flexibility through explicit machine,
board, and Device Tree separation.

Deployment-specific hardware integrations — including RF front-end
designs, synchronization hardware, timing modules, power amplifiers
(PAs), and carrier-specific configurations — may vary by platform and
remain outside the MOSART core platform scope.

---

## 5. Build Environment

### 5.1 Host Requirements

The MOSART Yocto build environment is intended to run on a Linux host
system using Docker-based reproducible build containers.

Minimum host requirements include:

- Validated build hosts currently include Ubuntu 24.04 LTS and
  compatible Linux distributions.
- Docker
- **Note**: Yocto build environments may require substantial disk space
  depending on enabled features, build artifacts, and cache retention
  policies.

The official build environment is distributed as a pre-configured
Docker image to ensure reproducibility, dependency consistency, and
long-term build compatibility across different development hosts.

Since BitBake internally uses Linux network namespaces (`netns`),
running BitBake as a non-root user requires enabling unprivileged user
namespace support on the host system.

Configure the following sysctl parameters (for example via
`/etc/sysctl.conf`):

```
kernel.apparmor_restrict_unprivileged_userns=0
kernel.unprivileged_userns_clone=1
```

### 5.2 Repository Checkout

The MOSART reference Yocto environment is distributed through Git
repositories hosted on GitLab.

Using the Git SSH protocol, clone the repository and all submodules as
follows:

```bash
git -c protocol.file.allow=always clone \
  --recurse-submodules \
  -b use-mosart \
  git@gitlab.com:metanoia-comm/mosart/public/meta-metanoia.git
```

If you are behind a firewall that only allows HTTP/HTTPS traffic, you
can rewrite Git SSH URLs to HTTPS by updating your `.gitconfig` and,
if required, configuring a GitLab HTTPS access token:

```
[credential]
       helper = store

[url "https://gitlab.com/"]
       insteadOf = git@gitlab.com:

[url "https://git.yoctoproject.org/"]
       insteadOf = git://git.yoctoproject.org/

[url "https://github.com/"]
       insteadOf = git@github.com:
```

---

## 6. Image Build Workflow

The reproducible build model is intended to support both local
development workflows and automated CI/CD integration pipelines.

### 6.1 Initialize Build Environment

After cloning the repository and starting the official MOSART Yocto
Docker build environment, initialize the Yocto build environment as follows:

```bash
export BB_ENV_PASSTHROUGH_ADDITIONS="USE_MOSART"
export USE_MOSART=1
. ./oe-init-build-env
```

### 6.2 Build Reference Image

```bash
bitbake dev-image
```

### 6.3 Build Output Structure

After compilation, the build directory contains the following structure:

```
build/
├── conf/                    # Build configuration (local.conf, bblayers.conf)
├── downloads/               # Downloaded source tarballs (DL_DIR)
├── sstate-cache/            # Shared state cache for faster rebuilds
├── cache/                   # BitBake parse cache
├── tmp/                     # Main build output directory
│   ├── deploy/
│   │   ├── images/          # Final deployable binary images
│   │   │   └── <MACHINE>/   # Machine-specific images (e.g., mt58xx-cobra-evb)
│   │   ├── rpm/             # Built packages (RPM format)
│   │   ├── licenses/        # License information
│   │   └── spdx/            # Software Bill of Materials
│   ├── work/                # Per-recipe build directories
│   ├── work-shared/         # Shared sources (kernel, gcc)
│   ├── sysroots-components/ # Staged components for cross-compilation
│   ├── stamps/              # Build completion markers
│   ├── log/                 # Build logs
│   └── buildstats/          # Build timing statistics
```

The `downloads/` and `sstate-cache/` directory may be shared across
multiple build environments to accelerate rebuild times and improve CI
efficiency.

The final deployable binary images are generated under:

```
build/tmp/deploy/images/<MACHINE>/
```

For the Cobra EVB reference platform, the image output directory is:
```
build/tmp/deploy/images/mt58xx-cobra-evb/
```

#### Key Image Files

The final deployment directory contains image artifacts used for
development, flashing, deployment, upgrade, recovery, and debugging
purposes.

| File | Description |
|------|-------------|
| `dev-image-*.full.img` | Complete flash image for full device programming and SD card generation |
| `dev-image-*.squashfs-xz` | Compressed root filesystem image using SquashFS with XZ compression |
| `fitImage*.bin` | Linux kernel and Device Tree packaged in FIT image format |
| `u-boot*.itb` | U-Boot bootloader packaged as a FIT image |
| `mtf-fip.bin` | Metanoia firmware image package used during early boot initialization |
| `cobra_lpddr4_3200*.bin` | DDR initialization and training firmware blobs |
| `*.dtb` | Device Tree Blob (DTB) describing board-specific hardware configuration |
| `swupgrade-*.zip` | Software upgrade package used for field or OTA upgrade workflows |
| `*.sysimg` | System deployment image used for manufacturing or deployment flows |
| `*.manifest` | Package manifest listing all software packages included in the image |

Depending on the selected build configuration and deployment profile,
additional debug symbols, SDK artifacts, recovery images, test images,
or intermediate build artifacts may also be generated.

---

## 7. Kernel and Bootloader Updates

### 7.1 Kernel

The supported Linux kernel within the MOSART framework is provided as
the `linux-metanoia` recipe, which contains the Cobra SoC BSP,
platform enablement patches, Device Tree support, and integration
configuration required for the reference platform.

Common kernel development operations include:

```bash
bitbake -c compile linux-metanoia
bitbake -c deploy virtual/kernel
```

Fast iteration is possible via Yocto task scripts (`run.do_compile`).

### 7.2 U-Boot

The MOSART reference platform uses U-Boot as the primary second-stage
bootloader for Cobra SoC platforms.

```bash
bitbake -c compile u-boot
bitbake -c deploy virtual/bootloader
```

---

## 8. Root Filesystem Customization

### 8.1 Adding Packages

User-space functionality within the MOSART Yocto environment is
typically added through:

- Image recipes
- Package groups
- Customer-owned Yocto layers
- `.bbappend` customization mechanisms

This approach preserves maintainability, upgrade compatibility, and
reproducibility across future MOSART SDK releases.

Recommended customization methods include:

- Adding packages through image recipe dependencies
- Creating deployment-specific package groups
- Extending images through customer-managed layers
- Using documented Yocto configuration and overlay mechanisms

Direct modification of platform-owned core recipes is discouraged
unless explicitly documented and supported.

### 8.2 Initramfs Images

Initramfs-based images are supported for:

- Early platform bring-up
- Recovery and rescue workflows
- Manufacturing and deployment testing
- Debug and development use cases

Example build command:

```bash
bitbake dev-image-initramfs
```

---

## 9. Supported Development Workflow (`devtool`)

Yocto `devtool` is the preferred and recommended mechanism for
modifying supported MOSART software components during development.

Example workflow:

```bash
devtool modify linux-metanoia
devtool build linux-metanoia
devtool update-recipe --append ../meta-metanoia linux-metanoia
```

This approach helps ensure that source modifications remain traceable,
reviewable, reproducible, and maintainable across future MOSART
software releases by capturing changes as explicit patches and recipe
extensions.

---

## 10. Upgrade Strategy

MOSART supports multiple upgrade approaches to accommodate different
deployment, operational, and lifecycle management requirements.

Supported upgrade approaches may include:

- **Full image upgrades**  
  Complete device reprogramming workflows such as SD card or eMMC
  image replacement.

- **Partial software updates**  
  Selective component updates such as kernel-only, bootloader-only, or
  root filesystem–only upgrades.

- **Customized deployment-specific upgrade mechanisms**  
  Customers may implement their own upgrade strategies and lifecycle
  management flows using the MOSART open platform according to their
  specific operational, system architecture, or deployment
  requirements.

    - Customers may implement A/B redundancy, rollback protection, or
      OTA lifecycle management frameworks as part of
      deployment-specific upgrade architectures.

On the Cobra SoC reference platforms, the default partition layout,
boot flow, and software upgrade behavior are defined through
Metanoia-provided Yocto image classes and BSP integration layers.

These reference mechanisms are intended to provide a reproducible and
maintainable baseline implementation for development, validation, and
demonstration purposes.

Customers are free to modify, extend, or replace the reference upgrade
strategy according to their own system requirements, manufacturing
flows, deployment architecture, redundancy models, or operational
policies.

Such deployment-specific upgrade solutions may be implemented
independently of Metanoia provided they align with the customer’s
overall system design and operational objectives.

> **Support Disclaimer**
>
> The reference partition layout, boot flow, and software upgrade
> mechanisms provided by Metanoia are intended primarily as reference
> implementations for development and validation.
>
> Upgrade architectures or partition layouts that diverge from the
> documented MOSART reference implementation may fall outside the
> standard MOSART support scope.
>
> Validation, maintenance, integration, and long-term compatibility of
> such customized upgrade mechanisms remain the responsibility of the
> customer or deployment integrator.


## 11. Version Identification

MOSART builds support explicit software version identification and
traceability through build metadata propagation.

Example environment configuration:

```bash
export BB_ENV_PASSTHROUGH_ADDITIONS="METANOIA_TAG METANOIA_HASH METANOIA_BRANCH METANOIA_SDKVERSION"
```
These variables allow the build system to embed version and source
control metadata into generated system artifacts and runtime
identification files.

Typical metadata may include:

- Software release tag
- Git commit hash
- Source branch name
- SDK or platform release version
- Build provenance information

This metadata is commonly propagated into:

- System identification files
- Build manifests
- Runtime version reporting utilities
- Support and diagnostic logs
- Deployment and upgrade metadata

Consistent version identification is important for:

- Build reproducibility
- Software release management
- Deployment tracking
- Upgrade compatibility validation
- Support and issue traceability

Deployment-specific build systems or customer-managed release flows
may extend or customize these metadata mechanisms according to their
own operational requirements.

---

## 12. Debug and Bring-Up

MOSART supports multiple debugging and platform bring-up workflows for
software development, system integration, and low-level platform
validation.

Supported debugging targets may include:

- Boot firmware and early boot stages
- OpenSBI
- U-Boot
- Linux kernel
- Device Tree and BSP bring-up
- User-space applications and services

Standard GDB-based debugging workflows are typically used together
with platform-specific debug probes, UART consoles, JTAG interfaces,
or remote debug servers depending on the deployment environment and
hardware configuration.

Common bring-up activities may include:

- Boot flow validation
- Early console debugging
- DDR initialization verification
- Kernel boot analysis
- Device Tree validation
- Driver and peripheral bring-up
- Platform service debugging
- DSP and subsystem integration testing

Toolchain paths, debug probe configuration, JTAG setup, and remote
debug server environments are deployment-specific and therefore
outside the scope of this public reference guide.

Deployment-specific debugging environments, proprietary tooling, or
customer-specific workflows may vary depending on the target platform,
hardware integration, and operational requirements.

---

## 13. What Is *Not* Covered

This public reference guide intentionally does **not** cover certain
deployment-specific, proprietary, or vendor-internal implementation
details.

Areas outside the scope of this document include:

- PHY, Low-PHY, and Hi-PHY internal implementation details
- DSP firmware architecture and development workflows
- Custom modem, waveform, or Layer-1 algorithm development
- Proprietary vendor-specific radio processing implementations
- Deployment-specific RF tuning and calibration procedures
- Carrier-specific optimization or certification workflows
- Undocumented Yocto layer modifications or unsupported BSP changes
- Proprietary customer integration frameworks and deployment tooling

These areas may remain vendor-internal, proprietary, or fully
customer-owned depending on the deployment model and system
architecture.

Such components and workflows are generally outside the standard
MOSART reference platform support scope unless explicitly documented
or separately agreed upon through commercial support or integration
engagements.

## 14. Summary

The MOSART Cobra Yocto platform provides a reproducible and
maintainable Linux system software environment for Cobra SoC–based
wireless infrastructure platforms.

Key characteristics of the MOSART reference platform include:

- A stable and supported Linux system software stack
- A modular Yocto-based BSP and integration framework
- Clearly defined extension and responsibility boundaries
- Reproducible builds aligned with Cobra SDK software releases
- Controlled customization through documented extension mechanisms
- Long-term maintainability and upgrade compatibility across software
  generations

By following the documented workflows, supported customization
mechanisms, and integration boundaries, developers, partners, and
system integrators can build, customize, validate, and maintain
Cobra-based systems with predictable deployment, upgrade, and support
characteristics.

The MOSART framework is intended to provide an open and extensible
foundation for future wireless infrastructure development while
allowing deployment-specific flexibility for proprietary integrations,
customer customization, and operational requirements.

---

## Legal Notices

### Open-Source Licensing

Unless otherwise specified, MOSART repositories and software
components are released under the open-source licenses documented
within their respective repositories.

Third-party software components may remain subject to their original
upstream licenses and terms.

### Trademark Notice

MOSART™ (Metanoia Open-Source Advanced Radio Technology), Cobra™, and
related names, logos, and branding are trademarks or registered
trademarks of Metanoia Communications Inc. or their respective owners.

Use of the MOSART name, logo, or branding does not grant endorsement,
certification, or official partnership status unless explicitly
authorized by Metanoia.

### Reference Platform Disclaimer

The MOSART platform software framework and reference deployment
examples described in this document are provided for development,
evaluation, integration, and educational purposes.

Commercial deployment architectures, regulatory compliance,
performance validation, security hardening, and production lifecycle
management remain deployment-specific responsibilities unless
explicitly documented otherwise.

