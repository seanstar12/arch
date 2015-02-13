### Stupid Permission Things...
#### Pacman.conf 'vim /etc/pacman.conf'
```
comment out SigLevel = ... (line 40)
```

#### Add Archlinuxfr
```
[archlinuxfr]
Server = http://repo.archlinux.fr/$arch
```
#### Navigate to 'cd /var/cache/pacman/pkg'
```
pacman -U {the package that failed}
```
### Add User to Wheel For Permissions
```
useradd steve
passwd steve
gpasswd -a steve wheel
```
### Sudo stuff
#### visudo
```
uncomment line 79
```
### Thinkpad Scroll Config
```
sudo wget --output-document /etc/X11/xorg.conf.d/30-thinkpad.conf http://goo.gl/qOn330 
```
### Systemctl stuff
```
sudo systemctl enable gdm
sudo systemctl enable NetworkManager
```

### Install Diff
```
CHANGED -- just incase uefi is there, we give it PLENTY of room... like 5 times more than it would ever need
Konami Code: o, y, n, enter, enter, +250M, ef02, n, enter, enter, enter, enter, x, a, 2, 2, enter, w, y.

pacman -S xf86-video-nouveau mesa-libgl lib32-mesa-libgl



###Notes from install
```
chroot /mnt extlinux -i /boot/syslinux
cat /mnt/usr/lib/syslinux/bios/gptmbr.bin > /dev/sda
cp /mnt/usr/lib/syslinux/bios/*.c32 /mnt/boot/syslinux/
vi /mnt/boot/syslinux/syslinux.cfg


cp /etc/resolv.conf /mnt/etc/resolv.conf
chroot /mnt
haveged -w 1024
pacman-key --init
pacman-key --populate archlinux
pkill haveged
vi /etc/pacman.conf
** Comment out SIG
** ADD ARCHLINUXFR


** EDIT MIRROR LIST
vi /etc/pacman.d/mirrorlist


pacman -Syy yaourt
**FAILED STUFF
:: File /var/cache/pacman/pkg/yajl-2.1.0-1-x86_64.pkg.tar.xz is corrupted (invalid or corrupted package (PGP signature)).

cd /var/cache/pacman/pkg 
pacman -U yajl-2.1.0-1-x86_64.pkg.tar.xz 
pacman -S yaourt

**FAILED///

useradd sean
gpasswd -a sean wheel
echo "sean    ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers;
mkdir /home/sean
chown sean:sean /home/sean
su sean

yaourt -S mkinitcpio-btrfs

sudo pacman -U kexec-tools-2.0.8-1-x86_64.pkg.tar.xz 

yaourt -S mkinitcpio-btrfs

sudo vi /etc/mkinitcpio.conf


** ADD MODULES TO mkinitcpio.conf
vi /etc/mkinitcpio.conf
mkinitcpio -p linux

btrfs subvolume list -t /btrfs

vi /etc/fstab

/dev/sda2 / btrfs defaults,noatime 0 0
/dev/sda2 /var/lib/ArchHDD btrfs defaults,noatime 0 0
/var/lib/ArchHDD/boot /boot none rw,bind 0 0

Edit btrfs stuff here.
To break your stuff >>

btrfs subvolume set-default 0 /
*** OR This one, not sure...
mkdir /btr
mount /dev/sda2 /btr
btrfs subvolume set-default 0 /btr

vi /etc/fstab    ---->
/dev/sda2 /var/lib/ArchHDD btrfs defaults,noatime,subvol=__active 0 0

then reboot

mkdir /btr
mount /dev/sda2 /btr
cp -R /btr/boot/* /btr/__active/boot/

vi /btr/__active/etc/fstab
REMOVE   /var/lib/ArchHDD/boot /boot none rw,bind 0 0
btrfs subvolume set-default 257 /btr/__active
```

