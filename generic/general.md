
# Update and install these packages
```bash
dnf update -y
dnf install -y make git autoconf gcc gcc-c++ openssl openssl-devel curl firewalld vim policycoreutils-devel
```
after that run the following
```bash
systemctl enable firewalld.service
systemctl start firewalld.service
firewall-cmd --permanent --add-service=ssh
firewall-cmd --add-service=ssh
```

Which will enable ssh through the firewall and also enable the dynamic firewall daemon.


