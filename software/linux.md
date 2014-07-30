# Linux Commands
## General Commands
### Show CPU Info
```sh
cat /proc/cpuinfo
```
### Show Kernel Version
```sh
uname -r
```
### Show OS Version
```sh
lsb_release -a #=> Show OS Version
cat /proc/version
cat /etc/issue
```
### Shutdown VPS
```sh
sudo shutdown -h now
```
### Make Symbolic Link
```sh
ln -s /path/to/file /path/to/symlink
```
### Search Package
```sh
# Debian
sudo apt-cache search <package_name>

# Red Hat
sudo yum search <package_name>
```
### Execute a Command at Boot
```sh
# Debian
/etc/rc.local #=> Put your cmd in this file
```
### Show Running Processes
```sh
ps auxf
```
### Show Groups
```sh
# Red Hat
sudo yum grouplist
```
## Network
### Get HTTP Server Headers
```sh
curl -I http://example.com
```
### Show Established Connections
```sh
netstat -an | grep ESTABLISHED
netstat -natp
```
### Show Listening Ports (udp/tcp)
```sh
netstat -nlutp
```
## Others
### AWS (Amazon Web Services)
```sh
sudo -s #=> Become root
```
### Video Card Informations
```sh
lspci | grep VGA #=> Identify your hardware (even if not configured at all)
find /dev -group video #=> Check if the correct kernel driver is loaded
glxinfo | grep -i vendor #=> Check if the correct X driver is loaded
```
### Terminal Softwares
```sh
apt-get install w3m #=> Terminal Web Browser
```
### How to mount a remote directory over ssh on Linux
```sh
sudo apt-get install sshfs
sudo usermod -a -G fuse <user_name>
sshfs my_user@remote_host:/path/to/directory <local_mount_point>

#To unmount a ssh-mounted directory:
fusermount -u <local_mount_point>

# If you would like to automatically mount over ssh upon boot, set up passwordless ssh login, and append the following in /etc/fstab.
sudo vi /etc/fstab
sshfs#my_user@remote_host:/path/to/directory <local_mount_point> fuse user 0 0
```
### Kernel Upgrade (official)
```sh
# Show available kernel images
apt-cache search linux-image

# Install kernel
sudo apt-get install linux-image-x.x.x-xx
```
### Kernel Upgrade (not-official)
```sh
# Add Debian backports
sudo vim /etc/apt/sources.list
  deb http://http.debian.net/debian wheezy-backports main
```
