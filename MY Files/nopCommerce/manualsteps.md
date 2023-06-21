### Install dotnet 7
--------------------

wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
sudo chmod +x ./dotnet-install.sh
./dotnet-install.sh --channel 7.0

sudo vi ~/.bashrc
   export PATH="/home/ubuntu/.dotnet:$PATH"
source ~/.bashrc

### Get nopCommerce
-------------------

mkdir ~/tmp
cd tmp
wget https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.3/nopCommerce_4.60.3_NoSource_linux_x64.zip
sudo apt-get install unzip
sudo unzip nopCommerce_4.60.3_NoSource_linux_x64.zip
mkdir bin logs
cd ~
sudo chown -R ubuntu:ubuntu tmp/ 
cd tmp
dotnet Nop.Web.dll --urls "http://0.0.0.0:5000"



***********Sir version:
------------------------

sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-7.0

sudo apt install unzip

sudo mkdir /usr/share/nopCommerce
cd /usr/share/nopCommerce/
sudo wget https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.3/nopCommerce_4.60.3_NoSource_linux_x64.zip
sudo unzip nopCommerce_4.60.3_NoSource_linux_x64.zip
sudo mkdir bin
sudo mkdir logs

sudo adduser nop
sudo chgrp -R nop /usr/share/nopCommerce/
sudo chown -R nop /usr/share/nopCommerce/

sudo nano /etc/systemd/system/nopCommerce.service

sudo systemctl enable nopCommerce.service
sudo systemctl start nopCommerce.service
sudo systemctl status nopCommerce.service
