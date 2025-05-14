## Update And Upgrade
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
## Install required packages
```
sudo apt install -y ca-certificates curl htop
```
## Install Tuned
```
sudo apt update &&
sudo apt upgrade -y &&
sudo apt install -y tuned &&
sudo systemctl enable tuned &&
sudo systemctl start tuned &&
sudo tuned-adm profile throughput-performance &&
sudo systemctl restart tuned &&
sudo tuned-adm active
```
## Add 8GB Swap Memory
```
if [ ! -f /swapfile ]; then
sudo fallocate -l 8G /swapfile &&
sudo chmod 600 /swapfile &&
sudo mkswap /swapfile &&
echo '/swapfile none swap sw,pri=2 0 0' | sudo tee -a /etc/fstab
sudo swapoff -a
sudo swapon -a
else
echo "Swapfile already exists."
fi
```
## Add 25% zRAM Swap Memory
```
sudo apt install -y zram-tools &&
sudo systemctl enable zramswap &&
sudo systemctl start zramswap &&
grep -q "^ALGO=" /etc/default/zramswap || echo "ALGO=lz4" | sudo tee -a /etc/default/zramswap > /dev/null &&
grep -q "^PERCENT=" /etc/default/zramswap || echo "PERCENT=25" | sudo tee -a /etc/default/zramswap > /dev/null &&
grep -q "^PRIORITY=" /etc/default/zramswap || echo "PRIORITY=1" | sudo tee -a /etc/default/zramswap > /dev/null &&
sudo systemctl restart zramswap
```
## Change Sysctl Parameters
```
grep -q "^vm.swappiness" /etc/sysctl.conf || echo "vm.swappiness = 10" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^vm.vfs_cache_pressure" /etc/sysctl.conf || echo "vm.vfs_cache_pressure = 50" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^fs.file-max" /etc/sysctl.conf || echo "fs.file-max = 9223372036854775807" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^net.core.somaxconn" /etc/sysctl.conf || echo "net.core.somaxconn = 8192" | sudo tee -a /etc/sysctl.conf > /dev/null
grep -q "^net.ipv4.tcp_tw_reuse" /etc/sysctl.conf || echo "net.ipv4.tcp_tw_reuse = 1" | sudo tee -a /etc/sysctl.conf > /dev/null
sudo sysctl -p
```
## Install Latest Docker
```
sudo install -m 0755 -d /etc/apt/keyrings &&
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc &&
sudo chmod a+r /etc/apt/keyrings/docker.asc &&
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update &&
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
