# Kali Linux Setup on macOS Using Oracle VirtualBox

## Project Overview

This project documents the setup of a Kali Linux virtual machine (VM) on
a macOS host using Oracle VirtualBox. The goal is to create an isolated
lab environment for learning Linux fundamentals and practicing
cybersecurity concepts safely.

## Objectives

-   Install Oracle VirtualBox on macOS.
-   Download the appropriate Kali Linux installer image.
-   Create and configure a Kali Linux virtual machine.
-   Install Kali Linux and boot to its desktop.
-   Configure networking for the lab.
-   Take a VM snapshot as a recovery point.

## Host and Virtual Machine Details

  Item                        Configuration
  --------------------------- -----------------------------------
  Host operating system       macOS
  Virtualization software     Oracle VirtualBox 7.2.22
  Guest operating system      Kali Linux
  Installer image shown       Kali Linux ARM64 installer ISO
  VM name                     `kalilinux`
  Virtual disk                25 GB, dynamically allocated VDI
  Network adapter shown       Intel PRO/1000 MT Desktop (NAT)
  USB controller shown        USB 3.0 (xHCI)
  Display memory configured   128 MB in the settings screenshot

> **Architecture note:** The screenshots show an ARM64 Kali installer.
> Use the Apple Silicon host package and an ARM64 Kali image on an Apple
> Silicon Mac. On an Intel Mac, use the Intel host package and a
> compatible x86-64 Kali image. Do not mix host and guest architectures.

## Prerequisites

-   A Mac with sufficient free storage and memory.
-   Oracle VirtualBox for the Mac's processor architecture.
-   The matching Kali Linux installer ISO.
-   A stable internet connection.

## Setup Procedure

### 1. Install VirtualBox

1.  Open the official [VirtualBox downloads
    page](https://www.virtualbox.org/wiki/Downloads).
2.  Download the macOS host package that matches your Mac:
    -   **macOS / Apple Silicon hosts** for M-series Macs.
    -   **macOS / Intel hosts** for Intel-based Macs.
3.  Open the downloaded `.dmg` file and run `VirtualBox.pkg`.
4.  Follow the installer prompts and approve any macOS security prompt
    if required.
5.  Open VirtualBox from the Applications folder.

### 2. Download Kali Linux

1.  Visit the official [Kali Linux download
    page](https://www.kali.org/get-kali/).
2.  Download the installer image matching your Mac's architecture.
3.  Keep the ISO file in a known folder so it can be selected in
    VirtualBox.

### 3. Create and Configure the VM

1.  In VirtualBox, select **New**.
2.  Set the VM name to `kalilinux`.
3.  Select the appropriate Linux type and architecture for the Kali
    image.
4.  Assign memory appropriate for the Mac (the screenshots show
    approximately 3.5 GB).
5.  Create a virtual hard disk. The example VM uses a 25 GB dynamically
    allocated VDI.
6.  Open **Settings → Storage** and attach the Kali installer ISO to the
    optical drive.
7.  Open **Settings → Display** and set video memory to 128 MB if
    supported.
8.  Review **System**, **Network**, and other settings before starting
    the VM.

### 4. Install Kali Linux

1.  Select the `kalilinux` VM and click **Start**.
2.  Follow the Kali installer prompts.
3.  Choose the required language, location, keyboard layout, user
    account, and installation options.
4.  Select the virtual disk for installation.
5.  Complete installation and reboot the VM.
6.  If the installer starts again after reboot, detach the ISO from
    **Settings → Storage** and start the VM again.
7.  Log in and confirm that the Kali desktop loads.

### 5. Configure Networking

The supplied VM details screenshot shows the adapter set to **NAT**. The
lab instructions call for a **NAT Network** using `10.0.0.0/24`; these
are not the same VirtualBox networking mode.

To configure the requested lab network:

1.  Open VirtualBox **Preferences / Tools → Network** (the location may
    vary by VirtualBox version).

2.  Create a NAT Network.

3.  Set its IPv4 prefix to `10.0.0.0/24` and enable DHCP if your lab
    requires it.

4.  Open the Kali VM's **Settings → Network**.

5.  Set **Attached to** to **NAT Network**, then select the network you
    created.

6.  Start Kali and check the assigned address with:

    ``` bash
    ip addr
    ip route
    ```

7.  Confirm connectivity only to systems you own or are authorized to
    test.

### 6. Take a Snapshot

1.  Shut down Kali cleanly, or use a powered-off state for a consistent
    snapshot.
2.  Select the VM in VirtualBox.
3.  Open **Snapshots** and choose **Take**.
4.  Give the snapshot a clear name, such as
    `Kali Linux - Initial Setup`.
5.  Add a short description and save it.

A snapshot provides a restore point before future lab changes.

## Evidence / Screenshots

Create a folder named `screenshots` in this repository and add your
screenshots using these suggested filenames:

  Suggested filename                 Evidence
  ---------------------------------- -----------------------------------------
  `01-virtualbox-installation.png`   VirtualBox installer on macOS
  `02-virtualbox-home.png`           VirtualBox Manager home screen
  `03-kali-iso-download.png`         Kali download page / selected installer
  `04-vm-display-settings.png`       VM display settings
  `05-vm-storage-settings.png`       Virtual disk and Kali ISO attached
  `06-vm-usb-settings.png`           USB controller settings
  `07-vm-summary.png`                VM configuration summary
  `08-kali-login.png`                Kali login screen
  `09-kali-desktop.png`              Kali desktop after successful boot

Update the filenames in this table if you use different names. Only
include screenshots that you have actually captured.

## Optional Phase 2

These are future extensions and are not required for the initial setup:

-   Install additional Windows or Linux virtual machines.
-   Place lab VMs on the same isolated NAT Network.
-   Perform basic connectivity checks between your own lab VMs.
-   Take snapshots before major configuration changes.

## Troubleshooting

-   **VM does not start:** Check that the ISO and VM architecture match
    the Mac's processor architecture.
-   **Black screen or display issues:** Check the VM's graphics
    controller and video memory; power off the VM before changing
    settings.
-   **Installer starts on every boot:** Detach the installer ISO after
    Kali has been installed.
-   **No network connection:** Confirm the selected adapter mode, NAT
    Network selection, DHCP settings, and Kali network interface.
-   **USB device is unavailable:** Check the USB controller setting and
    macOS permissions. Install the Extension Pack only if your required
    USB feature needs it, using a version compatible with your
    VirtualBox release.

## Learning Outcomes

After completing this project, you should be able to:

-   Explain the role of a hypervisor and virtual machine.
-   Install VirtualBox on macOS.
-   Select a guest OS image that matches the host architecture.
-   Configure virtual CPU, memory, storage, display, and networking.
-   Boot and use a Kali Linux virtual machine.
-   Create and restore VM snapshots.

## Safety and Responsible Use

Use Kali Linux tools only in systems and networks that you own or have
explicit permission to test. Keep experiments inside your isolated lab
environment.

## References

-   [Oracle VirtualBox
    Downloads](https://www.virtualbox.org/wiki/Downloads)
-   [Oracle VirtualBox User Manual](https://www.virtualbox.org/manual/)
-   [Kali Linux Get Kali](https://www.kali.org/get-kali/)

------------------------------------------------------------------------

**Project status:** Kali Linux has been booted to the desktop in the
supplied screenshots. Verify the NAT Network configuration and create a
snapshot before marking those tasks complete.
