# Installing Arch Linux on Thinkpad X270

Using [`ventoy`](https://www.ventoy.net/), download the latest Arch Linux ISO from https://archlinux.org/download/.

## Connecting to the internet
```bash
$ iwctl
[iwd]# device list
#                            Devices
# -------------------------------------------------------------
#   Name          Address          Powered    Adapter    Mode
# -------------------------------------------------------------
#   wlan0         ...              on         ...        ...
[iwd]# station DEVICE-NAME scan
[iwd]# station DEVICE-NAME get-networks # if necessary
[iwd]# station DEVICE-NAME connect SSID
[iwd]# exit
```
Run `ping google.com` to test your connection.

## Using `archinstall`

`archinstall` is a command built into the install medium that guides the user through the installation process.
```bash
$ archinstall
```
You should see something like this, assuming you correctly completed the previous step:
```bash
Set/Modify the below options
> Archinstall langauge      English (100%)
  Mirrors                   
  Locales                   Defined
  Disk configuration        
  Bootloader                Systemd-boot
  ...                       ...
```

### Language
I have an English keyboard, so I always set English. (**TODO:** look into a French keyboard for accents?)

### Mirrors
Select `Mirror region` and then the option closest to your location. Use `/` to search and `ENTER` to select.

### Disk configuration
Select `Use a best-effort default partition layout` unless you have a good reason not to. Select the drive you with to install to and the filesystem. `ext4` has always been extremely stable for me and I highly recommend it. When prompted to create a separate partition for `/home`, select yes. This may allow you to recover much of your data if your install becomes damaged in some way.

### Bootloader
`grub` is a field-tested bootloader that is used as the default on many distributions of Linux. It is most suitable for dual-boot systems or where the extra GUI is wanted. I haven't tested `systemd-boot`, `efistub`, or `limine` yet.

### Swap
I highly recommend reading ["In defence of swap"](https://chrisdown.name/2018/01/02/in-defence-of-swap.html) by Chris Down. Enabling swap has never caused me any problems, but many have reported the same with disabling it.

### Profile
I am still using `bspwm`, so I generally select the `xorg` profile and install on top of that. If you're less comfortable, try using `desktop` and selecting a window manager there. Graphics drivers are your preference; however, I generally select open-source unless I am using an nvidia GPU.

### Audio server
`pulseaudio` is tried and true and is generally what I use. However, `pipewire` is extremely light and is presented as a good alternative to `pulseaudio`. Do some research and see which are used for your usecase.

### Kernel
I use `linux-zen` and it has never given me problems. It probably decreases my battery life by a slight amount versus `linux`, but I don't care enough to measure the difference.

### Additional packages
The essentials for me are as follows.
~~```librewolf-bin bspwm sxhkd neovim-git vscodium-bin networkmanager light-git paru```~~
```bspwm sxhkd networkmanager git```
Other packages will be installed later.

### Network configuration
Already set up. I generally choose to use NetworkManager because of the authentication that OES uses.

When finished, select `install` and wait. When `archinstall` is finished, you will see a prompt. Type `exit` and then `reboot`.

## Post-installation
**Note:** You may have to reconnect to the internet before running the following commands. 
```bash
## update packages
sudo pacman -Syu --noconfirm

## installing paru, a `yay` alternative
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
cd ~
sudo sed -i 's/#Color/Color/g' /etc/pacman.conf # enable colors
sudo sed -i 's/#VerbosePkgLists/VerbosePkgLists/g' /etc/pacman.conf # format name/version/size of packages
sudo sed -i 's/#ParallelDownloads = 5/ParallelDownloads = 5/g' /etc/pacman.conf # download 5 packages at once
paru -S --noconfirm bat # PKGBUILD syntax highlighting

## installing helpful utilities/programs
paru -S --noconfirm man-db acpi xorg-xsetroot
curl -L -o ~/.bashrc https://raw.githubusercontent.com/itzaeon/hints/main/linux/bashrc

## installing wm, browser, and terminal
paru -S --noconfirm librewolf-bin bspwm sxhkd neovim alacritty rofi
echo -e '#!/bin/sh\nexec bspwm' >> ~/.xinitrc
mkdir ~/.config
mkdir ~/.config/bspwm
mkdir ~/.config/sxhkd
curl -L -o ~/.config/bspwm/bspwmrc https://raw.githubusercontent.com/itzaeon/hints/main/linux/bspwmrc
curl -L -o ~/.config/sxhkd/sxhkdrc https://raw.githubusercontent.com/itzaeon/hints/main/linux/sxhkdrc
mkdir ~/scripts
curl -L -o ~/scripts/sxhkd-help https://raw.githubusercontent.com/itzaeon/hints/main/linux/scripts/sxhkd-help
chmod +x ~/scripts/sxhkd-help
```
