

Welcome to my Homelab Mac Mini Late 2014 Multi OS project! 

This repository is a simple tutorial to help you and document my Homelab build and help anyone how wants to build something similar.

## What I used

- `Mac Mini Late 2014` — The primary machine running the HomeLab environment.
- `Window 10 Boot USB` — A bootable USB drive for installing Windows 10
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

## Windows 10 Boot USB Preparation

`Requirements` 

Before you begin, make sure you have:

A USB flash drive (8 GB or larger)

A working Windows, macOS, or Linux system

A stable internet connection

A valid Windows 10 license (for activation after installation)

balenaEtcher installed: (https://etcher.balena.io)

Windows 10 ISO : (https://www.microsoft.com/en-us/software-download/windows10?msockid=048a50d796596c76364c463797ea6d5f)

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

`Note` Etcher writes the ISO in a raw‑image format. Most systems will boot it normally, but some older BIOS‑only machines may require an MBR‑formatted USB created with other tools.

Flashing the USB will erase all data on it.

Always download Windows ISOs directly from Microsoft.

Etcher is ideal for simple, cross‑platform flashing, but advanced partitioning options (GPT/MBR selection) are not available.

## macOS Windows 10 Partition Installation

## Prepare External Hard Drive

## Ubuntu Boot USB Preparation

## Installation of Ubuntu
