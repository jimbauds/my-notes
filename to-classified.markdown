### Debian 7 NodeJS Installation
```sh
# Install
sudo apt-get -t wheezy-backports install nodejs
# Udpate nodejs command to node
sudo update-alternatives --install /usr/bin/node nodejs /usr/bin/nodejs 100
# Install NPM
curl https://www.npmjs.org/install.sh | sudo sh
```
