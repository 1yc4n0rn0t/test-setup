# 🚀 Setup Guide for Debian VM on Windows Host

This guide will help you configure a Debian 12 virtual machine on a Windows host, including adjustments for screen resolution, installation of necessary software, and system configuration.

## 📋 Prerequisites
- Hyper-V enabled on Windows
- Debian 12 ISO
- Internet connection for the VM

## 🛠 Initial Setup

### 🔧 Configure Screen Resolution
Run this command if you struggle to see your screen while running the setup:

```bash
xrandr | awk '/ connected/ { print $1 }' | xargs -I{} xrandr --output {} --mode 1920x1080
```

### 🖥 Create New VM
1. Choose "New VM" (not quick create)
2. Select "Generation 2"
3. Go to Settings:
   - Disable Secure Boot
   - Enable guest services in the Integration Services.

### 📦 Install Debian 12
Install Debian 12 as you prefer. Remember to set up both root/sudo and user accounts. During the final step of the installation:
- Configure Gnome

## ⚙️ Configuration Steps

### 🌟 Step 1: Post-Installation Setup
After the first boot:
```bash
# Login with your user account (not root)
su root  # Switch to root on that profile
apt install git -y  # Install git
```

### 📡 Step 2: Clone and Run Setup Script
```bash
git clone https://github.com/pentestfunctions/test-setup.git
cd test-setup
chmod +x setup.sh
./setup.sh
```

### 🔄 Reboot the System
After running `setup.sh`, the system will reboot (It is important to turn the machine OFF and close t he Virtual Machine Connection).
- The reason for this is ensure the hyper-v modules can be recognized that we just installed.

### 🔌 Enable Enhanced Session Mode
Run the following command in an administrator PowerShell on the Windows host (MAKE SURE YOU CHANGE DebianTest to your Hyper-V image name):
```bash
Set-VM -VMName DebianTest -EnhancedSessionTransportType HvSocket
```

### 💻 Configure RDP and Final Setup
When you boot the VM, on the login screen you will be prompted for enhanced session mode (RDP) after a few seconds. You can adjust the resolution now if you wish.

Once logged into the Xorg session, run:
```bash
cd ~/test-setup
sudo chmod +x configure.sh
./configure.sh
```

Then simply setup your .bashrc with this one
```
https://github.com/pentestfunctions/test-setup/blob/main/.bashrc
```
