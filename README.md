# arch-pi
A simple script installing [Arch Linux](https://www.archlinux.org/) on an SD
card for the
[Raspberry Pi](https://www.raspberrypi.org/products/).

The script supports the following hardware models of the
Raspberry Pi:

* Raspberry Pi Model A/A+/B/B+, Compute Module, Zero, Zero W (ARMv6)
* Raspberry Pi 2 Model B (ARMv7)
* Raspberry Pi 3 Model B/B+ (ARMv8, *but using ARMv7*)

**NOTE:** For the time being, the Raspberry Pi 3 Model B will install the ARMv7
version of Arch Linux also used by the Raspberry Pi 2 Model B.

The installation procedure pretty much matches the Installation Guides from
[Arch Linux ARM](http://archlinuxarm.org/),
but also adds some configuration settings like networking, including a static IP
address for a fully headless setup without a screen or keyboard.

After the installation you can directly login to your
Raspberry Pi
using the pre-configured IP address.

## Requirements

In order to use
`arch-pi`,
you need an extra Linux environment which is
connected to the Internet and has an SD card slot.

Just make sure the following commands are
available:

* `lsblk`
* `dd`
* `parted`
* `curl`
* `tar`

## Usage Guide

In a Terminal download and unpack the latest version of
`arch-pi`:

```
curl -L https://github.com/knight94/arch-pi/archive/master.tar.gz | tar zxvf -
```

For post installation setup and configuration doenload the folloeing file
```
curl -L https://github.com/knight94/ArchMatic/archive/master.tar.gz | tar zxvf -
```

Insert the SD card on which you want to install Arch Linux, but make sure none
of its partitions is mounted, otherwise unmount them. Then use `lsblk` to
determine the device name of the SD card, e.g. `/dev/mmcblk0`, and open the
configuration file:

```
vi arch-pi-master/arch-pi.conf
```

Make sure the `INSTALL_DEVICE` setting matches the device name of your SD card.

You may also want to change the following settings:

* `HOSTNAME`
* `TIMEZONE`
* `CONSOLE_KEYMAP`
* `SET_ETHERNET` -- if set to `YES`, then also check the other `ETHERNET_*` settings
* `SET_WIRELESS` -- if set to `YES`, then also check the other `WIRELESS_*` settings

Once you are done, save and close the configuration file.

To write and format partitions on the SD card,
`arch-pi`
needs super-user privileges. So `su` to `root` or use `sudo` to start the
installation process:

```
sudo arch-pi-master/arch-pi.sh
```

**CAUTION:** The installation will delete *all* existing data on the SD card.

The installation is done, once you see

```
[arch-pi] Wake up, Neo... The installation is done!
```

Then insert the SD card into your
Raspberry Pi
and start it up.

That's it!

You can login as the default user `alarm` with the password `alarm`.
The default root password is `root`.

## License

This software is distributed under the terms of the
[GNU General Public License v3](https://www.gnu.org/licenses/gpl-3.0.en.html).
