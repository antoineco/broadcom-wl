# Broadcom Linux hybrid wireless driver (64-bit)

Re-upload from the source code found on the [Broadcom 802.11 support page][1]

**Patched for Linux >= 4.7**

Tested on a BCM4360-based 802.11ac Wireless Network Adapter (TP-LINK Archer T8E)

[1]: https://www.broadcom.com/support/802.11

## Prerequisites

The following kernel modules are incompatible with this driver and should not be loaded:
* ssb
* bcma
* b43
* brcmsmac

Make sure to unload (`rmmod` command) and blacklist those modules in order to prevent them from being automatically
reloaded during the next system startup:

`/etc/modprobe.d/blacklist.conf`
```
# wireless drivers (conflict with Broadcom hybrid wireless driver 'wl')
blacklist ssb
blacklist bcma
blacklist b43
blacklist brcmsmac
```

## Compile and install

### Manually

Build and install for the running kernel:

```sh
$ make
$ make install
$ depmod -A
$ modprobe wl
```

### Automatically

Using [DKMS][2] and the included `dkms.conf` file, one can let the operating system rebuild and install the module
automatically on every new kernel installation:

```sh
$ dkms add /path/to/this/repo
$ dkms status
broadcom-wl, 6.30.223.271: added
```

Providing that the `dkms` service is enabled, the module should appear as *installed* in the list of modules managed by
DKMS after the system boots for the first time on the new kernel:

```sh
$ dkms status
broadcom-wl, 6.30.223.271, 4.7.6-200.x86_64, x86_64: installed
```

[2]: http://linux.dell.com/dkms/manpage.html

## See also

* [Official README file][3]
* Arch Linux packages: [broadcom-wl][4] / [broadcom-wl-dkms][5]
* Debian packages: [broadcom-sta][6] ([source repository][7])
* [kmod-wl][8] package for RPM Fusion ([source repository][9])

[3]: https://www.broadcom.com/docs/linux_sta/README_6.30.223.271.txt
[4]: https://aur.archlinux.org/packages/broadcom-wl/
[5]: https://aur.archlinux.org/packages/broadcom-wl-dkms/
[6]: https://packages.debian.org/source/sid/broadcom-sta
[7]: https://gitlab.com/setecastronomy/broadcom-sta/tree/debian
[8]: http://download1.rpmfusion.org/nonfree/fedora/development/rawhide/Everything/x86_64/os/repoview/kmod-wl.html
[9]: https://github.com/rpmfusion/wl-kmod
