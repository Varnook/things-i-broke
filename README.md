# Index
1. [Arch](#arch)
    - [Failed to mount boot](#failed-to-mount-boot)

## Arch
### Failed to mount boot
When booting the following error showed up in the kernel initialization screen:
```
[Failed] Failed to mount /boot
See 'systemctl status boot.mount' for details
[DEPEND] Dependency filed for Local File System
```
later on, this message showed up:
```
You are in emergency mode. 
After logging in, type "journalctl -xb" to view system logs, 
"systemctl reboot" to reboot, "systemctl default" 
or ^D to try again to boot into default mode".
Give root password for maintenace (or press Control-D to continue):
```
I was able to log in as root and use the pc normally.

This likely happened when I needed to update the `linux-headers` package in order to be able to build the module [vendor-reset](https://github.com/gnif/vendor-reset.git). However, when doing so, I didn't update `linux`and probably ended up with the kernel version not matching that of its headers. It seemed to be a common cause of the problem when I looked online.

The fix was to update `linux` and `linux-headers` using the packages located in `/var/cache/pacman/pkg/`, making sure they both had the same version. I also removed the modules installed with dkms, just in case. After that my computer booted normally, and I was able to do a full system upgrade without any more issues.

## Drivers
### wifi
- https://github.com/aircrack-ng/rtl8812au/issues/1153
