# waku

sudo apt update && sudo apt upgrade -y
sudo apt-get install build-essential git libpq5 jq -y

# 1. seçenek
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"

sudo apt install docker.io -y
sudo curl -L "https://github.com/docker/compose/releases/download/v2.24.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

git clone https://github.com/waku-org/nwaku-compose
cd nwaku-compose

cp .env.example .env
nano .env

ETH_CLIENT_ADDRESS
ETH_TESTNET_KEY
RLN_RELAY_CRED_PASSWORD

./register_rln.sh

# yes
sudo ufw enable

sudo ufw allow 22    
sudo ufw allow 3000   
sudo ufw allow 8545   
sudo ufw allow 8645   
sudo ufw allow 9005   
sudo ufw allow 30304  
sudo ufw allow 8645

docker-compose up -d

