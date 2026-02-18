

# Mac Mini Late 2014 — Triple‑Boot HomeLab Setup 

A fully documented HomeLab project built on a **Mac Mini Late 2014**, upgraded with external storage and configured to run **macOS**, **Windows 10**, and **Ubuntu Linux**. This repository tracks the evolution of the setup, installation steps, configurations, and experiments along the way.

## 🚀Project Overview 

This project demonstrates how to transform an older Mac Mini into a flexible HomeLab environment capable of running multiple operating systems for learning, testing, and experimentation. 

You will learn how to:

- Prepare macOS for multi‑booting
- Create Windows 10 and Ubuntu bootable USB installers
- Install Windows 10 using Boot Camp Assistant
- Install Ubuntu on an external hard drive
- Configure partitions safely without breaking macOS
- Boot each OS reliably using the Mac startup manager

---

## 🖥️Hardware Used

- **Mac Mini Late 2014** (base system)
- **Windows 10 Boot USB** (8–16 GB)
- **Ubuntu Boot USB** (8–16 GB)
- **External Hard Drive** (1 TB Western Digital HDD)
- **SATA‑to‑USB 2.5" Adapter**
- **Keyboard, Mouse, HDMI Display**

--- 

## 🧰Software & Tools
- **balenaEtcher** — Create bootable USB installers https://etcher.balena.io
- **Windows 10 ISO** https://www.microsoft.com/en-us/software-download/windows10
- **Ubuntu Desktop ISO** https://ubuntu.com/download/desktop

---

## Table of Contents
- [Project Overview](#project-overview)
- [Hardware Used](#️hardware-used)
- [Software & Tools](#software--tools)
- [1. macOS Update & Preparation](#1macos-update--preparation)
- [2. Create Windows 10 Boot USB](#2create-windows-10-boot-usb)
- [3. Install Windows 10 Using Boot Camp Assistant](#3install-windows-10-using-boot-camp-assistant)
- [4. Prepare External Hard Drive for Ubuntu](#4prepare-external-hard-drive-for-ubuntu)
- [5. Create Ubuntu Boot USB](#5create-ubuntu-boot-usb)
- [6. Install Ubuntu on External Drive](#6install-ubuntu-on-external-drive)
- [7. Booting Between macOS Windows and Ubuntu](#7booting-between-macos-windows-and-ubuntu)
- [Final Result](#final-result)

---

## 🍎1.macOS Update & Preparation

- Check the macOS version and update to the latest supported version for the 2014 Mac Mini.
- Avoid installing unsupported macOS versions.
- After updating, prepare the system for partitioning.

`Warning` I do not recommend attempting to install a macOS version that is not officially supported on the Mac Mini.

--- 

## 🪟2.Create Windows 10 Boot USB (balenaEtcher)

This section explains how to create a bootable Windows 10 USB installer using balenaEtcher, a simple and cross‑platform flashing tool. The resulting USB can be used to install or repair Windows 10 on compatible hardware.

`Requirements` 

- USB drive (8 GB+)
- Windows 10 ISO
- balenaEtcher installed

**Steps** 
1. Download the Windows 10 ISO from Microsoft.
2. Open balenaEtcher → *Flash from file* → select ISO.
3. Choose the USB drive → *Flash*.
4. Wait for validation to complete.

`Notes` 

-Etcher writes the ISO in a raw‑image format. Most systems will boot it normally, but some older BIOS‑only machines may require an MBR‑formatted USB created with other tools.

-Flashing the USB will erase all data on it.

-Always download Windows ISOs directly from Microsoft.

-Etcher is ideal for simple, cross‑platform flashing, but advanced partitioning options (GPT/MBR selection) are not available.

---

## 🪟3.Install Windows 10 Using Boot Camp Assistant

This guide explains how to install Windows 10 on a macOS Monterey system using Boot Camp Assistant together with a Windows 10 bootable USB. This method is designed for older Macs—such as the Mac mini (Late 2014)—where Boot Camp Assistant may not automatically create a USB installer but still supports partitioning and installation.

`Requirements`

- macOS Monterey
- Windows 10 ISO
- Bootable USB installer
- 40 GB+ free disk space

**Steps**
1. Open **Boot Camp Assistant**.
2. Create the Windows partition.
3. Reboot and hold **Option (⌥)**.
4. Select **EFI Boot** (USB).
5. Format the BOOTCAMP partition → install Windows.

`Notes`

-Boot Camp Assistant on Monterey still handles partitioning correctly even if it no longer creates USB installers.

-Using a manually created USB installer is the most reliable method for older Macs.

-Always back up macOS before modifying partitions.

---

## 💾4.Prepare External Hard Drive for Ubuntu

You will create two partitions:

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

---

## 🐧5.Create Ubuntu Boot USB (balenaEtcher)

Same process as Windows: 

1. Download Ubuntu ISO.
2. Flash using balenaEtcher.

`Notes` 

-Etcher writes the ISO in a raw‑image format. Most systems will boot it normally, but some older BIOS‑only machines may require an MBR‑formatted USB created with other tools.

-Flashing the USB will erase all data on it.

-Always download Windows ISOs directly from Ubuntu.

-Etcher is ideal for simple, cross‑platform flashing, but advanced partitioning options (GPT/MBR selection) are not available.

---

## 🐧6.Install Ubuntu on External Drive

**Steps**
Step 1 — Boot the Mac Mini From the USB Installer

1. Plug in:
  -The Ubuntu USB installer
  -The external hard drive (target install disk
2.  Boot Mac → hold **Option (⌥)** → choose **EFI Boot**.
3.   Select **Install Ubuntu**.
4.   Select the external drive (usually `/dev/sdb`).
5.   Create:
   - EFI (512 MB, FAT32, `/boot/efi`)
   - Root (ext4, `/`)
   - Swap (4–8 GB)
   - Home (optional)
6.Install GRUB to the external drive (NOT `/dev/sda`).

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
  
Step 5 — Finish Installation

1. Let the installer complete.

2. Shut down the Mac mini.

3. Remove the USB installer.

4. Keep the external Ubuntu drive connected.

Step 6 — Boot Ubuntu From the External Drive

1. Power on the Mac mini.

2. Hold Option (⌥) or Alt during startup.

3. Select EFI Boot (your external Ubuntu drive).

Ubuntu should now start normally.

---

## 🔄7.Booting Between OSes

- Hold **Option (⌥) or Alt ** during startup.
- Choose:
  - **Macintosh HD** → macOS
  - **EFI Boot** → Windows
  - **EFI Boot (External)** → Ubuntu
 
 ---
    
## 🎉Final Result

You now have a fully functional **triple‑boot HomeLab** running on a Mac Mini Late 2014 — perfect for:

- Linux administration practice
- Windows testing
- macOS development
- Networking & virtualization experiments
- Portable Linux environment
