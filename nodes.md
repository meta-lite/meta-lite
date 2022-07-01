##Ironfish Commands 


##Celestia Commands
* Additional Peers - https://polkachu.com/testnets/celestia/peers
* Start Node - `sudo systemctl start celestia-bridge && sudo journalctl -u  celestia-bridge.service -f`


AppD Daemon Status - systemctl status celestia-appd

Open Logs - journalctl -u celestia-appd.service -f
Unjail Validator - celestia-appd tx slashing unjail --from=WALLET --chain-id mamaki
Restart App - systemctl restart celestia-appd
Init Bridge - celestia bridge init --core.remote tcp://localhost:26657 --core.grpc tcp://localhost:9090
Kill Appd - sudo pkill -9 celestia-appd
Bridge Logs - celestia-bridge.service -f
Check Sync Status - curl -s localhost:26657/status | jq .result | jq .sync_info
Check Peers - curl -s http://localhost:26657/net_info | jq -r '.result.n_peers'


#Delegate more stake
celestia-appd tx staking delegate \
celestiavaloper1q3v5cugc8cdpud87u4zwy0a74uxkk6u43cv6hd 1000000utia \
    --from=$VALIDATOR_WALLET(redefine this) --chain-id=mamaki

celestia-appd keys add <wallet name>

#Update Celestia App
cd $HOME
rm -rf celestia-app
git clone https://github.com/celestiaorg/celestia-app.git
cd celestia-app
APP_VERSION=$(curl -s https://api.github.com/repos/celestiaorg/celestia-app/releases/latest | jq -r ".tag_name")
git checkout tags/$APP_VERSION -b $APP_VERSION
make install