# Ubuntu Setup Documentation

## Update and Upgrade System
```bash
sudo apt update && sudo apt upgrade -y
sudo apt autoremove --purge -y
```

## Install Essential Tools
```bash
sudo apt install gnome-tweaks
sudo apt install gnome-shell-extensions
sudo apt install flatpak
sudo flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
sudo apt install curl git wget unzip build-essential -y

# Override Flatpak file system permissions for GTK configurations
sudo flatpak override --filesystem=xdg-config/gtk-3.0 && sudo flatpak override --filesystem=xdg-config/gtk-4.0
```

---

## Customize Ubuntu

### WhiteSur Theme Setup

#### 1. Theme
Clone the WhiteSur GTK theme repository and install the theme:
```bash
git clone https://github.com/vinceliuice/WhiteSur-gtk-theme.git --depth=1
cd WhiteSur-gtk-theme
./install.sh -n MyTheme -a alt -t blue -c dark -m -l -N mojave
```

#### 2. Cursor
Clone the WhiteSur cursor repository and install the cursors:
```bash
git clone https://github.com/vinceliuice/WhiteSur-cursors.git --depth=1
cd WhiteSur-cursors
./install.sh
```

#### 3. GRUB Theme
Clone the WhiteSur GRUB theme repository and install the GRUB theme:
```bash
git clone https://github.com/vinceliuice/grub2-themes.git --depth=1
cd grub2-themes
./install.sh
```

---

### Optional Customization

#### Customize Firefox
Apply tweaks to Firefox:
```bash
./tweaks.sh -f monterey 5+3 alt -e flat -f
```

---

## Add Swap RAM
To increase swap space to 8GB, follow these steps:

### 1. Remove Old Swap (Optional, if you need to recreate it)
Disable the currently active swap:
```bash
sudo swapoff -a
```

Remove the old swap file (if it exists and you want to replace it):
```bash
sudo rm /swapfile
```

### 2. Create a New Swap File
Create a new 8GB swap file:
```bash
sudo fallocate -l 8G /swapfile
```

If `fallocate` is not available, use this command instead:
```bash
sudo dd if=/dev/zero of=/swapfile bs=1G count=8
```

### 3. Set Permissions for the Swap File
Set the file permissions to restrict access to root:
```bash
sudo chmod 600 /swapfile
```

### 4. Format the File as Swap
Format the file to be used as swap:
```bash
sudo mkswap /swapfile
```

### 5. Activate the New Swap
Enable the swap:
```bash
sudo swapon /swapfile
```

### 6. Verify the Swap
Ensure the swap is active:
```bash
free -h
```

### 7. Make the Swap Permanent
Edit the `/etc/fstab` file to make the swap persist after reboot:
```bash
sudo nano /etc/fstab
```

Add the following line at the end of the file:
```
/swapfile none swap sw 0 0
```

Save and exit by pressing `CTRL+O`, `ENTER`, and `CTRL+X`.
