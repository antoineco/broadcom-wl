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

Make sure to unload them with the `rmmod` command and add them the blacklist so that they are not automatically reloaded
during the next system startup:

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

The module should appear as *installed* in the list of modules managed by DKMS after the first system startup on the new
kernel:

```sh
$ dkms status
broadcom-wl, 6.30.223.271, 4.7.6-200.x86_64, x86_64: installed
```

[2]: http://linux.dell.com/dkms/manpage.html

## See also

* [Official README file][3]

[3]: https://www.broadcom.com/docs/linux_sta/README_6.30.223.271.txt
