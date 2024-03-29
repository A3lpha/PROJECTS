# Installing Kali Linux

Installing Kali Linux (single boot) on your computer is an easy process. This guide will cover the basic install (which can be done on bare metal or [guest VM](https://www.kali.org/docs/virtualization/)), with the option of encrypting the partition. At times, you may have sensitive data you would prefer to encrypt using Full Disk Encryption (FDE). During the setup process you can initiate an LVM encrypted install on either Hard Disk or USB drives.

First, you’ll need compatible computer hardware. Kali Linux is supported on amd64 (x86_64/64-bit) and i386 (x86/32-bit) platforms. Where possible, we would **recommend using the amd64 images**. The hardware requirements are minimal as listed in the section below, although better hardware will naturally provide better performance. You should be able to use Kali Linux on newer hardware with UEFI and older systems with BIOS.

Our i386 images, by default use a [PAE](https://en.wikipedia.org/wiki/Physical_Address_Extension) [kernel](https://pkg.kali.org/pkg/linux), so you can run them on systems with over 4 GB of RAM.

In our example, we will be installing Kali Linux in a fresh guest VM, without any existing operating systems pre-installed. We will explain other possible scenarios throughout the guide.

# **System Requirements**

The installation requirements for Kali Linux will vary depending on what you would like to install and your setup. For system requirements:

- On the low end, you can set up Kali Linux as a basic Secure Shell (SSH) server with no desktop, using **as little as 128 MB of RAM (512 MB recommended)** and **2 GB of disk space**.
- On the higher end, if you opt to install the default Xfce4 desktop and the `kali-linux-default` [metapackage](https://www.kali.org/docs/general-use/metapackages/), you should really aim for **at least 2 GB of RAM** and **20 GB of disk space**.
    - When using resource-intensive applications, such as Burp Suite, [they recommend](https://portswigger.net/support/burp-suite-software-faqs) at least **8 GB of RAM** *(and even more if it is a large web application!)* or using simultaneous programs at the same time.

# **Installation Prerequisites**

This guide will make also the following assumptions when installing Kali Linux:

- Using the amd64 installer image.
- CD/DVD drive / USB boot support.
- Single disk to install to.
- Connected to a network (with DHCP & DNS enabled) which has outbound Internet access.

We will be wiping any existing data on the hard disk, so please backup any important information on the device to an external media.

# **Preparing for the Installation**

1. [Download Kali Linux](https://www.kali.org/docs/introduction/download-official-kali-linux-images/) *(We [recommend](https://www.kali.org/docs/introduction/what-image-to-download/#which-image-to-choose) the image marked **Installer**).*
2. Burn The Kali Linux ISO to DVD or [image Kali Linux Live to USB drive](https://www.kali.org/docs/usb/live-usb-install-with-windows/). *(If you cannot, check out the [Kali Linux Network Install](https://www.kali.org/docs/installation/network-pxe/)).*
3. Backup any important information on the device to an external media.
4. Ensure that your computer is set to boot from CD/DVD/USB in your BIOS/UEFI.
5. In the UEFI settings, ensure that Secure Boot is disabled. The Kali Linux kernel is not signed and will not be recognized by Secure Boot.

# **Kali Linux Installation Procedure**

**[Boot](https://www.kali.org/docs/installation/hard-disk-install/#boot)**

1. To start your installation, boot with your chosen installation medium. You should be greeted with the Kali Linux Boot screen. Choose either **Graphical install** or **Install** (Text-Mode). In this example, we chose the Graphical install.

![https://www.kali.org/docs/installation/hard-disk-install/boot-installer.png](https://www.kali.org/docs/installation/hard-disk-install/boot-installer.png)

If you’re using the **live** image instead, you will see another mode, **Live**, which is also the default boot option.

![https://www.kali.org/docs/installation/hard-disk-install/boot-live.png](https://www.kali.org/docs/installation/hard-disk-install/boot-live.png)

**[Language](https://www.kali.org/docs/installation/hard-disk-install/#language)**

1. Select your preferred language. This will be used for both the setup process and once you are using Kali Linux.

![https://www.kali.org/docs/installation/hard-disk-install/setup-language-1.png](https://www.kali.org/docs/installation/hard-disk-install/setup-language-1.png)

---

1. Specify your geographic location.

![https://www.kali.org/docs/installation/hard-disk-install/setup-language-2.png](https://www.kali.org/docs/installation/hard-disk-install/setup-language-2.png)

---

1. Select your keyboard layout.

![https://www.kali.org/docs/installation/hard-disk-install/setup-language-3.png](https://www.kali.org/docs/installation/hard-disk-install/setup-language-3.png)

**[Network](https://www.kali.org/docs/installation/hard-disk-install/#network)**

1. The setup will now probe your network interfaces, looks for a DHCP service, and then prompt you to enter a hostname for your system. In the example below, we’ve entered **kali** as our hostname.

If there is no network access with DHCP service detected, you may need to manually configure the network information or do not configure the network at this time.

- If there isn’t a DHCP service running on the network, it will ask you to manually enter the network information after probing for network interfaces, or you can skip.
- If Kali Linux doesn’t detect your NIC, you either need to include the drivers for it when prompted, or generate a [custom Kali Linux ISO](https://www.kali.org/docs/development/live-build-a-custom-kali-iso/) with them pre-included.
- If the setup detects multiple NICs, it may prompt you which one to use for the install.
- If the chosen NIC is 802.11 based, you will be asked for your wireless network information before being prompted for a hostname.

![https://www.kali.org/docs/installation/hard-disk-install/setup-hostname-1.png](https://www.kali.org/docs/installation/hard-disk-install/setup-hostname-1.png)

---

1. You may optionally provide a default domain name for this system to use (values may be pulled in from DHCP or if there is an existing operating systems pre-existing).

![https://www.kali.org/docs/installation/hard-disk-install/setup-hostname-2.png](https://www.kali.org/docs/installation/hard-disk-install/setup-hostname-2.png)

**[User Accounts](https://www.kali.org/docs/installation/hard-disk-install/#user-accounts)**

1. Next, create the user account for the system (Full name, username and a strong password).

![https://www.kali.org/docs/installation/hard-disk-install/setup-user-1.png](https://www.kali.org/docs/installation/hard-disk-install/setup-user-1.png)

![https://www.kali.org/docs/installation/hard-disk-install/setup-user-2.png](https://www.kali.org/docs/installation/hard-disk-install/setup-user-2.png)

![https://www.kali.org/docs/installation/hard-disk-install/setup-user-3.png](https://www.kali.org/docs/installation/hard-disk-install/setup-user-3.png)

**[Clock](https://www.kali.org/docs/installation/hard-disk-install/#clock)**

1. Next, set your time zone.

![https://www.kali.org/docs/installation/hard-disk-install/setup-clock.png](https://www.kali.org/docs/installation/hard-disk-install/setup-clock.png)

**[Disk](https://www.kali.org/docs/installation/hard-disk-install/#disk)**

1. The installer will now probe your disks and offer you various choices, depending on the setup.

In our guide, we are using a clean disk, so we have four options to pick from. We will select **Guided - the entire disk**, as this is the single boot installation for Kali Linux, so we do not want any other operating systems installed, so we are happy to wipe the disk.

If there is an pre-existing data on the disk, you will have have an extra option *(Guided - use the largest continuous free space)* than the example below. This would instruct the setup not to alter any existing data, which is perfect for dual-booting into another operating system. As this is not the case in this example, it is not visible.

Experienced users can use the “Manual” partitioning method for more granular configuration options, which is covered more in our [BTRFS guide](https://www.kali.org/docs/installation/btrfs/).

If you want to encrypt Kali Linux, you can enable Full Disk Encryption (FDE), by selecting **Guided - used entire disk and setup encrypted LVM**. When selected, later on in the setup (not in this guide) prompt you to enter a password (twice). You will have to enter this password every time you start up Kali Linux.

![https://www.kali.org/docs/installation/hard-disk-install/setup-partition-1.png](https://www.kali.org/docs/installation/hard-disk-install/setup-partition-1.png)

---

1. Select the disk to be partitioned.

![https://www.kali.org/docs/installation/hard-disk-install/setup-partition-2.png](https://www.kali.org/docs/installation/hard-disk-install/setup-partition-2.png)

---

1. Depending on your needs, you can choose to keep all your files in a single partition - the default - or to have separate partitions for one or more of the top-level directories.

If you’re not sure which you want, you want “**All files in one partition**”.

![https://www.kali.org/docs/installation/hard-disk-install/setup-partition-3.png](https://www.kali.org/docs/installation/hard-disk-install/setup-partition-3.png)

![https://www.kali.org/docs/installation/hard-disk-install/setup-partition-4.png](https://www.kali.org/docs/installation/hard-disk-install/setup-partition-4.png)

---

1. Next, you’ll have one last chance to review your disk configuration before the installer makes irreversible changes. After you click *Continue*, the installer will go to work and you’ll have an almost finished installation.

![https://www.kali.org/docs/installation/hard-disk-install/setup-partition-5.png](https://www.kali.org/docs/installation/hard-disk-install/setup-partition-5.png)

**[Encrypted LVM](https://www.kali.org/docs/installation/hard-disk-install/#encrypted-lvm)**

If enabled in the previous step, Kali Linux will now start to perform a secure wipe of the hard disk, before asking you for a LVM password.

Please be sure a strong password is used, or else you will be prompted with a weak passphrase warning.

This wipe may take “a while” (hours) depending on the size and speed of the drive.

If you wish to risk it, you can skip it.

**[Proxy Information](https://www.kali.org/docs/installation/hard-disk-install/#proxy-information)**

1. Kali Linux uses a central repository to distribute applications. You’ll need to enter any appropriate proxy information as needed.

![https://www.kali.org/docs/installation/hard-disk-install/setup-proxy.png](https://www.kali.org/docs/installation/hard-disk-install/setup-proxy.png)

**[Metapackages](https://www.kali.org/docs/installation/hard-disk-install/#metapackages)**

If network access was not setup, you will want to **continue with setup** when prompt.

If you are using the **Live** image, you will not have the following stage.

1. Next you can select which [metapackages](https://www.kali.org/docs/general-use/metapackages/) you would like to install. The default selections will install a standard Kali Linux system and you don’t really have to change anything here.

Please [refer to this guide](https://www.kali.org/docs/introduction/what-image-to-download/#which-desktop-environment-and-software-collection-to-choose-during-installation) if you prefer to change the default selections.

![https://www.kali.org/docs/installation/hard-disk-install/setup-default-metapackages.png](https://www.kali.org/docs/installation/hard-disk-install/setup-default-metapackages.png)

**[Boot Information](https://www.kali.org/docs/installation/hard-disk-install/#boot-information)**

1. Next confirm to install the GRUB boot loader.

![https://www.kali.org/docs/installation/hard-disk-install/setup-grub-1.png](https://www.kali.org/docs/installation/hard-disk-install/setup-grub-1.png)

---

1. Select the hard drive to install the GRUB bootloader in (**it does not by default select any drive**).

![https://www.kali.org/docs/installation/hard-disk-install/setup-grub-2.png](https://www.kali.org/docs/installation/hard-disk-install/setup-grub-2.png)

**[Reboot](https://www.kali.org/docs/installation/hard-disk-install/#reboot)**

1. Finally, click Continue to reboot into your new Kali Linux installation.

![https://www.kali.org/docs/installation/hard-disk-install/setup-reboot.png](https://www.kali.org/docs/installation/hard-disk-install/setup-reboot.png)

# **Post Installation**

Now that you’ve completed installing Kali Linux, it’s time to customize your system
