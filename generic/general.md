
# Update and install these packages
```bash
dnf update -y
dnf install -y make git autoconf gcc gcc-c++ openssl openssl-devel curl firewalld vim policycoreutils-devel postgresql-devel node-gyp clang automake gettext pkgconfig boost boost-devel wget python python3 node ruby
```
after that run the following
```bash
systemctl enable firewalld.service
systemctl start firewalld.service
firewall-cmd --permanent --add-service=ssh
firewall-cmd --add-service=ssh
```

Which will enable ssh through the firewall and also enable the dynamic firewall daemon.




# Swap space

If there is no swap space, you **must** add one especially with machines with less than 16GB of physical RAM.


## Finding out if there is swap
run `free -h` if there is no line that starts with `Swap` then you don't have swap.


## Creating Swap

Swap space should be a minimum of 4GB, if your memory is greater than 8Gb then swap should be half your physical RAM.
run the following as root to create a swap file
```bash
dd if=/dev/zero of=/swapfile bs=1024 count=10485760
mkswap /swapfile
chmod -R 0600 /swapfile
swapon /swapfile
```

To automount swap on system boot run the following again as root.

`echo "/swapfile swap swap defaults 0 0" >> /etc/fstab`

