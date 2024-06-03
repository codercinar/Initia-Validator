# Initia-Validator


<h1 align="center"> PROJECT INITIA</h1>

<p align="center">
  <img src="initia logo" alt="Project Logo">
</p>

<p align="center">
  <a href="https://t.me/corenodechat">Community Channel</a> | 
  <a href="https://twitter.com/corenodeHQ">Community Twitter</a> | 
  <a href="https://discord.com/invite/0glabs">Discord</a> | 
  <a href="https://twitter.com/xbonds">Twitter</a> | 
  <a href="https://discord.gg/initia">Initia Discord</a>
</p>

## 🔗 Links

- **FAUCET**: [faucet.testnet.initia.xyz](https://faucet.testnet.initia.xyz/)
- **Explorer**: [scan.testnet.initia.xyz/initiation-1](https://scan.testnet.initia.xyz/initiation-1)

## 💻 System Requirements
| Component | Minimum Requirements | 
| --------- | -------------------- |
| CPU       | 6 Cores              |
| RAM       | 16+ GB               |
| Storage   | 400 GB SSD           |
| System    | Ubuntu 22.04 OR 20.04|

## 🚧 Necessary Installations
\`\`\`bash
sudo apt update && sudo apt install curl git jq build-essential gcc unzip wget lz4 -y
\`\`\`

## 🚧 Go Installation
\`\`\`bash
ver="1.22.0" && wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && rm "go$ver.linux-amd64.tar.gz" && echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> $HOME/.bash_profile && source $HOME/.bash_profile && go version
\`\`\`

## 🚧 Binary Files
\`\`\`bash
git clone https://github.com/initia-labs/initia
cd initia
git checkout v0.2.15
make build
\`\`\`

## 🚧 Your Variables
\`\`\`bash
echo 'export MONIKER="YOUR_MONIKER"' >> ~/.bash_profile
echo 'export CHAIN_ID="initiation-1"' >> ~/.bash_profile
echo 'export WALLET="wallet"' >> ~/.bash_profile 
source $HOME/.bash_profile
\`\`\`

## 🚧 Node init
cd $HOME
initiad init $MONIKER --chain-id $CHAIN_ID
\`\`\`

## 🚧 Genesis and Addrbook Files - I used blacknodes files for this
\`\`\`bash
wget -O genesis.json https://files2.blacknodes.net/initiatestnet/genesis.json --inet4-only
mv genesis.json $HOME/.initia/config/
wget -O addrbook.json https://files2.blacknodes.net/initiatestnet/addrbook.json --inet4-only
mv addrbook.json $HOME/.initia/config/
\`\`\`

## 🚧 Live Peers - I used blacknodes peers
peers=$(curl -s https://services.blacknodes.net/Initia-Testnet/data/peers.txt)
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.initia/config/config.toml
\`\`\`

## 🚧 Download Snap & Sync
> NOTE: Replace snap url with latest snaps you find when you setup your validator. You can search in latest snaps in discord validator channel.
\`\`\`bash
sudo apt-get install wget liblz4-tool aria2 -y
aria2c -x5 -s4 https://files3.blacknodes.net/initiatestnet/initiation-1_679476.tar.lz4
lz4 -c -d initiation-1_679476.tar.lz4 | tar -x -C $HOME/.initia/data
\`\`\`

## 🚧 Genesis and Addrbook
\`\`\`bash
sudo tee /etc/systemd/system/initiad.service > /dev/null <<EOF
[Unit]
Description=Initia Node
After=network.target

[Service]
User=$USER
Type=simple
ExecStart=$(which initiad) start --home $HOME/.initia
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
\`\`\`

## 🚧 Enable Service & Start The Node
\`\`\`bash
sudo systemctl daemon-reload
sudo systemctl enable initiad.service
sudo systemctl restart initiad.service
sudo journalctl -u initiad.service -f -o cat
\`\`\`

Validator Setup

## 🚧 Seed Nodes
\`\`\`bash
Will be add
\`\`\`
