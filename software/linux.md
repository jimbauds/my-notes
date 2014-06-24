# Linux Commands

### Basic Commands
```shell
ln -s /path/to/file /path/to/symlink #=> make symbolic link
```

### Debian
```shell
netstat -an | grep ESTABLISHED #=> Show established internet connections
netstat -natp
```

### RedHat, Ubuntu, Debian
```shell
lsb_release -a #=> Show OS Version
netstat -nlutp #=> Show Listening Ports (Udp/Tcp)
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