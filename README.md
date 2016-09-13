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
blacklist ssb
blacklist bcma
blacklist b43
blacklist brcmsmac
```

## Compile and install

```sh
$ make
$ make install
$ depmod -A
$ modprobe wl
```

## See also

* [Official README file][2]

[2]: https://www.broadcom.com/docs/linux_sta/README_6.30.223.271.txt
