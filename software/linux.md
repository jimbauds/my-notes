# Linux Commands

## Show CPU Info
```sh
cat /proc/cpuinfo
```
### Show kernel version
```sh
uname -r
```
## Kernel Upgrade (official)
```sh
# Show available kernel images
apt-cache search linux-image

# Install kernel
sudo apt-get install linux-image-x.x.x-xx
```

## Kernel Upgrade (not-official)
```sh
# Add Debian backports
sudo vim /etc/apt/sources.list
  deb http://http.debian.net/debian wheezy-backports main
  

```

### Basic Commands
```shell
ln -s /path/to/file /path/to/symlink #=> make symbolic link
sudo apt-cache search <package_name>

# Shutdown VPS
sudo shutdown –h now
```

### Debian
```shell
netstat -an | grep ESTABLISHED #=> Show established internet connections
netstat -natp

# Execute command at boot
/etc/rc.local
```

### RedHat, Ubuntu, Debian
```shell
lsb_release -a #=> Show OS Version
netstat -nlutp #=> Show Listening Ports (Udp/Tcp)
curl -I http://example.com => Get Header
ps auxf => Show running processes
```

### RedHat
```shell
sudo yum grouplist #=> Show Groups
```

### AWS (Amazon Web Services)
```shell
sudo -s #=> Become root
```

### Video Card Informations
```shell
lspci | grep VGA #=> Identify your hardware (even if not configured at all)
find /dev -group video #=> Check if the correct kernel driver is loaded
glxinfo | grep -i vendor #=> Check if the correct X driver is loaded
```

### Terminal Softwares
```shell
apt-get install w3m #=> Terminal Web Browser
```
### How to mount a remote directory over ssh on Linux
```shell
sudo apt-get install sshfs
sudo usermod -a -G fuse <user_name>
sshfs my_user@remote_host:/path/to/directory <local_mount_point>

#To unmount a ssh-mounted directory:
fusermount -u <local_mount_point>

# If you would like to automatically mount over ssh upon boot, set up passwordless ssh login, and append the following in /etc/fstab.
sudo vi /etc/fstab
sshfs#my_user@remote_host:/path/to/directory <local_mount_point> fuse user 0 0
```
