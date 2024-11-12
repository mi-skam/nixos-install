# NixOS Installation Guide

## Introduction
This guide will walk you through the process of setting up a NixOS aarch64 virtual machine (VM) on macOS using the UTM QEMU frontend. Follow the steps below to get started.

## Prerequisites
- macOS installed on your machine
- UTM application installed (download from [UTM](https://mac.getutm.app/))
- NixOS ISO for aarch64 (download from [NixOS Downloads](https://nixos.org/download.html))

## Steps

### 1. Download NixOS ISO
Download the NixOS ISO for aarch64 from the [NixOS Downloads](https://nixos.org/download.html) page.

### 2. Install UTM
If you haven't already, download and install the UTM application from [UTM](https://mac.getutm.app/).

### 3. Create a New Virtual Machine
1. Open UTM and click on the "+" button to create a new VM.
2. Select "Virtualize" and click "Next".
3. Choose "Linux" as the operating system and click "Next".
4. Name your VM (e.g., "NixOS aarch64") and click "Next".

### 4. Configure the VM
1. **System**:
   - Set the architecture to "aarch64".
   - Allocate at least 2 GB of RAM.
   - Set the CPU cores to 2 or more.

2. **Drives**:
   - Add a new drive and set the size to at least 20 GB.
   - Add the NixOS ISO as a removable drive.

3. **Network**:
   - Enable network access by selecting "Emulated" and choosing a network interface.

### 5. Boot the VM
1. Start the VM by clicking the "Play" button.
2. The VM should boot from the NixOS ISO. You will see the NixOS boot menu.
3. Select the default option to start the NixOS live environment.

### 6. Install NixOS
1. Once in the NixOS live environment, open a terminal.
2. Partition the disk:
   ```sh
   parted /dev/vda -- mklabel gpt
   parted /dev/vda -- mkpart primary 512MiB 100%
   parted /dev/vda -- mkpart ESP fat32 1MiB 512MiB
   parted /dev/vda -- set 2 boot on
   mkfs.ext4 -L nixos /dev/vda1
   mkfs.fat -F 32 -n boot /dev/vda2