# Debian 7 Wheezy

### Init
```sh
# Connect to the server
ssh root@<server>

# Change root password
passwd

# Add new user for ssh access
adduser <username>

# Give new user sudo right
visudo
  <username> ALL=(ALL:ALL) ALL

# Edit the ssh config file
nano /etc/ssh/sshd_config

# Change port number
  Port <port_number>

# Remove the root login
  PermitRootLogin no

# Add a the new user access
  AllowUsers <username>

# Remove password authentication (only authorized keys are accepted)
  PasswordAuthentication no

# Create a new directory under the new user home folder,
# for storing is key.
mkdir /home/<username>/.ssh

# Store the user public key under authorized_keys
vi /home/<username>/.ssh/authorized_keys
  - put your public key and save the file

# Restart the ssh service
service ssh restart
```
### **IMPORTANT**
**TEST THE CONNECTION BEFORE EXIT**
```sh
# Open a new terminal
ssh -p <port_number> <username>@<server>
sudo apt-get update #=> This should work!
```
#### Firewall Configuration (Iptables)
```sh
# Iptables should be already install on a fresh Debian 7 Install
# sudo apt-get install iptables

# Flush current firewall rules
sudo iptables -F

# Block null packets
sudo iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Reject syn-flood attack
sudo iptables -A INPUT -p tcp ! --syn -m state --state NEW -j DROP

# Reject XMAS packets
sudo iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# Allow localhost connection
sudo iptables -A INPUT -i lo -j ACCEPT

# Allow established connections
sudo iptables -I INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allow web server traffic (if needed)
sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp -m tcp --dport 443 -j ACCEPT

# Allow SSH connection from an IP Address
sudo iptables -A INPUT -p tcp -s <your_ip_address> -m tcp --dport <ssh_port> -j ACCEPT

# DROP ALL others INPUT/FORWARD connections
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP

# DROP all IPv6 Connections if you don't use IPv6
sudo ip6tables -P INPUT DROP
sudo ip6tables -P OUTPUT DROP
sudo ip6tables -P FORWARD DROP

# Accept all OUTPUT connections
# OUTPUT connections should be closed and configured carefully on highly secured systems
sudo iptables -P OUTPUT ACCEPT

# Save the rules permanently
sudo apt-get install iptables-persistent
sudo service iptables-persistent start
```
# To Classified
## Storing iptables rules in a file

###Create the file
```sh
editor /etc/iptables.test.rules
```

###Enter rules
```sh
*filter

# Allows all loopback (lo0) traffic and drop all traffic to 127/8 that doesn't use lo0
-A INPUT -i lo -j ACCEPT
-A INPUT ! -i lo -d 127.0.0.0/8 -j REJECT

# Accepts all established inbound connections
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allows all outbound traffic
# You could modify this to only allow certain traffic
-A OUTPUT -j ACCEPT

# Allows HTTP and HTTPS connections from anywhere (the normal ports for websites)
-A INPUT -p tcp --dport 80 -j ACCEPT
-A INPUT -p tcp --dport 443 -j ACCEPT

# Allows SSH connections 
# THE -dport NUMBER IS THE SAME ONE YOU SET UP IN THE SSHD_CONFIG FILE
-A INPUT -p tcp -m state --state NEW --dport 30000 -j ACCEPT
#-A INPUT -p tcp -s YOUR_IP_ADDRESS -m tcp --dport 22 -j ACCEPT

# Allow ping
#-A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT

# log iptables denied calls (access via 'dmesg' command)
-A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

# Reject all other inbound - default deny unless explicitly allowed policy:
-A INPUT -j REJECT
-A FORWARD -j REJECT

COMMIT
```
### Activate the rules
```sh
sudo iptables-restore < /etc/iptables.test.rules
```
### Save the new rules to the master iptables file
```sh
su
iptables-save > /etc/iptables.up.rules
editor /etc/network/if-pre-up.d/iptables
  #!/bin/sh
  /sbin/iptables-restore < /etc/iptables.up.rules
chmod +x /etc/network/if-pre-up.d/iptables
sudo apt-get install iptables-persistent
sudo service iptables-persistent start
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
## Debian 7 (Wheezy) Default /etc/apt/sources.list
```sh
deb http://http.debian.net/debian wheezy main
deb-src http://http.debian.net/debian wheezy main

deb http://http.debian.net/debian wheezy-updates main
deb-src http://http.debian.net/debian wheezy-updates main

deb http://security.debian.org/ wheezy/updates main
deb-src http://security.debian.org/ wheezy/updates main

```

### Update Hostname
```sh
# Update hostname
sudo nano /etc/hostname
# Update file to correspond to new hostname
sudo nano /etc/hosts
```

### Change Keyboard Map
```sh
setxkbmap ca
# For permanent change add the command to ~./xsessionrc
```






