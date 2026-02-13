

Welcome to my Homelab Mac Mini Late 2014 Multi OS project! 

This repository is a simple tutorial to help you and document my Homelab build and help anyone how wants to build something similar.

## What I used

- `Mac Mini Late 2014` — The primary machine running the HomeLab environment.
 
- `Window 10 Boot USB` — A bootable USB drive for installing Windows 10. Recommended size: 8–16 GB
 
- `Ubuntu Boot USB` —   A bootable USB drive for installing Ubuntu/Linux. Recommended size: 8–16 GB
 
- `External Hard Drive` —  Used for Ubuntu/Linux installation and additional storage. Current setup uses a 1 TB Western Digital Hard Disk Drive , 2.5-inch
 
- `Sata to USB Cable` — Sata to USB cable/enclouse to be able to use the external HHD
 
- `Extras` — Mouse,Keyboard,HDMI,Extra Computer

## Programs

- `Balena Etcher` — We use this to create a OS Boor USB/ Burn ISO into a USB. (https://etcher.balena.io/)


## Websites

- `Window 10 ISO` — (https://www.microsoft.com/en-us/software-download/windows10?msockid=048a50d796596c76364c463797ea6d5f)
 
- `Ubuntu ISO` — (https://ubuntu.com/download/desktop)

## Table of Contents

Table of Contents

1. macOS Update and Preparation

2. Windows 10 Boot USB Preparation

3. macOS Windows 10 Partition Installation

4. Prepare External Hard Drive

5. Ubuntu Boot USB Preparation

6. Ubuntu Installation


## Setup

## macOS Update and Preparation

-Begin by checking which version of macOS the Mac Mini is currently running.

-Verify whether this version is the latest operating system supported by the device.

-Once the appropriate macOS version has been downloaded and installed, you can proceed with partitioning the system.

`Warning` I do not recommend attempting to install a macOS version that is not officially supported on the Mac Mini.

## Windows 10 Boot USB Preparation (Using balenaEtcher)

This section explains how to create a bootable Windows 10 USB installer using balenaEtcher, a simple and cross‑platform flashing tool. The resulting USB can be used to install or repair Windows 10 on compatible hardware.

`Requirements` 

Before you begin, make sure you have:

-A USB flash drive (8 GB or larger)

-A working Windows, macOS, or Linux system

-A stable internet connection

-balenaEtcher installed: (https://etcher.balena.io)

-Windows 10 ISO : (https://www.microsoft.com/en-us/software-download/windows10?msockid=048a50d796596c76364c463797ea6d5f)

Step 1 — Download the Windows 10 ISO

From Microsoft (Recommended)

1.  Visit the official Microsoft download page:
(https://www.microsoft.com/en-us/software-download/windows10?msockid=048a50d796596c76364c463797ea6d5f)

2. Scroll to Create Windows 10 installation media “Download Now - Windows 10 Disk Image (ISO File)”.

3. Wait until it finish downloading.

Step 2 — Create the Bootable USB with Etcher

balenaEtcher works the same across Windows, macOS, and Linux.

1.  Visit the official balenaEtcher download page:  (https://etcher.balena.io)

2. Install and open balenaEtcher. 

3. Click Flash from file and select the Windows 10 ISO.

4. Click Select target and choose your USB drive.

5. Click Flash!

6. Wait for Etcher to finish writing and validating the USB.

`Notes` 

-Etcher writes the ISO in a raw‑image format. Most systems will boot it normally, but some older BIOS‑only machines may require an MBR‑formatted USB created with other tools.

-Flashing the USB will erase all data on it.

-Always download Windows ISOs directly from Microsoft.

-Etcher is ideal for simple, cross‑platform flashing, but advanced partitioning options (GPT/MBR selection) are not available.

## macOS Monterey — Windows 10 Installation Using Boot Camp Assistant (With Windows 10 Boot USB)

This guide explains how to install Windows 10 on a macOS Monterey system using Boot Camp Assistant together with a Windows 10 bootable USB. This method is designed for older Macs—such as the Mac mini (Late 2014)—where Boot Camp Assistant may not automatically create a USB installer but still supports partitioning and installation.

`Requirements`

-macOS Monterey

-A Mac that supports Windows 10 installation (tested on Mac mini 2014)

-Windows 10 ISO file

-Bootable Windows 10 USB (created with balenaEtcher)

-At least 40 GB of free disk space

-USB keyboard/mouse recommended

-Internet connection for driver installation

Step 1 — Open Boot Camp Assistant

1. On macOS, open:
Applications → Utilities → Boot Camp Assistant

2. Boot Camp Assistant may not show the option to create a USB installer on Monterey, but it still supports partitioning.

3. Click Continue.

Step 2 - Create the Windows Partition

1. In Boot Camp Assistant, adjust the partition slider.

2. Allocate amount GB for Windows (your choice).

3. Click Install.

4. Boot Camp Assistant will:

-Resize the macOS partition

-Create a BOOTCAMP partition

-Restart the Mac

`Note` Boot Camp Assistant will reboot, but it may not automatically detect the USB installer. That’s expected on older Macs.

Step 3 - Boot From the Windows 10 USB

1. When the Mac restarts, immediately hold Option (⌥) Alt for regular keyboard.

2. Select EFI Boot (your Windows USB).

3. The Windows installer will load.

Step 4 - Install Windows 10

1. Choose your language and click Install Now.

2. Enter your product key or skip for later activation.

3.Select Windows 10 Home or Pro.(doesn't show sometimes)

4. When asked where to install Windows:

-Select the BOOTCAMP partition

-Click Format

-Click Next

`Do not delete or modify macOS partitions.` Only format the BOOTCAMP partition.

Step 5 - Complete Installation

Windows will reboot several times.
If it boots into macOS:

1. Restart

2. Hold Option (⌥) or Alt

3. Select Windows

Continue setup until you reach the Windows desktop.

`Notes`

-Boot Camp Assistant on Monterey still handles partitioning correctly even if it no longer creates USB installers.

-Using a manually created USB installer is the most reliable method for older Macs.

-Always back up macOS before modifying partitions.

## Prepare External Hard Drive

You will be doing three main things:

1. Back up the drive (everything will be erased).

2. Partition the drive into:

 -A bootable Linux OS partition

 -A shared storage partition

Step 1 — Back Up the Drive
 
Before anything else, copy any important files off the external drive. Partitioning will wipe it.

Step 2 — Partition the External Drive

`On macOS (Disk Utility)`

This is the cleanest method for your Mac mini setup.

Steps:

1. Open Disk Utility

2. In the top-left, choose View → Show All Devices

3. Select the physical external drive (not the volume under it)

4. Click Erase

-Format: GUID Partition Map (GPT)

-File system: ExFAT (temporary; we’ll repartition next)

5. After erase completes, click Partition

6. Create two partitions:

-Linux OS partition

   -Name: LinuxOS

   -Format: MS-DOS (FAT) (Linux installer will reformat it to ext4)

   -Size:  GB depending on your needs

-Storage partition

  -Name: Storage

  -Format: ExFAT (works on macOS, Windows, Linux)

  -Size: the rest of the drive

`Why FAT for the Linux partition?`

Linux installers can’t install directly onto APFS or ExFAT. FAT is just a placeholder; the installer will convert it to ext4 or btrfs.

`On Windows (Disk Management)`

Steps:

1. Open diskmgmt.msc

2. Right‑click the external drive → Delete Volume until it’s unallocated

3. Right‑click → New Simple Volume

4. Create:

  -Partition 1: LinuxOS → Format FAT32

  -Partition 2: Storage → Format NTFS or exFAT

`Note`

For me what it work when installing linux on the external Hard drive so it reconasizes it to make the hard drive unallocated

`Windows: Make an External Drive Unallocated`

`Warning`

This erases all data on the external drive. Double‑check you selected the correct disk.

Steps (Disk Management)

1. Connect the external drive to your PC.

2. Press Win + X → choose Disk Management.

3. In the bottom panel, find your external drive (look for the correct size).

4. Right‑click each partition on that drive → choose Delete Volume.

   -Repeat until the entire drive shows black bar labeled Unallocated.

5. That’s it — the drive is now unallocated.

`macOS: Make an External Drive Unallocated`

macOS doesn’t show “unallocated” the same way Windows does, but you can erase the drive so it has no partitions except free space.

`Warning`

This also erases all data.

Steps (Disk Utility)

1. Connect the external drive.

2. Open Disk Utility (Applications → Utilities).

3. In the top-left, click View → Show All Devices.

4. Select the physical drive (not the volume under it).

5. Click Erase.

6. Choose:

  -Format: Free Space (if available) or a placeholder format like ExFAT

  -Scheme: GUID Partition Map

7. Click Erase.

## Ubuntu Boot USB Preparation (Using balenaEtcher)

This section explains how to create a bootable Ubuntu USB installer using balenaEtcher, a simple and cross‑platform flashing tool. The resulting USB can be used to install or repair Ubuntu on compatible hardware.

`Requirements` 

Before you begin, make sure you have:

-A USB flash drive (8 GB or larger)

-A working Windows, macOS, or Linux system

-A stable internet connection

-balenaEtcher installed: (https://etcher.balena.io)

-Ubuntu ISO : (https://ubuntu.com/download/desktop)

Step 1 — Download the Ubuntu ISO

From Ubuntu (Recommended)

1.  Visit the official Ubuntu download page:
(https://ubuntu.com/download/desktop)

2. Scroll to Ubuntu latest OS page “Download the Ubuntu version you want to install (ISO File)”.

3. Wait until it finish downloading.

Step 2 — Create the Bootable USB with Etcher

balenaEtcher works the same across Windows, macOS, and Linux.

1.  Visit the official balenaEtcher download page:  (https://etcher.balena.io)

2. Install and open balenaEtcher. 

3. Click Flash from file and select the Ubuntu ISO.

4. Click Select target and choose your USB drive.

5. Click Flash!

6. Wait for Etcher to finish writing and validating the USB.

`Notes` 

-Etcher writes the ISO in a raw‑image format. Most systems will boot it normally, but some older BIOS‑only machines may require an MBR‑formatted USB created with other tools.

-Flashing the USB will erase all data on it.

-Always download Windows ISOs directly from Ubuntu.

-Etcher is ideal for simple, cross‑platform flashing, but advanced partitioning options (GPT/MBR selection) are not available.

## Installation of Ubuntu

Step 1 — Boot the Mac Mini From the USB Installer

1. Plug in:

  -The Ubuntu USB installer

  -The external hard drive (target install disk)

2. Restart the Mac mini.

3. Hold Option (⌥) or Alt immediately after the chime.

4. Select EFI Boot (this is the Ubuntu installer).

Step 2 — Start Ubuntu Installer

1. When Ubuntu loads, choose:

  -Try or Install Ubuntu → Install Ubuntu

`IMPORTANT: Manual Partitioning (So You Don’t Break macOS)`

This is the critical part.

When you reach Installation Type, choose:

✔️ “Something else”

This prevents Ubuntu from overwriting your internal macOS disk.

Step 3 — Partition the External Hard Drive for Ubuntu

When the Ubuntu installer reaches the partitioning screen:

1. Select your external drive

  -Usually /dev/sdb or /dev/sdc

  -Do NOT select /dev/sda — that’s your internal macOS drive
  
2. Create the following partitions:

`Example`

Partition | Size | Type |	Mount Point |

EFI System Partition |	512 MB |	FAT32 |	/boot/efi |

Root | 20–50 GB	| ext4 | / |

Swap	| 4–8 GB |	swap | (none) |

Home (optional)	| Remaining | ext4 |	/home |

Step 4 — Install GRUB to the External Drive

-At the bottom of the partitioning window:

-Device for bootloader installation:  
 
  Example: /dev/sdb

`Do NOT choose:`

- /dev/sdb1

- /dev/sda (your internal macOS disk)

This ensures Ubuntu only boots when the external drive is connected.
  

