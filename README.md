git clone https://github.com/masternodes/vps.git && cd vps

cp -r new_coin_template seraph
cd seraph

nano coin.env
# nano /root/vps/config/seraph/seraph.env

CODENAME=seraph
MNODE_DAEMON=${MNODE_DAEMON:-/usr/local/bin/seraphd}
MNODE_INBOUND_PORT=${MNODE_INBOUND_PORT:-25676}
GIT_URL=https://github.com/seraphcoin/seraph.git
SCVERSION="tags/Ubuntu16.04_V3.1.1"
NETWORK_BASE_TAG="2018"

mv coin.compile seraph.compile
mv coin.conf seraph.conf 
mv coin.env seraph.env 

cd /root/vps
mv seraph config

./install.sh -p seraph -c 5

nano /etc/masternodes/seraph_n1.conf

/usr/local/bin/activate_masternodes_seraph

/usr/local/bin/seraph-cli -conf=/etc/masternodes/seraph_n1.conf getinfo
/usr/local/bin/seraph-cli -conf=/etc/masternodes/seraph_n1.conf mnsync status

nano /tmp/seraph_masternode.conf


ON YOUR COLD WALLET:
1. Create new address label SeraphMN1
2. Send 5000 SERA to new created address
3. Go to your GUI Wallet and open Help > Debug window > Console tab Enter command "masternode genkey" to console and save somewhere your mnprivatekey
4. Wait 15 confirms go to your GUI Wallet and open Help > Debug window > Console tab Enter command "masternode outputs" to console and save somewhere your mnoutputs and index
5. open masternode.conf  Paste this (change IP - you IP ,YOURKEY is mnprivatekey ,mnoutputs and index)
SeraphMN1 IP:25676 YOURKEY MNOUTPUTS OUTPUTINDEX
6. Restart win wallet
7. Debug window > Console "startmasternode alias false SeraphMN1"

/usr/local/bin/activate_masternodes_seraph
/usr/local/bin/seraph-cli -conf=/etc/masternodes/seraph_n1.conf masternode status
