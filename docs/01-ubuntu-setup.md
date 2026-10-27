# 01. Setting Up Ubuntu

The drone simulation guides in this repository use **Ubuntu 20.04 (Focal Fossa)**, with ROS Noetic and Gazebo Classic 11. This page helps you choose a way to run Ubuntu before you install the simulation software.

There are two common ways to run Ubuntu on a Windows PC: inside a virtual machine, or as a second operating system through dual boot. On a Mac, the route depends on whether the Mac has an Intel processor or Apple Silicon (M1, M2, M3, and later).

> **Important version note:** Ubuntu 20.04 reached the end of standard security maintenance on 31 May 2025, and ROS Noetic is also end-of-life. This repository documents an older stack for reproducibility; it is not a recommendation for a new production system. Ubuntu Pro can extend Ubuntu's security maintenance, but it does not bring ROS Noetic back into support. See [Ubuntu's release lifecycle](https://ubuntu.com/about/release-cycle) and the [ROS Noetic end-of-life announcement](https://discourse.openrobotics.org/t/ros-noetic-end-of-life-may-31-2025/43160).

## First: choose your route

| Your computer | Recommended route for a beginner | Do you need a USB drive? | Important limitation |
|---|---|---|---|
| Windows PC with an Intel or AMD processor | VirtualBox virtual machine | **No** | Gazebo's 3D graphics may be slow in a VM. |
| Windows PC with an Intel or AMD processor, and you want Ubuntu running directly on the hardware | Dual boot Windows and Ubuntu | **Yes** | Requires partitioning the drive. Back up first; a mistake can cause data loss. |
| Intel-based Mac | UTM virtual machine using the AMD64 Ubuntu image | **No** | 3D graphics performance may vary. |
| Apple Silicon Mac (M1/M2/M3/…) | UTM virtual machine using an ARM64 Ubuntu image | **No** | The main simulation guide targets `amd64` / `x86_64`; the complete stack has not been verified end-to-end on ARM64. Some steps may need changes. |

**What does dual boot mean?** Windows and Ubuntu are installed separately on the same computer. When you turn the computer on, you choose which operating system to start. You are not running both systems at once.

**Do you need a pen drive?** Only for the usual physical-installation route, such as dual boot. You download an Ubuntu `.iso` file and use a tool to write it to a USB stick, turning the stick into installation media. That process erases the contents of the stick. For a virtual machine, you attach the ISO file directly in the VM settings, so no USB stick is needed.

For this guide, **start with a virtual machine if you are new to Ubuntu**. It keeps the installation separate from your existing operating system and is easier to remove. If Gazebo performs poorly, a native Ubuntu installation or a suitable x86-64 Linux machine may be a better choice.

## Before you start

- A stable internet connection.
- At least **25 GB of free space** for the software stack; more is sensible because source builds and models take up space.
- An account with administrator privileges on the host computer.
- Enough RAM and CPU capacity to run the host operating system and Ubuntu at the same time.

For a virtual machine, **50–64 GB of virtual disk space** is a reasonable starting point. If your host has enough memory, start around **8 GB RAM and 4 virtual CPUs** for the VM. Do not allocate all your computer's memory or CPU cores to Ubuntu; the host still needs resources. Adjust these values to suit your hardware.

## Download Ubuntu

### Windows PCs and Intel Macs

Download the **Ubuntu 20.04.6 Desktop image for 64-bit Intel/AMD PCs (AMD64)** from the official Ubuntu release page:

**[Download Ubuntu 20.04.6 Desktop (AMD64)](https://releases.ubuntu.com/20.04/)**

The downloaded file should be named `ubuntu-20.04.6-desktop-amd64.iso`.

Use the **Desktop** image, not the Server image, for these VM instructions. The desktop environment is useful for Gazebo and other graphical applications.

### Apple Silicon Macs (M1, M2, M3, and later)

Apple Silicon uses the ARM64 architecture. Do **not** attach the AMD64 ISO above to an ARM64 virtual machine.

For this legacy Ubuntu 20.04 setup, an ARM64 Server image is available from the [official Ubuntu 20.04 release directory](https://cdimage.ubuntu.com/ubuntu/releases/20.04/release/). Choose the file whose name ends in `live-server-arm64.iso`. A Server image initially installs a command-line environment; the UTM steps below explain how to add the desktop.

**Compatibility warning:** Installing Ubuntu ARM64 on an Apple Silicon Mac does not guarantee that every command in the main drone simulation guide will work unchanged. The guide's tested target is `amd64` / `x86_64`; treat the ARM64 route as experimental and verify each stage separately. For the closest match to the instructions as written, use an x86-64 Ubuntu environment.

---

## Option A: Windows PC using VirtualBox

This installs Ubuntu **inside a virtual machine**. Windows remains your normal operating system. No pen drive is needed.

### 1. Install VirtualBox

1. Download VirtualBox from the [official VirtualBox downloads page](https://www.virtualbox.org/wiki/Downloads).
2. Run the installer and follow the prompts.
3. Download the Ubuntu 20.04.6 Desktop AMD64 ISO using the link above.

### 2. Create the virtual machine

1. Open VirtualBox and choose **New**.
2. Name the VM `Ubuntu 20.04`.
3. If asked for the operating system type, choose **Linux** and **Ubuntu (64-bit)**.
4. Assign RAM and CPU cores. If the host has sufficient resources, use approximately 8 GB RAM and 4 virtual CPUs as a starting point. Leave resources for Windows.
5. Create a virtual hard disk of approximately 50–64 GB. A dynamically allocated disk grows as files are added, but your physical drive still needs enough free space.
6. If VirtualBox asks for an installation image, select `ubuntu-20.04.6-desktop-amd64.iso`. Otherwise, open the VM's **Settings → Storage**, select the empty optical drive, and attach the ISO there.

### 3. Install Ubuntu inside the VM

1. Select the VM and click **Start**.
2. Choose **Try or Install Ubuntu**, then select **Install Ubuntu**.
3. Follow the language, keyboard, network, account, and installation prompts.
4. If the installer presents **Erase disk and install Ubuntu**, only proceed if you have confirmed that the selected disk is the VM's virtual disk. It must not be your physical Windows drive. If you cannot tell which disk is selected, stop rather than guess.
5. When the installation completes, restart the VM. If it returns to the installer, eject the ISO from the VM's virtual optical drive and restart again.

Ubuntu should now open in a window while Windows continues running underneath it. You can shut down Ubuntu like a separate computer and start it again from VirtualBox whenever you need it.

### What about dual boot on Windows?

Dual boot is an alternative to VirtualBox, not a requirement. It can give Ubuntu more direct access to the computer's hardware, which may help a 3D simulator, but it changes the computer's disk layout and needs more care.

A typical dual-boot installation requires a bootable USB stick of **8 GB or larger**. Creating the installer erases everything on that USB stick. Before you start:

1. Back up important files to a different drive or cloud location.
2. Make sure you have access to your Windows recovery key if device encryption or BitLocker is enabled.
3. Check that the computer has enough disk space for Ubuntu. Use Windows Disk Management to shrink the Windows partition and leave unallocated space for Ubuntu; do not delete the Windows partition.
4. Download the Ubuntu ISO, then use a tool such as [Rufus](https://rufus.ie/) to write it to the USB stick. This is not the same as copying the ISO file onto the stick.
5. Restart the computer and use its boot menu to start from the USB stick.
6. In the Ubuntu installer, choose **Install Ubuntu alongside Windows** if that option is shown and you understand the disk selected. **Do not choose “Erase disk and install Ubuntu” if you want to keep Windows.** If the installer does not offer a safe alongside-Windows option, cancel and investigate before making changes.
7. Finish the installation and restart. A boot menu should let you choose Ubuntu or Windows. The USB stick is only needed for installation; you do not need to keep it plugged in for dual boot.

If BitLocker/device encryption is enabled, the installer may not be able to safely install Ubuntu alongside Windows. Intel RST storage settings can also prevent the installer from detecting the drive. Read the relevant [official Ubuntu BitLocker guidance](https://ubuntu.com/desktop/docs/en/latest/reference/bitlocker-during-ubuntu-installation/) and [Intel RST guidance](https://ubuntu.com/desktop/docs/en/latest/reference/intel-rst-during-ubuntu-installation/) before proceeding. If you are unfamiliar with partitions or recovery keys, use the VirtualBox route instead.

For a broader overview, see [Ubuntu's official installation guide](https://ubuntu.com/desktop/docs/en/latest/tutorial/install-ubuntu-desktop/). The screens may look different because this repository uses Ubuntu 20.04 and the official site may show instructions for a newer release.

---

## Option B: Mac using UTM

UTM lets you run Ubuntu in a window on macOS. You do not need a pen drive. The exact ISO and compatibility depend on whether your Mac has an Intel processor or Apple Silicon.

### 1. Install UTM

1. Download UTM from the [official UTM website](https://utm.app/).
2. Install and open UTM.

### 2A. Intel Mac

1. Download the Ubuntu 20.04.6 Desktop AMD64 ISO from the [official Ubuntu release page](https://releases.ubuntu.com/20.04/).
2. In UTM, click **+** to create a VM.
3. Choose **Virtualize**, then **Linux**.
4. Select the Ubuntu AMD64 ISO when prompted.
5. Assign suitable RAM and CPU resources, and create a virtual disk of about 50–64 GB.
6. Save the VM, start it, and follow the Ubuntu installation steps. During installation, ensure you are working on the VM's virtual disk, not any physical drive.

### 2B. Apple Silicon Mac (M1, M2, M3, and later)

1. Download the Ubuntu 20.04 ARM64 Server ISO from the [official Ubuntu 20.04 release directory](https://cdimage.ubuntu.com/ubuntu/releases/20.04/release/). Select the file ending in `live-server-arm64.iso`.
2. In UTM, click **+** to create a VM.
3. Choose **Virtualize**, then **Linux**.
4. Select the ARM64 Server ISO. Allocate RAM and CPU resources without starving macOS, and create a virtual disk of about 50–64 GB.
5. Save the VM and start it. Follow the Ubuntu Server installer, creating a username and password. When installation finishes, shut down the VM if it does not restart cleanly.
6. Before starting it again, open the VM settings and eject or clear the installer ISO, then start the VM from its new virtual disk.
7. Sign in at the terminal and install the Ubuntu desktop environment:

   ```bash
   sudo apt update
   sudo apt install ubuntu-desktop
   sudo reboot
   ```

After the reboot, Ubuntu should launch its graphical desktop. If it does not, consult the [UTM Ubuntu guide](https://docs.getutm.app/guides/ubuntu/) for troubleshooting steps.

**Important:** This gives you an Ubuntu ARM64 VM; it does not turn the VM into an AMD64 computer. The full drone simulation stack in this repository has not been verified end-to-end on Apple Silicon/ARM64. If a later stage fails because of architecture-specific packages, paths, or binaries, do not assume the Ubuntu installation itself is broken. The most reliable way to follow the main guide exactly is to use an x86-64 Ubuntu environment.

---

## Verify Ubuntu before continuing

Open a terminal inside Ubuntu and run:

```bash
lsb_release -a
uname -m
dpkg --print-architecture
df -h /
```

For the x86-64 setup assumed by the main simulation guide, expect:

```text
Release: 20.04
Codename: focal
x86_64
amd64
```

The `df -h /` output includes an `Avail` column. Check that at least 25 GB is available on the root filesystem before installing the simulation stack.

If you see Ubuntu 22.04/24.04, or `aarch64`/`arm64`, pause before continuing. The following guides are version- and architecture-specific; do not mix instructions from a different Ubuntu or ROS setup into this one.

## A note on Gazebo performance

Gazebo is a 3D simulator, and virtual machines do not provide the same graphics performance on every host. You may see low frame rates or graphics issues. Increasing VM memory alone will not solve every graphics limitation. If the simulator is unusably slow, consider a suitable native x86-64 Ubuntu installation or another Linux machine.

## Next step

Once Ubuntu reports `20.04` / `focal`, confirm the architecture, and check your available disk space, continue to [Understanding the Simulation Stack](02-understanding-the-stack.md).

## Official references

- [Ubuntu 20.04 downloads](https://releases.ubuntu.com/20.04/)
- [VirtualBox downloads](https://www.virtualbox.org/wiki/Downloads)
- [UTM](https://utm.app/)
- [UTM's Ubuntu guide](https://docs.getutm.app/guides/ubuntu/)
- [Ubuntu installation guide](https://ubuntu.com/desktop/docs/en/latest/tutorial/install-ubuntu-desktop/)
- [Create a bootable USB stick](https://ubuntu.com/desktop/docs/en/latest/how-to/create-a-bootable-usb-stick/)
- [Ubuntu 20.04 support lifecycle](https://ubuntu.com/about/release-cycle)
- [ROS Noetic end of life](https://discourse.openrobotics.org/t/ros-noetic-end-of-life-may-31-2025/43160)
