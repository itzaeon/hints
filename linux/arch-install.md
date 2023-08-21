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
Select `Use a best-effort default partition layout` unless you have a good reason not to. Select the drive you with to install to and the filesystem. `ext4` has always been extremely stable for me and I highly reccomend it.

