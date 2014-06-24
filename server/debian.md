### Initial Server Configuration:
```shell
# Connect to the server
ssh root@<server>

# Change root password
passwd

# Add new user for ssh access
adduser <username>

# Give new user sudo right
visudo #=> Open sudo config file and add new user rights
  - <username> ALL=(ALL:ALL) ALL

# Edit the ssh config file
nano /etc/ssh/sshd_config

# Change port number
  - Port <portnumber>

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
service ssh restart
```
### **IMPORTANT**
**TEST THE CONNECTION BEFORE EXIT**
```shell
# Open a new terminal
ssh -p <port_number> <username>@<server>
sudo apt-get update #=> This should work!
```
