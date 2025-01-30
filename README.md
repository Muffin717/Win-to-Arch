# Win-to-Arch: A Simple Guide for Migrating from Windows to Arch Linux

## Introduction

**Win-to-Arch** is a simple step-by-step guide, completely written by myself to help anyone who would like to switch from their Windows 10/11 system to an Arch Linux-based system while keeping the process as simple as possible without adding any unnecessary bloat to the operating system.

I believe the best way to do this is to share experience; therefore, this guide will be mostly based on my personal experience on this journey, tailored to fit anyone who is on the same path.

> **⚠ WARNING:** Win-to-Arch targets users who have a certain amount of knowledge about GNU/Linux and are comfortable with using the terminal. Even though this document aims to make Arch as user-friendly and graphical as possible, please ensure you do enough research about GNU/Linux and the terminal before attempting the migration, as you will need to use the terminal to resolve issues or even install packages/applications.
>
> Everything that is aimed to be used in this guide is completely free and open-source software.

---

## Preparing Arch Installation

Arch Linux by itself does not have any graphical installation screen, which may be difficult for those who would like to use the simplicity and lightweight nature of Arch without the hassle or risk of messing up the installation.

Therefore, the best option for this case would be using **EndeavourOS**. EndeavourOS is an Arch-based operating system that follows the same principles as Arch and is the most popular Arch-based distro according to Distrowatch.

To install Arch (EndeavourOS), you will need to create a bootable drive. The recommended method is to use a USB stick (minimum **2 GB recommended**) and turn it into a bootable drive, which will be used to install EndeavourOS.

On Windows 10/11, there are multiple tools that can execute this task, such as **Ventoy** and **Rufus**. The recommended program for this guide is **Rufus**, as it is the one I have used, but feel free to use any other tool if you know how to.

### Steps to Create a Bootable USB Drive

#### 1. Download Rufus
- Visit the [official Rufus website](https://rufus.ie/) and download the version suitable for your system.
- (Optional) Choose between the **standard** or **portable** versions.

#### 2. Download EndeavourOS ISO
- Visit the [official EndeavourOS website](https://endeavouros.com/) and download the latest ISO version from the listed mirrors.
- Also, download the **signature file**.
- For faster downloads, choose a mirror closest to your geographical location.

#### 3. Verify the ISO (Optional but Highly Recommended)
To check the authenticity and safety of the downloaded ISO file, you can use **GPG**. The recommended way to use GPG in this guide is via **WSL (Windows Subsystem for Linux)**.

1. Install WSL by running **PowerShell as administrator** and executing:
   ```powershell
   wsl --install
   ```
   Restart your computer once the installation is complete.
2. The default distro in WSL is **Ubuntu**, so this guide assumes you are using Ubuntu.
3. Check if GPG is installed by running:
   ```bash
   sudo apt install gpg
   ```
   If it is not installed, install it using the above command.
4. Follow the instructions on the EndeavourOS website to verify the ISO file using the **sha512** and **gpg** commands.
5. If the verification returns **"OK"**, proceed with the next step.

#### 4. Create a Bootable USB with Rufus
1. Plug in your **USB stick** and open **Rufus**.
2. If Rufus does not automatically detect your USB, manually select it.
   > **⚠ WARNING:** Ensure you select the correct drive, as **ALL DATA WILL BE ERASED**.
3. Under "Image Option," select the **EndeavourOS ISO** file (the signature file is no longer needed after verification).
4. Choose the appropriate partition scheme:
   - If your computer supports **UEFI**, select:
     - **GPT** as the partition scheme.
     - **UEFI (non CSM)** as the target system.
   - If your computer is **very old** and does **not** support UEFI, select:
     - **MBR** as the partition scheme.
     - **BIOS or UEFI** as the target system.
5. Leave other options as default.
6. Click **START**. When prompted, even if Rufus recommends choosing "Write in ISO Image mode", **do not** select that option yet.
   - This guide **recommends selecting "Write in DD Image mode"** to avoid future issues.

   > **⚠ WARNING:** Choosing this option may cause for you to not access the USB stick completely after writing the ISO to it, so make sure to use a USB stick **purely for the purposes of this task.**

7. Confirm the warnings about data loss and wait for the process to complete.
8. Once done, you will see a green box labeled **"READY."**
9. You have now successfully created a bootable USB drive. You may now eject it if needed.

---

Work in progress!
