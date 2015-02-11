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
