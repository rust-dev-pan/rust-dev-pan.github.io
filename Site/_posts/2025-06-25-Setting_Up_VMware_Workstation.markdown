---
layout: post
title: "🛠️ Setting Up VMware Workstation on Ubuntu 22.04"
date: 2025-06-25
categories: Hacking
permalink: /blog/Setting_Up_VMware_Workstation/
---

# 🛠️ Setting Up VMware Workstation on Ubuntu 22.04

> _“If I had 30 minutes to cut down a tree, I’d spend the first 20 sharpening my axe.”_ — Abraham Lincoln

This quote perfectly captures the mindset needed in the field of information security. The more you practice, the less time it takes to solve a challenge or crack a machine. Preparation is everything.

To ethically practice hacking and security skills, it’s crucial to set up your own local lab environment. Virtualization software enables us to run multiple isolated systems safely on a single host machine. Among the most popular options are **VirtualBox** and **VMware**.

As a developer using a Debian-based **Ubuntu** machine, I’ll walk you through how I set up **VMware Workstation** to create a secure and legal hacking lab on **Ubuntu 22.04**. (This method should also work for other Ubuntu versions with minor adjustments.)

---

## 🔧 Step 1: Update Your System

Before starting, ensure your system is up-to-date:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 📥 Step 2: Download the VMware Workstation Installer

We’ll be using **VMware Workstation 17.5.0** in this guide:

```bash
cd ~/Downloads
wget https://ia801608.us.archive.org/12/items/vmware-workstation-full-17.5.0-22583795.x-86-64-by-vmware.bundle/VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle
chmod +x VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle
sudo ./VMware-Workstation-Full-17.5.0-22583795.x86_64.bundle
```

- The installer is downloaded into the `Downloads` directory.
- We make the `.bundle` file executable.
- Then run it with `sudo` to begin installation.

After installation, **VMware Player** and other components should be available.

---

## ⚠️ Step 3: Fixing Kernel Module Errors

When running `vmplayer` for the first time, you may encounter errors related to missing kernel modules like `vmmon` or `vmnet`. These are required for VMware to work properly with the Linux kernel.

---

## 🛠️ Step 4: Install Required Tools & Patch Modules

Install the necessary packages and build the missing modules using the community-maintained `vmware-host-modules` repository:

```bash
sudo apt install build-essential linux-headers-$(uname -r)
sudo vmware-modconfig --console --install-all

git clone https://github.com/mkubecek/vmware-host-modules.git
cd vmware-host-modules
git checkout workstation-17.5.0
make
sudo make install
sudo systemctl restart vmware
```

- This installs build tools and kernel headers.
- Rebuilds the required modules for VMware Workstation 17.5.0.
- Finally, restarts the VMware service.

---

## ✅ You're Ready!

With this setup, you're now ready to start building and experimenting with your own ethical hacking lab—right from your Ubuntu machine!

Feel free to fork or update this guide for newer versions or other distributions.

---

**Happy hacking!** 🐧💻🕵️‍♂️
