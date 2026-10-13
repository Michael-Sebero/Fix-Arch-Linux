<p align="center">
    <img src="https://i.postimg.cc/VN4QtMzw/Fix-Arch.png" style="width:50%; height:auto;" />
</p>

Repair tool for Arch Linux and Arch-based distributions (Artix, EndeavourOS, Manjaro, CachyOS). It supports systemd, OpenRC, runit, s6 and dinit runs on an installed system or from a live USB, and asks before it changes anything. Every file it replaces or moves is kept in `/var/lib/fix-arch-linux/backup/<date>/`.

## What this script fixes

### Diagnostics

. Health check with pass/warn/fail results and the action that fixes each failure

. Support report for forum posts, saved to your home directory

. System logs: errors from this and the previous boot, kernel errors, the last pacman transaction, Xorg and display manager logs

### Packages

. Safe system updates: shows Arch news since your last upgrade, updates the keyrings first, resolves file conflicts, applies the linux-firmware split procedure, protects legacy NVIDIA GPUs, then reports new .pacnew files, pending reboots and unbuilt DKMS modules

. Unable to lock database (pacman, pamac and the pacman keyring)

. Failed to synchronize all databases: removed repositories such as [community], empty mirrorlists, the pacman 7 download user, local repository permissions, clock and DNS errors, corrupted sync databases

. Corrupted PGP signatures and GPG key errors: updates the keyring packages and rebuilds the keyring only when verification fails, keeping keys you added yourself

. Exists in filesystem conflicts: moves files that no package owns out of the way and retries

. Corrupted packages: checks installed files for missing files or SHA256 mismatches and reinstalls the exact installed version from the cache

. Damaged pacman database entries (missing desc or files, duplicate entries)

. Interrupted upgrades and power loss during an update

. Mirrorlists: reflector, the archlinux.org mirror status or rankmirrors, and the distribution's own tool on Manjaro, EndeavourOS and CachyOS

. .pacnew and .pacsave merging with pacdiff, or a built-in merger when pacdiff is unavailable

. Rollback of the last upgrade or of a single package from the cache or the Arch Linux Archive

. AUR packages broken by library or Python updates, including a broken yay or paru

. Low disk space: package cache, orphans, journal, core dumps, AUR build caches, unused Flatpak runtimes

### Boot and login

. Botched kernel updates: mounts /boot from fstab, restores kernels that were updated while /boot was unmounted, rebuilds the initramfs (mkinitcpio, dracut, booster) and DKMS modules, regenerates the GRUB configuration and checks systemd-boot entries

. GRUB reinstallation for UEFI and BIOS, re-signing with sbctl when Secure Boot is enabled

. NVIDIA: missing modules and headers, DKMS build failures, mismatched driver versions, and the 590 driver dropping Maxwell and Pascal (switches to nvidia-580xx-dkms)

. Login failures: faillock lockouts, locked or expired accounts, missing login shells, home files owned by root, full disks, missing desktop sessions, the Plasma 6.4 X11 session, disabled display managers

. sudo and doas: broken sudoers files and missing wheel access

. Unbootable systems: from a live USB it unlocks LUKS, activates LVM, mounts the installed system (including btrfs subvolumes) and runs itself inside it

### System

. Clock time: NTP synchronization (systemd-timesyncd, chrony, ntpd) with an HTTP fallback, time zone and hardware clock

. Connectivity: blocked radios, missing drivers and firmware, conflicting network managers, NetworkManager with iwd, and a gateway, DNS and HTTPS test

. DNS and DNSCrypt: broken /etc/resolv.conf links, stopped local resolvers, invalid dnscrypt-proxy configuration, socket and service conflicts

. Sound: missing sof-firmware, PipeWire packages and user services, WirePlumber state

. Bluetooth: blocked radio, driver, packages and service

. Locale errors: generates the locales set in /etc/locale.conf

. Failed services

## How to Install

```
sudo curl -fLo /usr/local/bin/fix-arch-linux https://raw.githubusercontent.com/Michael-Sebero/Fix-Arch-Linux/main/fix-arch-linux && sudo chmod 755 /usr/local/bin/fix-arch-linux
```

## Usage

Run `fix-arch-linux` to open the menu, or pass an action:

```
fix-arch-linux check
```

`fix-arch-linux --list` shows every action. `--noconfirm` accepts the default answer for every prompt. The script asks for your password through sudo, doas, run0 or su.

If the system no longer boots, start an Arch Linux ISO and run:

```
curl -fLO https://raw.githubusercontent.com/Michael-Sebero/Fix-Arch-Linux/main/fix-arch-linux && bash fix-arch-linux rescue
```

## Donations and Contacts
PayPal: https://www.paypal.com/donate/?cmd=_donations&business=YYGU9JWJEE2AG

Email: michaelsebero@disroot.org
