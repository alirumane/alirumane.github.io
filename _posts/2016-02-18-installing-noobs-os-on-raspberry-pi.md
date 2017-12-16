---
layout: post
title: Installing NOOBS OS on Raspberry Pi
tags: [Raspberry Pi, NOOBS]
category: Raspberry Pi Tutorials
thumbnail:  images/post/installing-noobs-os-on-raspberry-pi.png
description: You bought a Raspberry Pi and want to run an OS on it
---

>You bought a Raspberry Pi and want to run an OS on it

* Do not remove this line (it will not be displayed)
{:toc}

**N**ew **O**ut **O**f the **B**ox **S**oftware - an easy Operating System installer

[Raspberrypi.org](https://www.raspberrypi.org/) suggests NOOBS OS installation. It has a complete guide for installing the OS, still cut through...

## A. Get NOOBS

There are two common methods to get NOOBS

- Buy a pre-installed SD card

  SD cards with NOOBS preinstalled are available, a list can be found on Raspberrypi website.
  
  If you bought pre-installed SD card, directly follow Booting step in Installation.
  
- Download NOOBS from Raspberrypi website

  NOOBS is available for download on Raspberrypi website.

## B. Setting up


**Essentials:**

* Raspberry Pi
* SD Card (16GB class 10 Preferred / 8GB Class 4 may also work)
* HDMI to VGA/HDMI cable (connecting to Display e.g. Monitor or T.V.)
* Keyboard and Mouse
* Power Supply (Micro USB e.g. phone charger)

## C. Installation

**Instructions:**

**Download**

* You will need a computer with an SD card reader. If you don't have one, you can buy a USB SD Card reader.

* Download NOOBS installer from [https://www.raspberrypi.org/downloads/noobs/](https://www.raspberrypi.org/downloads/noobs/).

* You will have two options NOOBS and NOOBS Lite

  NOOBS - Offline and network install
  
  NOOBS Lite - Network install only

It is preferred to download NOOBS over NOOBS Lite.

**Format SD Card**

![SD Formatter selection]({{site.url}}/images/SD_Formatter_4_instr.png "SD Formatter selection"){: .center-image }*SD Formatter selection*

* Format SD card using [SD Card Formatter](https://www.sdcard.org/downloads/formatter_4/).

* Insert SD card into the SD card reader connected to your computer.

* Check the drive letter allocated to it, e.g. G:/

* Set "FORMAT SIZE ADJUSTMENT" option to "ON" in the "Options" menu to ensure that the entire SD card volume is formatted.

* Click on Format button to format your SD card.

**NOOBS files on SD Card**

* Extract the downloaded NOOBS zip file in SD card and make sure the extracted file is not present in the folder.

* The files will be transferred to your SD card.

* Safely eject the SD card and insert it into Raspberry Pi.

**Booting the first time**

 ![Raspbian installation selection]({{site.url}}/images/noobs_raspbian_recom.png "Raspbian installation selection"){: .center-image }*Raspbian installation selection*

* Insert the SD card in Raspberry Pi, connect the Mouse, Keyboard and HDMI cable.

*  Connect USB cabled Power supply across it.

* Raspberry Pi will boot, and a window will appear with a list of different operating systems that you can install.

* Install Raspbian as Default OS.

* Once the install process has completed, it may ask for date and time. Set them as per your region.

**Logging in**

* The default login for Raspbian is username **pi** and password **raspberry**.

* Though won't ask by default, you can change it later.

## D. Update

You can update Raspberry Pi by typing the following commands on terminal.

It assures you run the latest builds and fixes for smooth operation.

Type

```bash
sudo apt-get update
```

and

```bash
sudo apt-get upgrade
```

to run the latest build.

You have successfully installed NOOBS in your Raspberry Pi!
