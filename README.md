# Dev Guides
![Last Commit](https://img.shields.io/github/last-commit/josecgeo/josecgeo.github.io)
- [Debian](#debian)
  - [Update And Upgrade](#update-and-upgrade)
  - [Install required packages](#install-required-packages)
  - [Install Tuned](#install-tuned)
  - [Add 8GB Swap Memory](#add-8gb-swap-memory)
  - [Add zRAM Swap Memory](#add-zram-swap-memory)
  - [Change Sysctl Parameters](#change-sysctl-parameters)
  - [Install Latest Docker](#install-latest-docker)
  - [Install Periphery Agent for Komodo](#install-periphery-agent-for-komodo)
- [Odoo Installation](#Odoo)
  - [Update And upgrade](#Update-And-Upgrade---Odoo)
  - [Install required packages](#Install-required-packages---Odoo)
  - [Install wkhtmltopdf 0.12.6.1-3 - Odoo](#Install-wkhtmltopdf-0.12.6.1-3-Odoo)
  - [Install Required Python Packages - Odoo](#install-required-python-packages---odoo-global-python-environment)
  - [Installing PostgreSQL 17](#Installing-PostgreSQL-17)
  - [Optional - Clone the Odoo themes repository](#optional---clone-the-odoo-themes-repository-to-optodoothemes-you-may-change-this-accordingly)
  - [Setting up odoo.conf](#setting-up-odooconf-at-optodooodoocconf)
  - [Setting up odoo.service](#setting-up-odooservice-at-optodooodooservice-virtual-python-environment)

# Debian
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
echo '/swapfile none swap sw,pri=1 0 0' | sudo tee -a /etc/fstab
sudo swapoff -a
sudo swapon -a
else
echo "Swapfile already exists."
fi
```
## Add zRAM Swap Memory
```
sudo apt install -y zram-tools &&
grep -q "^ALGO=" /etc/default/zramswap || echo "ALGO=lz4" | sudo tee -a /etc/default/zramswap > /dev/null &&
grep -q "^PERCENT=" /etc/default/zramswap || echo "PERCENT=25" | sudo tee -a /etc/default/zramswap > /dev/null &&
grep -q "^PRIORITY=" /etc/default/zramswap || echo "PRIORITY=2" | sudo tee -a /etc/default/zramswap > /dev/null &&
sudo systemctl enable zramswap &&
sudo systemctl start zramswap &&
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
## Install Periphery Agent for Komodo
```
curl -sSL https://raw.githubusercontent.com/moghtech/komodo/main/scripts/setup-periphery.py | python3 - --force-service-file &&
sudo systemctl enable periphery &&
sudo systemctl restart periphery
```
# Odoo
## Update And Upgrade - Odoo
```
sudo apt update &&
sudo apt upgrade -y &&
sudo dpkg --configure -a &&
sudo apt-get autoremove -y &&
sudo apt-get install -f -y &&
sudo apt-get clean -y
```
## Install Required Packages - Odoo
```
sudo apt install -y \
python3 python3-dev python3-venv python3-pip python3-setuptools python3-wheel \
python3-pandas python3-cffi python3-certbot-nginx \
libzip-dev libxslt1-dev libldap2-dev libsasl2-dev libjpeg-dev libpq-dev libffi-dev \
libxml2-dev libssl-dev libjpeg8-dev liblcms2-dev libblas-dev zlib1g-dev \
libatlas-base-dev libmysqlclient-dev libfreetype6-dev \
git wget htop curl zip unzip ncdu fail2ban \
xfonts-75dpi xfonts-base fontconfig lsb-release gpg xfsprogs \
build-essential nodejs npm &&
sudo ln -sf /usr/bin/nodejs /usr/bin/node &&
sudo npm install -g less less-plugin-clean-css && npm fund
```
## Install wkhtmltopdf 0.12.6.1-3 - Odoo
```
sudo wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.bookworm_amd64.deb &&
sudo wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-3/wkhtmltox_0.12.6.1-3.jammy_amd64.deb &&
sudo dpkg -i  wkhtmltox_0.12.6.1-3.bookworm_amd64.deb || sudo dpkg -i  wkhtmltox_0.12.6.1-3.jammy_amd64.deb &&
sudo rm -rf wkhtmltox_0.12.6.1-3.bookworm_amd64.deb && sudo rm -rf wkhtmltox_0.12.6.1-3.jammy_amd64.deb &&
sudo wkhtmltopdf --version
```
## Install Required Python Packages - Odoo (Global Python Environment)
#### Odoo 18
```
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
setuptools wheel &&
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
asana openpyxl pyzk gdown numpy_utils phonenumbers PyJWT google_auth \
num2words ofxparse dbfread ebaysdk firebase_admin pdfminer.six qrcode email_validator \
pyOpenSSL dropbox pyncclient boto3 nextcloud-api-wrapper paramiko astor &&
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
-r https://github.com/odoo/odoo/raw/18.0/requirements.txt
```
#### Odoo 17
```
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
setuptools wheel &&
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
asana openpyxl pyzk gdown numpy_utils phonenumbers PyJWT google_auth \
num2words ofxparse dbfread ebaysdk firebase_admin pdfminer.six qrcode email_validator \
pyOpenSSL dropbox pyncclient boto3 nextcloud-api-wrapper paramiko astor &&
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
-r https://github.com/odoo/odoo/raw/17.0/requirements.txt
sudo pip3 install --upgrade --ignore-installed --no-cache --break-system-packages \
cryptography==38.0.4 blosc2==2.3.0 numpy==1.26.4 plotly==5.22.0
```
## Install Required Python Packages - Odoo (Virtual Python Environment)
### Setup and activate virtual python environment at /opt/odoo/venv
```
python3 -m venv /opt/odoo/venv &&
source /opt/odoo/venv/bin/activate
```
#### Odoo 18
```
sudo pip3 install --upgrade --ignore-installed --no-cache \
setuptools wheel &&
sudo pip3 install --upgrade --ignore-installed --no-cache \
asana openpyxl pyzk gdown numpy_utils phonenumbers PyJWT google_auth \
num2words ofxparse dbfread ebaysdk firebase_admin pdfminer.six qrcode email_validator \
pyOpenSSL dropbox pyncclient boto3 nextcloud-api-wrapper paramiko astor &&
sudo pip3 install --upgrade --ignore-installed --no-cache \
-r https://github.com/odoo/odoo/raw/18.0/requirements.txt
```
#### Odoo 17
```
sudo pip3 install --upgrade --ignore-installed --no-cache \
setuptools wheel &&
sudo pip3 install --upgrade --ignore-installed --no-cache \
asana openpyxl pyzk gdown numpy_utils phonenumbers PyJWT google_auth \
num2words ofxparse dbfread ebaysdk firebase_admin pdfminer.six qrcode email_validator \
pyOpenSSL dropbox pyncclient boto3 nextcloud-api-wrapper paramiko astor &&
sudo pip3 install --upgrade --ignore-installed --no-cache \
-r https://github.com/odoo/odoo/raw/17.0/requirements.txt
sudo pip3 install --upgrade --ignore-installed --no-cache \
cryptography==38.0.4 blosc2==2.3.0 numpy==1.26.4 plotly==5.22.0
```
### Deactivate virtual python environment at /opt/odoo/venv
```
deactivate
```
## Installing PostgreSQL 17
```
sudo sh -c 'echo "deb https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' -y  &&
sudo wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -  &&
sudo apt update && 
sudo apt install -y -f \
postgresql-17
```
## Setting up Postgres user for Odoo | User-Odoo Pass-password123$
```
sudo -u postgres psql -c "DROP USER IF EXISTS odoo;" &&
sudo -u postgres psql -c "CREATE USER odoo WITH PASSWORD 'password123$';" &&
sudo -u postgres psql -c "ALTER USER odoo WITH CREATEDB;"
```
## Clone the Odoo github repository to /opt/odoo/server (You may change this accordingly)
### Odoo 18
```
sudo git clone https://www.github.com/odoo/odoo.git --depth 1 --branch 18.0 /opt/odoo/server
```
### Odoo 17
```
sudo git clone https://www.github.com/odoo/odoo.git --depth 1 --branch 17.0 /opt/odoo/server
```
## Optional - Clone the Odoo themes repository to /opt/odoo/themes (You may change this accordingly)
### Odoo 18
```
sudo git clone https://github.com/odoo/design-themes.git --depth 1 --branch 18.0 /opt/odoo/themes
```
### Odoo 17
```
sudo git clone https://github.com/odoo/design-themes.git --depth 1 --branch 17.0 /opt/odoo/themes
```
## Setting up odoo.conf at /opt/odoo/odoo.cconf
```
sudo tee /opt/odoo/odoo.conf > /dev/null << 'EOF'
[options]
db_host = localhost
db_port = 5432
db_user = odoo
db_password = password123$
logfile = /opt/odoo/odoo.log
addons_path = /opt/odoo/server/addons, /opt/odoo/server/odoo/addons
EOF
```
## Setting up odoo.service at /opt/odoo/odoo.service (Global Python Environment)
```
sudo tee /opt/odoo/odoo.service > /dev/null << 'EOF'
[Unit]
Description=Odoo
Requires=postgresql.service
After=network.target postgresql.service
[Service]
Type=simple
SyslogIdentifier=odoo
PermissionsStartOnly=true
User=odoo
Group=odoo
ExecStart=/usr/bin/python3 /opt/odoo/server/odoo-bin -c /opt/odoo/odoo.conf
StandardOutput=journal+console
Restart=always
[Install]
WantedBy=multi-user.target
EOF &&
sudo rm -rf /etc/systemd/system/odoo.service &&
sudo ln -sf /opt/odoo/odoo.service /etc/systemd/system/odoo.service &&
sudo systemctl daemon-reload &&
sudo systemctl enable odoo &&
sudo systemctl start odoo
```
## Setting up odoo.service at /opt/odoo/odoo.service (Virtual Python Environment)
```
sudo tee /opt/odoo/odoo.service > /dev/null << 'EOF'
[Unit]
Description=Odoo
Requires=postgresql.service
After=network.target postgresql.service
[Service]
Type=simple
SyslogIdentifier=odoo
PermissionsStartOnly=true
User=odoo
Group=odoo
ExecStart=/opt/odoo/venv/bin/python3 /opt/odoo/server/odoo-bin -c /opt/odoo/odoo.conf
StandardOutput=journal+console
Restart=always
[Install]
WantedBy=multi-user.target
EOF &&
sudo rm -rf /etc/systemd/system/odoo.service &&
sudo ln -sf /opt/odoo/odoo.service /etc/systemd/system/odoo.service &&
sudo systemctl daemon-reload &&
sudo systemctl enable odoo &&
sudo systemctl start odoo
```