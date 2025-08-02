# Win-to-Arch: A Simple Guide for Migrating from Windows to Arch Linux

| 📝 **Quote** |
|--------------|
| "No matter how great the crises arising from freedom, they are never more dangerous than the false security of too much repression." |

## Introduction

**Win-to-Arch** is a simple step-by-step guide, completely written by myself to help anyone who would like to switch from their Windows 10/11 system to an Arch Linux-based system while keeping the process as simple as possible without adding any unnecessary bloat to the operating system.

I believe the best way to do this is to share experience; therefore, this guide will be mostly based on my personal experience on this journey, tailored to fit anyone who is on the same path.

> **⚠ WARNING:** Win-to-Arch targets users who have a certain amount of knowledge about GNU/Linux and are comfortable with using the terminal. Even though this document aims to make Arch as user-friendly and graphical as possible, please ensure you do enough research about GNU/Linux and the terminal before attempting the migration, as you will need to use the terminal to resolve issues or even install packages/applications.
>
> It is recommended to completely read this guide before attempting any of the steps to prevent future complications. 
>
> Everything that is aimed to be used in this guide is **completely free and open-source software**.

---

## Preparing Arch Installation

Arch Linux by itself does not have any graphical installation screen, which may be difficult for those who would like to use the simplicity and lightweight nature of Arch without the hassle or risk of messing up the installation.

Therefore, the best option for this case would be using **EndeavourOS**. EndeavourOS is an Arch-based operating system that follows the same principles as Arch and is the most popular Arch-based distro according to Distrowatch.

To install Arch (EndeavourOS), you will need to create a bootable drive. The recommended method is to use a USB stick (minimum **2 GB recommended**) and turn it into a bootable drive, which will be used to install EndeavourOS.

On Windows 10/11, there are multiple tools that can execute this task, such as **Ventoy** and **Rufus**. The recommended program for this guide is **Rufus**, as it is the one I have used, but feel free to use any other tool if you know how to.

### Steps to Create a Bootable USB Drive

#### 1. Download Rufus
- Visit the [official Rufus website](https://rufus.ie/) and download the version suitable for your system.
- Feel free to choose between the standart or portable versions.

#### 2. Download EndeavourOS ISO
- Visit the [official EndeavourOS website](https://endeavouros.com/) and download the latest ISO version that is suitable for your system from the listed mirrors.
- Consider downloading the **signature file** for the 3. step.
- To make the overall process faster, choose a mirror closest to your geographical location.

#### 3. Verify the ISO (Optional but Highly Recommended)
To check the authenticity and safety of the downloaded ISO file, you can use **GPG**. The recommended way to use GPG in this guide is via **WSL (Windows Subsystem for Linux)**.

1. Install WSL by running **PowerShell as administrator** and run:
(The default distro in WSL is **Ubuntu**, however because this guide aims to only use free and open source software, Debian will be used instead.)

   ```powershell
   wsl --install -d Debian
   ```
3. Restart your computer once the installation is complete.

4. Check if GPG is installed by running:
   ```bash
   sudo apt install gnupg
   ```
   If it is not installed, install it using the above command.
5. Follow the instructions on the EndeavourOS website to verify the ISO file using the **sha512** and **gpg** commands.
6. If the verification returns **"OK"**, proceed with the next step.

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

## Installing Arch via EndeavourOS

- In order to install EndeavourOS to your system, insert the bootable USB drive to the device that you'd like to use Arch on while it is **not running**.

Proceed with booting up your system and constantly pressing the correct key to launch into your BIOS/UEFI interface. If you don't know what the correct key is, you can search for it in your computer's / motherboard's manifacturer's website, or you can try a few common keys like DEL, F2, F10, and ESC to see which one will work.

> **⚠ WARNING:** If you are installing GNU/Linux on a Windows system that is infected with malware, make sure you know the correct key. If you accidently boot into your infected operating system with the USB drive inserted, it may also get infected depending on the type and behavior of the malware. This guide recommends for you to ensure that your infected system can not access the network in any way and to test the correct key **before booting the system with the USB inserted**, to safely check if you can successfully boot into your BIOS/UEFI without taking any major risks.
>
> This method is generally safe for devices that only have the operating system infected and not the boot loader / BIOS/UEFI. Proceed with caution.
>
> You may ignore this warning if your system is not infected.

Once you safely boot up to your BIOS/UEFI with your bootable USB drive inserted, you can proceed by selecting the USB drive from the boot menu. If you have trouble locating it, you may need to check the sources of the manifacturer of your computer / motherboard.


EndeavourOS comes with the Calamares system installer, which is an installer with a graphical user interface.

EndeavourOS only ships with the following packages, which provide security and contribute to having a complete Arch system: Firefox, Pacman, Yay, FirewallD, Pipewire, Nvidia installer, Dracut, Power-Profiles-Daemon.

During the installation most of the options will be clearly understandable in your preferred language. 


- In the desktop environment choosing part, this guide recommends KDE Plasma, as it is a complete desktop environment with all the basic features as Windows and an app ecosystem with a similar look and feel. It is also highly customisable. However feel free to choose any other desktop environment or window manager.

> **⚠ WARNING:** During the **"Partition"** section of the installation, you will be asked to edit your drive's partitions and choose one to install the operating system on.
>
> If you prefer to dual-boot Windows with Arch, you can create a new partition while keeping your Windows partition. The minimum requirement mentioned in the official EndeavourOS website is 15 GB.
>
> However, if you prefer to completely wipe your drive (recommended for users who do not want to keep Windows on their system), you may delete all of the listed partitions, and install EndeavourOS on one of them.
>
> Please make sure to **backup any data from your system that you would like to keep** before proceeding.

You will also be presented with the choice to encrypt your disk. 

Disk encryption is an option which you can choose to completely encrypt your drive, which will lead you to enter passwords more than usual. If you want to protect your data from being accessed when your drive is stolen, you should enable this option. Especially recommended for laptop users.


When you're done with the disk partitioning, you may move on with the next steps and finish the installation.


## Booting into Arch
 
When your installation process is finished, you will be prompted to restart your system. Once you restart you should be greeted with your new Arch installation. If not, you may need to boot into your BIOS/UEFI and change the boot order priority, or check the boot menu settings.

> **NOTE:** EndeavourOS is esentially just Arch Linux with a graphical installation screen to make process simpler and a few packages pre-installed (that have been mentioned before), which you may choose to not install most of them during the installation screen. After the installation your system will be running Arch Linux. 

This guide mentions that the software that is used in this guide will be completely free and open-source.

For Nvidia users: If you would also like all of the software in your system to be free and open-source, you would want to use the open source Nouveau drivers instead of the closed-source proprietary Nvidia drivers. To achieve this, you can run `sudo nvidia-inst -n` in your preferred terminal and proceed. 

If you are not using an Nvidia graphics card and want to keep your system fully free and open-source, you may search for any packages that might be included in your system that are related to the proprietary Nvidia drivers as the latest EndeavourOS ISO releases ship with them, and remove them.

---

**Thank you for following this guide in your journey, and congratulations on your new Arch system!**
