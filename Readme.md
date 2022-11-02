# Tp-link USB AC1300 -  Wifi drivers Ubunti 22.10
https://www.tp-link.com/nl/support/download/archer-t3u/
Cloned from https://github.com/cilynx/rtl88x2bu   credits to him

I edited some files git and compiled it at Ubuntu 22.10     Use: install_t3uv3.sh to install it

## Using and Installing the Driver
### Simple Usage

In order to make direct use of the driver it should suffice to build the driver
with `make` and to load it with `insmod 88x2bu.ko`. This will allow you to use the driver directly without changing your system persistently.
It might happen that your system freezes instantaneously. Ensure to not loose important work by saving and such beforehand.

### DKMS installation
If you want to have the driver available at startup, it will be convenient to
register it in DKMS. An executable explanation of how to do so can be found in
the script `deploy.sh`. Since registering a kernel module in DKMS is a major
intervention, only execute it if you understand what the script does.

### Known Problems
Some users reported problems due to `Unknown symbol in module`. This can be
caused by old deployments of the driver still being present in the systems directories. One solution reported was to forcefully remove all old driver
modules:

    sudo dkms remove rtl88x2bu/5.8.7.4 --all
    find /lib/modules -name cfg80211.ko -ls
    sudo rm -f /lib/modules/*/updates/net/wireless/cfg80211.ko
