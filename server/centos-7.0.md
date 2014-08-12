# CentOS 7.0 x64

## Initial Server Configuration
### Connect to the server
```sh
ssh root@<server>
```
### Change root password
```sh
passwd
```
### Add new user for SSH access
```sh
adduser <username>
passwd <username>
```

### Install sudo (not install by  default)
```sh
yum install sudo
```

### Give new user sudo right
```sh
# Execute
visudo
# Add the following
<username> ALL=(ALL) ALL
```
### Edit the SSH config file
```sh
vi /etc/ssh/sshd_config

# Change port number
Port <port_number>

# Remove the root login
PermitRootLogin no

# Add a the new user access
AllowUsers <username>

# Remove password authentication (only authorized keys are accepted)
PasswordAuthentication no
```
### New User Access
```sh
# Create a new directory under the new user home folder, for storing is key.
mkdir /home/<username>/.ssh
chmod 700 /home/<username>/.ssh

# Store the user public key under authorized_keys
vi /home/<username>/.ssh/authorized_keys
# Put the public key and save the file
chmod 600 authorized_keys
```
### Restart the SSH service
```sh
service sshd restart
```

### **IMPORTANT**
**TEST THE CONNECTION BEFORE EXIT**
```sh
# Open a new terminal
ssh -p <port_number> <username>@<server>
# This should work!
sudo yum update
```
## Repos
### EPEL Repos Installtion
```sh
curl -O http://dl.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm
sudo rpm -ivh epel-release-7-0.2.noarch.rpm
```
## Firewall Installation/Configuration (Iptables)
### Check if iptables is installed
```sh
sudo iptables -V
sudo rpm -q iptables
```

### Enable iptables and ip6tables and Mask firewalld
I prefer to use iptables for now.
```sh
sudo yum install iptables-services
sudo systemctl mask firewalld.service
sudo systemctl enable iptables.service
sudo systemctl enable ip6tables.service
```
### Check if iptables is running
```sh
sudo lsmod | grep ip_tables
```
### Check current rules
```sh
sudo iptables -L -n
```
### Iptables Configuration
```sh
# Temporary ACCEPT ALL connections to not lock yourself out from the server (SSH)
sudo iptables -P INPUT ACCEPT

# Now, you can FLUSH the current firewall rules
sudo iptables -F

# Block null packets
sudo iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Reject syn-flood attack
sudo iptables -A INPUT -p tcp ! --syn -m state --state NEW -j DROP

# Reject XMAS packets
sudo iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# Accept localhost connection
sudo iptables -A INPUT -i lo -j ACCEPT

# Accept established connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Add yourself for SSH connection
sudo iptables -A INPUT -p tcp -s <your_ip> --dport <ssh_port> -j ACCEPT

# log iptables denied calls (access via 'dmesg' command)
iptables -A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

# DROP ALL others INPUT/FORWARD connections
iptables -P INPUT DROP
iptables -P FORWARD DROP

# Accept all OUTPUT connections
iptables -P OUTPUT ACCEPT

# DROP all IPv6 Connections
ip6tables -P INPUT DROP
ip6tables -P OUTPUT DROP
ip6tables -P FORWARD DROP
```
### Save permanently the rules
```sh
yum install policycoreutils
service iptables save
service ip6tables save
```
## Log files
### Default location
```sh
/var/log/ 
```
### Dispatch log using rsyslog
```sh
sudo vi /etc/rsyslog.d/my_iptables.conf
  :msg,contains,"iptables denied: " /var/log/iptables.log
```
## Docker Installation
### From EPEL Repos
```sh
# Check Version
sudo yum info docker-io
# Install
sudo yum install docker-io
```
### From CentOS 7 Extra Repos
```sh
# Check Version
sudo yun info docker

# Install
sudo yum install docker
```
## To classified
```sh
# Allow web server traffic
sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT

# Block everything else, Allow all outgoing connections
sudo iptables -P OUTPUT ACCEPT
sudo iptables -P INPUT DROP

Protocol 2
Port 22
UsePrivilegeSeparation yes
SyslogFacility AUTH
LogLevel INFO
PermitRootLogin no
StrictModes yes
LoginGraceTime 30
RSAAuthentication yes
PasswordAuthentication no
PubkeyAuthentication yes
AllowTcpForwarding no
X11Forwarding no
PrintLastLog yes
KeepAlive yes
UsePAM no
Subsystem sftp /usr/libexec/openssh/sftp-server
```

