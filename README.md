# Archlinux-installation-guide 🌠

## Step 1 - livecd

```bash
setfont cyr-sun16 (cyr-sun16, sun12x22 or else)
```

```bash
nano /etc/pacman.conf
-paralel downloads to 15 (change)*
```


```bash
iwctl
-device list
-station devicename* scan
-station devicename* get-networks
-station devicename* connect networkname*
```


```bash
ping archlinux.com
```


```bash
lsblk
```


```bash
cfdisk
-1G > EFI
-50% of ram > SWAP
-remains > linuxfilesystem
```


```bash
mkfs.ext4 /dev/maindiskpart*
mkfs.fat -F32 /dev/bootdiskpart*
mkswap /dev/swapdiskpart*
```


```bash
mount /dev/maindiskpart* /mnt
mount --mkdir dev/bootdiskpart* /mnt/boot/efi
swapon dev/swapdiskpart*
```


```bash
pacstrap -K /mnt
-base linux linux-firmware
-grub efibootmgr
-sudo
-nano vim
-networkmanager
```


```bash
genfstab -U /mnt >> /mnt/etc/fstab
```


```bash
arch-chroot /mnt
```



## Step 2 - system config
```bash
ln -sf /usr/share/zoneinfo/Europe/Moscow /etc/localtime

hwclock --systohc

timedatectl set-ntp true
```


```bash
nano /etc/locale.gen
-en_US.UTF-8 (uncomment)
-ru_RU.UTF-8 (uncomment)

locale-gen

echo "LANG=en_US.UTF-8" > etc/locale.conf
```


```bash
nano /etc/vconsole.conf
-KEYMAP= en (add)
-FONT=cyr-sun16 (sun12x22 or else) (add)
```


```bash
echo "pcname*" > etc/hostname

nano /ets/hosts 
- 127.0.1.1 localhost.localdomain pcname* (add)
```

```bash
systemctl enable NetworkManager
```

```bash
grub-install /dev/disk*
grub-mkconfig -o /boot/grub/grub.cfg
```

```bash
useradd -m -G wheel username*
passwd username*

visudo
-%wheel ALL = (ALL) ALL (uncomment)
```


```bash
passwd
```


```bash
exit

umount -R /mnt

reboot
```



## Step 3 - after installation
```bash
nmtui
-Acticate a connection
```


```bash
pacman -S git neofetch
```

```bash
neofetch
```



## nvidia drivers 💀
```bash
pacman -S nvidia nvidia-utils nvidia-settings
```

```bash
nano /etc/mkinitcpio.conf
-remove kms from HOOKS
```

```bash
nvidia-settings
```
