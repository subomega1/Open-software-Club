# LINUX_WORKSHOP
## Acknowledgements

This workshop draws inspiration from the Linux community, official distribution documentation
(Ubuntu, Debian, Arch, Fedora, Kali), and open-source advocates who promote accessible computing.

### Table of Contents

- [1. Why Linux Matters](#1-why-linux-matters)
- [2. Open Source Philosophy](#2-open-source-philosophy)
- [3. Where Linux Is Used](#3-where-linux-is-used)
- [4. Understanding Linux Distros](#4-understanding-linux-distros)
- [5. Choosing the Right Distro](#5-choosing-the-right-distro)
- [6. Installing Linux](#6-installing-linux)
  - [6.1 Live USB](#61-live-usb)
  - [6.2 Virtual Machine](#62-virtual-machine)
  - [6.3 Dual Boot](#63-dual-boot)
- [7. Troubleshooting Installation](#7-troubleshooting-installation)
- [8. First Steps After Install](#8-first-steps-after-install)

### 1. Why Linux Matters
Linux underpins modern computing. It powers the majority of servers on the internet, all Android
devices, most cloud platforms, networking gear, supercomputers, and is central in DevOps, data
engineering, cybersecurity, and embedded/IoT systems.

Key strengths:
- Stability and security-first design
- Performance and resource efficiency
- Flexibility from desktops to clusters to embedded boards
- Open ecosystem with rapid innovation

***Quiz***
Which of the following is NOT a typical Linux strength?
- [] Stability and security
- [] Performance and efficiency
- [x] Proprietary-only licensing
- [] Flexibility across devices

***Quiz (advanced)***
Which command prints kernel release information?
- [] cat /etc/issue
- [x] uname -r
- [] lscpu
- [] cat /proc/cpuinfo

Which file commonly contains distro identification fields like ID and VERSION_ID?
- [] /etc/fstab
- [] /etc/hosts
- [x] /etc/os-release
- [] /etc/resolv.conf

### 2. Open Source Philosophy
Open source is about freedom to use, study, modify, and share software. Licenses like GPL, MIT,
and Apache ensure these freedoms, enabling collaborative development and transparent security.

Impacts:
- Faster innovation cycles through community collaboration
- Lower total cost of ownership
- Auditability and reproducibility for research and security
- Vendor independence and portability


***Quiz***

Which statement best captures open-source licensing?
- [] Source code may be viewed but not modified or redistributed
- [x] Users can use, study, modify, and redistribute the code
- [] Code is free of cost and closed to changes
- [] License forbids commercial use in all cases


Which license is known for copyleft provisions requiring derivative works to remain open-source?
- [x] GPL
- [] MIT
- [] BSD-2-Clause
- [] Apache-2.0

Which command on Debian/Ubuntu can show a package’s license metadata?
- [] systemctl status
- [] lsmod
- [x] apt show <pkg>
- [] ifconfig

### 3. Where Linux Is Used
Linux is ubiquitous:

- Servers and cloud: web servers, databases, container hosts
- DevOps and CI/CD: Docker, Kubernetes, runners, IaC
- Cybersecurity: offensive tooling (Kali), defensive monitoring, forensics
- Data/AI: Python, GPU compute, distributed systems (Spark, Ray)
- Networking: routers, firewalls, SDN controllers
- Embedded/IoT: Raspberry Pi, automotive, industrial controllers
- Desktops and workstations: development, creators, power users

***Quiz***
Linux dominates which segment the most today?
- [] Consumer gaming consoles
- [x] Servers and cloud infrastructure
- [] Feature phones
- [] Mainframe-exclusive OS market

Which command most directly checks whether a systemd-managed web server is running?
- [] ps -ef | grep http
- [x] systemctl status nginx
- [] top
- [] journalctl -b

Which command requests only HTTP headers from a local web server?
- [] ping 127.0.0.1
- [] wget http://127.0.0.1
- [x] curl -I http://127.0.0.1
- [] traceroute 127.0.0.1

### 4. Understanding Linux Distros
A Linux distribution (distro) packages the Linux kernel with userspace tools, package management,
and defaults.

Common families and examples:
- Debian-based: Debian, Ubuntu, Linux Mint (APT/DEB)
- Red Hat-based: Fedora, RHEL, CentOS, Rocky, Alma (DNF/RPM)
- Arch-based: Arch, Manjaro (pacman)
- Specialized: Kali (security), Parrot, Tails (privacy)

Differences you’ll notice:
- Package manager and repositories
- Release model (LTS vs. rolling)
- Defaults and tooling (system installers, desktops)
- Community vs. enterprise focus

***Quiz***
Which pair correctly matches a distro family and package manager?
- [] Fedora – apt
- [x] Arch – pacman
- [] Debian – dnf
- [] Ubuntu – rpm


Which is a rolling-release distribution?
- [] Ubuntu LTS
- [] Debian stable
- [x] Arch Linux
- [] Rocky Linux

Which command prints the package manager version on Fedora?
- [] apt --version
- [x] dnf --version
- [] pacman -V
- [] zypper --version

### 5. Choosing the Right Distro
Guidelines:

- Beginners and general desktop: Ubuntu LTS, Linux Mint
- Developers: Ubuntu/Fedora for fresh toolchains; Arch/Manjaro if you want rolling
- Security training: Kali (use in VM), Parrot
- Servers: Ubuntu LTS, Debian stable, Rocky/Alma for RHEL compatibility
- Lightweight/old hardware: Lubuntu, Xubuntu, Debian with XFCE

Decision points:
- Stability vs. latest features
- Hardware support and drivers
- Community and documentation
- Ecosystem tooling you need

***Quiz***

For a long-lived production server you most likely choose:
- [] Arch rolling release
- [x] Ubuntu LTS or Debian stable
- [] Kali
- [] Fedora Rawhide


Which choice prioritizes stability over newest features for servers?
- [x] Debian stable
- [] Fedora Rawhide
- [] Arch
- [] Kali

Which command lists PCI devices, often used to check GPUs and drivers?
- [] lsmod
- [x] lspci -k
- [] ip a
- [] df -h

### 6. Installing Linux
There are three common paths. Start with Live USB or a Virtual Machine; use Dual Boot only if you
need full bare-metal performance.

#### 6.1 Live USB
Steps:
1) Download ISO from the official distro site (verify checksum if possible).
2) Create bootable USB:
   - use Balena Etcher or Rufus (on Windows)
3) Reboot, select the USB in BIOS/UEFI boot menu.
4) Choose “Try” (live session) or “Install”.

**Assignment**
Verify ISO integrity and write the USB safely (use Rufus or Etcher):

***Quiz***
What’s the safest beginner tool to create a bootable USB on Windows?
- [] dd
- [] cat
- [x] Rufus (or Etcher)
- [] tar

#### 6.2 Virtual Machine
Tools: VirtualBox, VMware Workstation Player, or GNOME Boxes.

Steps (VirtualBox):
1) Create a new VM, set Type: Linux, Version: match your distro.
2) Allocate 2–4 vCPUs, 4–8 GB RAM, 25+ GB disk.
3) Mount the ISO as the optical drive.
4) Boot VM and follow the installer.
5) After install, add “Guest Additions” for better display and clipboard.

**Assignment**

Set up and start a VM.

***Quiz***

Guest Additions/VM Tools primarily provide:
- [] Kernel upgrades
- [x] Better graphics, shared clipboard, and integration
- [] Package updates
- [] Dual-boot capability

#### 6.3 Dual Boot

Pre-checks:

- Backup your data
- Disable encryption (BitLocker)
- Ensure UEFI/Secure Boot understanding; have recovery media
- Free unallocated space (20–50 GB+)

Steps:

1) In Windows: shrink partition to create free space (Disk Management).
2) Create Live USB and boot into it.
3) Choose “Install alongside Windows” if offered; otherwise select “Something else” and create:
   - EFI System Partition (if missing)
   - Root `/` (ext4)
   - Optional: `/home` and `swap`
4) Install bootloader to the EFI (usually default).
5) Reboot and select Linux in the boot menu.

**Assignment**

Follow the steps and create a successful dual-boot system.

***Quiz***

What’s the most important precaution before dual booting?
- [] Disable UEFI
- [x] Backup your data
- [] Remove Windows first
- [] Use MBR instead of GPT always

### 7. Troubleshooting Installation
Common issues and fixes:
- No bootable device: re-create USB, check UEFI/Legacy settings, secure boot toggles
- Black screen/NVIDIA: use “Safe Graphics” or add `nomodeset`; install proprietary drivers
post-install
- Wi-Fi missing: use Ethernet/USB tethering, install firmware packages
- Partition errors: ensure free space and correct GPT/MBR scheme; repair with `boot-repair` for
GRUB issues
- Slow VM: enable virtualization in BIOS, increase RAM/CPU, enable 3D acceleration

**Assignment**

Check that the OS you downloaded is working; if not, troubleshoot and try to fix it.

***Quiz***

If GRUB doesn’t appear after install on UEFI systems, a helpful tool is:
- [] fsck
- [] parted
- [x] boot-repair
- [] rsync

### 8. First Steps After Install
Recommended initial setup:
- Update system: `sudo apt update && sudo apt upgrade -y` (Debian/Ubuntu) or the equivalent for your distro
- Install drivers/firmware as needed (NVIDIA/select firmware packages)
- Create a non-root user if not already created
- Install common tools: `git`, `curl`, `build-essential`, editor/IDE, browser
- Enable firewall: `ufw enable` (on Ubuntu) and allow necessary services
- Flatpak as needed for apps
- Create a Projects directory and set up SSH keys for Git hosting


**Assignment**

Update your system and install some packages add user (make it sudo user)

Execute and record concrete setup steps (Debian/Ubuntu shown):

```bash
sudo apt update && sudo apt install -y build-essential git curl vim ufw openssh-client
# Drivers (Ubuntu):
sudo ubuntu-drivers autoinstall 2>/dev/null || true
# User management (if creating another user):
sudo adduser devuser
sudo usermod -aG sudo devuser
```

***Quiz***

On Ubuntu, enabling a simple host firewall is done via:
- [] systemctl enable firewall
- [] iptables --enable
- [x] ufw enable
- [] firewalld start
