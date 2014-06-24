# Apache 2.4 installation procedure:

## Update the system and install required packages
- apt-get update
- apt-get install curl
- apt-get install build-essential

## Install APR (Apache Portable Runtime)
- ./configure
- make
- make install

## Install APR-util
- ./configure --with-apr=/usr/local/apr/
- make
- make install

## Install PCRE
- ./configure
- make
- make install

## Install Apache
- ./configure
- make
- make install