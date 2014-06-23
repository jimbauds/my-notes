# git-2.0.0 Installation from source

### Prerequisite installation: gettext
```shell
sudo apt-get install gettext
sudo apt-get remove git git-man
```
---
### Prerequisite installation: asciidoc
```shell
Download from http://sourceforge.net/projects/asciidoc/
tar -xzf asciidoc-8.6.9.tar.gz
cd asciidoc-8.6.9
autoconf
./configure
make
make install
```
---
### Prerequisite installation: xsltproc
```shell
sudo apt-get install xsltproc
```
---
### Prerequisite installation: xmlto
#### **WARNING** (Install a bunch of stuff)
Check with this command (simulation):
```shell
apt-get -sV install xmlto
```
Install with this command
```shell
sudo apt-get install xmlto
```
---
### Installation: git
```shell
curl -O https://www.kernel.org/pub/software/scm/git/git-2.0.0.tar.xz
tar -xf git-2.0.0.tar.xz
cd git-2.0.0.0
make configure
./configure --prefix=/home/jimbauds/compile
make all doc
sudo make install install-doc install-html
```