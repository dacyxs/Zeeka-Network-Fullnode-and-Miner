# <h1 align="center">Zeeka-Network-Fullnode-and-Miner</h1>

This guide uses https://github.com/mmc6185/node-testnets/blob/main/zeeka-network/bazooka/fullnode_manuel.md as a reference.


# Zeeka Fullnode Manual Installation

## We are doing a Linux system update.
```
sudo apt-get update && apt-get upgrade -y
```

## We install the necessary libraries
```
sudo apt-get -y install libssl-dev && apt-get -y install cmake build-essential git wget jq make gcc
```
![image](https://user-images.githubusercontent.com/101191449/189369723-4d784619-3b45-4c1b-a6ad-5f34539a13dd.png)

## We are installing rust toolchain. type 1 after the first command and confirm
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
```
![image](https://user-images.githubusercontent.com/101191449/189370229-0090379c-3238-4972-902b-89a008c75368.png)

## we check the rust version.
```
rustc --version
```
![image](https://user-images.githubusercontent.com/101191449/189370417-c1a6ec34-73af-4b34-a872-b2624e1b40db.png)

## We clone zeeka's github file from the zeeka-network repository to our server and install the binary.
```
git clone https://github.com/zeeka-network/bazuka
cd ~/bazuka
cargo install --path .
```
## We are doing the initialize operation. We remove the parenthesis and enter the name we want where it says [your seed phrase].
```
bazuka init --seed [your seed phrase] --network debug --node 127.0.0.1:8765
```

## We are creating our Zeeka.service file. At the end of the ExecStart section, we enter our own discord information.
```
IPADDR=$(curl icanhazip.com)
sudo tee <<EOF >/dev/null /etc/systemd/system/zeeka.service
[Unit]
Description=Zeeka node
After=network.target

[Service]
User=$USER
ExecStart=/root/.cargo/bin/bazuka node --listen 0.0.0.0:8765 --external $IPADDR:8765 --network debug --db ~/.bazuka-debug --bootstrap 152.228.155.120:8765 --bootstrap 95.182.120.179:8765 --bootstrap 195.2.80.120:8765 --bootstrap 195.54.41.148:8765 --bootstrap 65.108.244.233:8765 --bootstrap 195.54.41.130:8765 --bootstrap 185.213.25.229:8765 --bootstrap 195.54.41.115:8765 --bootstrap 62.171.188.69:8765 --bootstrap 49.12.229.140:8765 --bootstrap 213.202.238.77:8765 --bootstrap 5.161.152.123:8765 --bootstrap 65.108.146.132:8765 --bootstrap 65.108.250.158:8765 --bootstrap 195.2.73.130:8765 --bootstrap 188.34.167.3:8765 --bootstrap 188.34.166.77:8765 --bootstrap 45.88.106.199:8765 --bootstrap 79.143.188.183:8765 --bootstrap 62.171.171.11:8765 --bootstrap 65.108.201.41:8765 --bootstrap 159.203.176.252:8765 --bootstrap 194.163.191.80:8765 --bootstrap 146.19.207.4:8765 --bootstrap 135.181.43.174:8765 --bootstrap 95.111.234.205:8765 --bootstrap 192.241.131.113:8765 --bootstrap 45.67.217.16:8765 --bootstrap 65.108.157.67:8765 --bootstrap 65.108.251.175:8765 --bootstrap 95.216.204.235:8765 --bootstrap 45.82.178.159:8765 --bootstrap 161.97.111.145:8765 --bootstrap 149.102.133.130:8765 --bootstrap 65.108.61.32:8765 --bootstrap 95.216.204.32:8765 --bootstrap 188.34.160.74:8765 --bootstrap 185.245.183.246:8765 --bootstrap 213.246.39.14:8765 --discord-handle "Tharkunas#4691"
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```

## we are starting our service.
```
sudo systemctl daemon-reload
sudo systemctl enable zeeka
sudo systemctl restart zeeka
```

## Log control command
```
journalctl -u zeeka -f -o cat
```

# Bazuka Miner Installation guide



# System requirements
```
OS : Linux
CPU: 12-16 vcpu (AMD Ryzen 9 16-core)
Ram: 32GB ram
Disk : Minimum 32GB
GPU: 2080Ti card
```

