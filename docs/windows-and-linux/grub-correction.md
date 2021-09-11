---
id: grub-correction
title: GRUB Correction
date: 2021-09-09 15:23:49
---

After installing Windows (and if your GRUB failed) you need boot with `LIVE CD/FLASH` and run in cmd:

> I have two LIVE CD/FLASH: 4Gb (Linux iso) and 8GB (Windows iso). I need to use 8G with windows iso.  

```cmd
bcdboot c:\Windows /s c: /l en-us
```

In case of error, correct it as written in this paragraph: https://papa31.github.io/hm/docs/new-disk/partitioning-new-disk/#single-windows

After that you need to reboot, enter into the BIOS/UEFI and change the boot order to:

## The Last Way to Repair

```bios
 -------- Boot (tab) -------------

...
# 1     [P0: P3-256]
# 2     [UEFI OS (P1:256)]
...
```

```bios
HARD DRIVE BBS PRIORITIES (subsection)
# 1     [P0 P3-256]
# 2     [NE-512]
...
```

## First Way to Repair

Set the first UEFI option to:

```uefi
P1:PS-256 (or P0-256 what disk first doesn`t matter)
```

And set second UEFI option to:

```uefi
OS UEFI P1:PS-256
```

Here main goal is installing GRUB without detection Windows.

Reboot Linux, open terminal and run:

```bash
sudo update-grub
```

Reboot again and change second boot option to:

```bios
P1:PS-256 (first option need to be the same: P1:PS-256)
```

Reboot. You should see grub table menu. Choose linux start.

Then, open terminal again and repeat previous command:

```bash
sudo update-grub
```

After that command you should see detected Windows.

```bash {8}
~ $ sudo update-grub  
[sudo] password for papa:
Generating grub configuration file ...  
Found linux image: /boot/vmlinuz-5.6.0-2-amd64  
Found initrd image: /boot/initrd.img-5.6.0-2-amd64  
Found memtest86+ image: /boot/memtest86+.bin  
/dev/sdc: open failed: No medium found  
Found Windows 10 on /dev/nvme0n1p1  
done
```

## Final boot setup

```bios
 -------- Boot (tab) -------------

...
# 1     [P0: P3-256]
# 2     [UEFI OS (P1:256)]
# 3     [UEFI: JetFlashTranscend …]
...
```

```bios
HARD DRIVE BBS PRIORITIES (subsection)

# 1     [P0 P3-256]
# 2     [NE-512]
# 3     [JetFlashTranscend ...]
...
```

```bios
CSM PARAMETERS (subsection)

...
Boot option filter:            [UEFI and Legacy]
Launch PXE OpROM:              [UEFI only]
Launch storage OpROM policy:   [UEFI only]
Launch Video OpROM policy:     [Legacy only]
...
```