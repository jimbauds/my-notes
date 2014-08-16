```sh
uname -mrns
wget https://www.kernel.org/pub/linux/kernel/v3.x/linux-3.16.tar.xz
wget https://www.kernel.org/pub/linux/kernel/v3.x/linux-3.16.tar.sign
unxz linux-3.16.tar.xz
gpg --recv-keys  00411886
gpg --verify linux-3.16.tar.sign
sudo apt-get install libncurses5-dev
sudo apt-get install fakeroot
sudo apt-get install kernel-package
tar -xf linux-3.16.tar
cd linux-3.16/
su
cp /boot/config-'uname -r' .config
make menuconfig
make-kpkg clean
fakeroot make-kpkg --append-to-version "-rockon" --revision "1" --initrd kernel_image kernel_headers
dpkg -i linux-image-3.16.0-rockon_1_amd64.deb
dpkg -i linux-headers-3.16.0-rockon_1_amd64.deb
reboot
```
