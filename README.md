# <h1 align="center">Zeeka-Network-Fullnode-and-Miner</h1>
![image](https://user-images.githubusercontent.com/101191449/189383414-8959a27a-c86a-475e-b255-c8222d173669.png)



# Zeeka Fullnode Manual Installation

This guide uses [LINK](https://github.com/mmc6185/node-testnets/blob/main/zeeka-network/bazuka/fullnode_manuel.md) as a reference.


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

[LINK](https://github.com/mmc6185/node-testnets/blob/main/zeeka-network/bazuka/miner_node.md) is used as a reference in this guide

# System requirements
```
OS : Linux
CPU: 12-16 vcpu (AMD Ryzen 9 16-core)
Ram: 32GB ram
Disk : Minimum 32GB
GPU: 2080Ti card
```

## We are checking the bazuka version. (If you get a `DifferentGenesis` error, it means that the genesis block has changed. In this case, you need to delete the `~/.bazuka-debug` folder and reboot.)
```
cd ~/bazuka
git pull origin master
cargo install --path .
```

## (DifferentGenesis errors) We delete the `~/.bazuka-debug` folder and start it again.
```
rm -rf ~/.bazuka-debug
sudo systemctl restart zeeka
```

## We install MPN Launcher. (`zoro`)
```
git clone https://github.com/zeeka-network/zoro
cd zoro
cargo install --path .
```

## We load the assertion parameters.
* Payment parameters (~700MB): [Link](https://drive.google.com/file/d/1sR-dJlr4W_A0sk37NkZaZm8UncMxqM-0/view?usp=sharing)
* Update parameters (~6GB): [Link](https://drive.google.com/file/d/149tUhC0oXJxsXDnx7vODkOZtIYzC_5HO/view?usp=sharing)

### To download directly using the CLI:
```
sudo apt install curl
```

## We go to the [oauthplayground](https://developers.google.com/oauthplayground/) link.


## We paste and click the `https://www.googleapis.com/auth/drive.readonly` link in the Authorize API Section. Then we authorize with an account.

## Click on Exchange authorization code for tokens. We copy the resulting `access_token` part.

## We paste the access_token that we copied into the access_token part.
```
curl -H "Authorization: Bearer access_token" https://www.googleapis.com/drive/v3/files/1sR-dJlr4W_A0sk37NkZaZm8UncMxqM-0?alt=media -o payment_params.dat
```

## Again we go to [oauthplayground](https://developers.google.com/oauthplayground/).

## We paste and click the `https://www.googleapis.com/auth/drive.readonly` link in the Authorize API Section. Then we authorize with an account.

## Click on Exchange authorization code for tokens. We copy the resulting `access_token` part.

## We paste the access_token that we copied into the access_token part.
```
curl -H "Authorization: Bearer access_token" https://www.googleapis.com/drive/v3/files/149tUhC0oXJxsXDnx7vODkOZtIYzC_5HO?alt=media -o update_params.dat
```
## We are running `zoro` with Node. In the `[executor account]` part, we need to enter a different name than the one we use for the node.
```
zoro --node 127.0.0.1:8765 --seed [executor account] --network debug \
  --update-circuit-params ~/zoro/update_params.dat --payment-circuit-params ~/zoro/payment_params.dat \
  --db ~/.bazuka-debug
```

## After a new block is created, uzi-miner should start working on the PoW puzzle, so you should also run uzi-miner on your system.
* We write the number of threads we will use in the `THREADNUMBER` part.
* 24-32 threads from 12-16vcpu recommended by the team
```
git clone https://github.com/zeeka-network/uzi-miner
cd ~/uzi-miner
cargo install --path .
uzi-miner --node 127.0.0.1:8765 --threads THREADNUMBER
```

## we are creating a zoro service file. In the `[executor account]` part, we enter the name we entered when starting Zoro above.
```
tee /etc/systemd/system/zoro.service > /dev/null <<EOF
[Unit]
Description=Zoro
After=network.target
[Service]
User=root
ExecStart=/root/.cargo/bin/zoro --node 127.0.0.1:8765 --seed '[executor account]' --network debug --update-circuit-params ~/zoro/update_params.dat --payment-circuit-params ~/zoro/payment_params.dat --db ~/.bazuka-debug
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```

## We create uzi-miner service file. In the `THREADNUMBER` section, we enter the number of threads we entered when starting the uzi miner above.
```
tee /etc/systemd/system/uzi.service > /dev/null <<EOF
[Unit]
Description=Uzi
After=network.target
[Service]
User=root
ExecStart=/root/.cargo/bin/uzi-miner --node 127.0.0.1:8765 --threads THREADNUMBER
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```

## we start zoro service.
```
sudo systemctl daemon-reload
sudo systemctl enable zoro
sudo systemctl restart zoro

## we start uzi miner service.
```
sudo systemctl daemon-reload
sudo systemctl enable uzi
sudo systemctl restart uzi
```

## Zero contract Deposit
```
bazuka deposit 
```

## Command to print this message or help of given subcommands
```
bazuka help 
```

## Node running
```
bazuka node Run node
```

## Usual token sending
```
bazuka rsend 
```

## To print the node status:
```
bazuka status 
```

## Zero-contract Token withdraw:
```
bazuka withdraw
```

## sending tokens with zero-transaction

```
bazuka zsend
```



> ## [Web Site](https://zeeka.io/)
> ## [Zeeka Explorer](http://152.228.155.120:8000/)
> ## [Zeeka Discord](https://discord.gg/vWkHJ8QU)

