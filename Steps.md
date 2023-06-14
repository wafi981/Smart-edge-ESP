# STEPS:

## Step 1: Clone the repo
```  git clone https://github.com/smart-edge-open/private-wireless-experience-kits --recursive --branch=main ~/pwek ```

## Step 2: Initialize yaml file:

``` cd ~/pwek
./pwek_aio_provision.py --init-config > prov.yml
```

## Step 3: Changes in prov.yaml

## Step 4: Installing dependencies:
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
```
sudo su -
mkdir -p /usr/local/bin
wget -O /usr/local/bin/docker-compose "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)"
chmod a+x /usr/local/bin/docker-compose
```

Also install PyYAML before moving ahead.

## Step 5: Clone ESP:
```  
cd /opt
git clone -b master --depth=1 https://github.com/intel/Edge-Software-Provisioner.git esp
cd esp
```
Do not run build and run scipt. 

## Step 6: Edit the existing conf/config.yml or copy conf/config.sample.yml to conf/config.yml:

``` cp conf/config.sample.yml conf/config.yml ```
See the changes in the config.yml

## Step 7: Build and Run
``` ./build.sh
     ./run.sh
```

## Step 8: Navigate to /root/pwek:
``` 
./pwek_aio_provision.py --config prov.yml --run-esp-for-usb-boot
```
