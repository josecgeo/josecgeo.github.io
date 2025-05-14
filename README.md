# Update and upgrade applications
~~~
sudo apt update &&
sudo apt upgrade -y &&
sudo dpkg --configure -a &&
sudo apt-get autoremove -y &&
sudo apt-get install -f -y &&
sudo apt-get clean -y &&
sudo apt update &&
sudo apt upgrade -y
~~~
# Install Tuned
```
sudo apt update &&
sudo apt upgrade -y &&
sudo apt install tuned -y &&
sudo systemctl enable tuned &&
sudo systemctl start tuned &&
sudo tuned-adm profile throughput-performance &&
sudo systemctl restart tuned &&
sudo tuned-adm active
```
# Add 8GB swap memory
```
if [ ! -f /swapfile ]; then
sudo fallocate -l 8G /swapfile &&
sudo chmod 600 /swapfile &&
sudo mkswap /swapfile &&
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
sudo swapoff -a
sudo swapon -a
else
echo "Swapfile already exists."
fi
```
# Sysctl Parameters
```
grep -q "^vm.swappiness" /etc/sysctl.conf || echo "vm.swappiness = 10" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^vm.vfs_cache_pressure" /etc/sysctl.conf || echo "vm.vfs_cache_pressure = 50" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^fs.file-max" /etc/sysctl.conf || echo "fs.file-max = 9223372036854775807" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^net.core.somaxconn" /etc/sysctl.conf || echo "net.core.somaxconn = 8192" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^net.ipv4.tcp_tw_reuse" /etc/sysctl.conf || echo "net.ipv4.tcp_tw_reuse = 1" | sudo tee -a /etc/sysctl.conf > /dev/null
sudo sysctl -p
```