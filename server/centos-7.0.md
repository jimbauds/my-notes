# CentOS 7.0 x64

## Initial Server Configuration
```sh
# Connect to the server
ssh root@<server>

# Change root password
passwd

# Add new user for ssh access
adduser <username>

# Give new user sudo right
visudo
  - <username> ALL=(ALL:ALL) ALL

# Edit the ssh config file
vi /etc/ssh/sshd_config

# Change port number
  - Port <port_number>

# Remove the root login
  - PermitRootLogin no

# Add a the new user access
  - AllowUsers <username>

# Remove password authentication (only authorized keys are accepted)
  - PasswordAuthentication no

# Create a new directory under the new user home folder,
# for storing is key.
mkdir /home/<username>/.ssh

# Store the user public key under authorized_keys
vi /home/<username>/.ssh/authorized_keys
  - put your public key and save the file

# Restart the ssh service
service sshd restart
```

### **IMPORTANT**
**TEST THE CONNECTION BEFORE EXIT**
```sh
# Open a new terminal
ssh -p <port_number> <username>@<server>
sudo yum update #=> This should work!
```
### EPEL Repos Installtion
```sh
curl -O http://dl.fedoraproject.org/pub/epel/beta/7/x86_64/epel-release-7-0.2.noarch.rpm
```


## Firewall Installation/Configuration (Iptables)
```sh
# Check if iptables is installed
sudo iptables -V
sudo rpm -q iptables

# Enable iptables and ip6tables
yum install iptables-services
systemctl mask firewalld.service
systemctl enable iptables.service
systemctl enable ip6tables.service

# Check if iptables is running
sudo lsmod | grep ip_tables

# Enable iptables
# sudo system-config-securitylevel

# You can install iptables with this command
sudo yum install iptables

# Check current rules
sudo iptables -L -n

# Temporary ACCEPT all connection to not lock yourself out from the server (SSH)
sudo iptables -P INPUT ACCEPT

# Now, you can flush the current firewall rules
sudo iptables -F

# Accept localhost connection
sudo iptables -A INPUT -i lo -j ACCEPT

# Accept established connections
sudo iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Add yourself for SSH connection
sudo iptables -A INPUT -p tcp -s <your_ip> --dport <ssh_port> -j ACCEPT

# Drop ALL OTHERs INPUT/FORWARD connections
iptables -P INPUT DROP
iptables -P FORWARD DROP

# Accept all OUTPUT connections
iptables -P OUTPUT ACCEPT

# DROP all IPv6 Connections
ip6tables -P INPUT DROP
ip6tables -P OUTPUT DROP
ip6tables -P FORWARD DROP

# Save permantly the rules
service iptables save
service ip6tables save
```

## Log files
### Default location
```sh
/var/log/ 
/var/log/kern.log
```
### Dispatch log using rsyslog
```sh
sudo nano /etc/rsyslog.d/my_iptables.conf

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
# Block null packets
sudo iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Reject syn-flood attack
sudo iptables -A INPUT -p tcp ! --syn -m state --state NEW -j DROP

# Reject XMAS packets
sudo iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# Allow localhost connection
sudo iptables -A INPUT -i lo -j ACCEPT

# Allow outgoing connections
sudo iptables -I INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow web server traffic
sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT

# Allow SSH connection from an IP Address
sudo iptables -A INPUT -p tcp -s YOUR_IP_ADDRESS -m tcp --dport 22 -j ACCEPT

# Block everything else, Allow all outgoing connections
sudo iptables -P OUTPUT ACCEPT
sudo iptables -P INPUT DROP
```

