# AZTEC-SEQUENCER NODE

Aztec is a L2 protcol on Ethereum that provides privacy and enable private transanction onchain.
Details Guide on how to  Run `Sequencer Node` on Aztec Network Testnet, Earn `Apprentice` Role on discord and Produce blocks on the network.

* **What does sequencer nodes does  in the testnet?**
  * `Sequencer Nodes` proposes blocks, validates blocks from others, and votes on upgrades.
 

## Roles Info

## Hardware Requirements
* **Sequencer Node**: Minimum  of 8 cores CPU, 16GB RAM, 100GB+ SSD (Most Vps will return 132 error, best exprience is gotten from Baremetal servers)

---

**Windows Users** 
For windows 10+ and above, Open your cmd and type `wsl.exe` , it should take you to your window subsytem where the commands below will work fine or just download ubuntu if you don't have wsl ready.

# Install All Require Dependecies

```
sudo apt-get update && sudo apt-get upgrade -y
```

* Install Node.js 

```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && sudo apt update && sudo apt install -y nodejs
```

* Other Packages

```
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen ufw -y
```


# Install Docker & Docker Compose


```
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```
sudo apt update && sudo apt install -y docker-ce && sudo systemctl enable --now docker
```

```
sudo usermod -aG docker $USER && newgrp docker
```


```
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose
```


*  Verify installation

```
docker --version && docker-compose --version
```



# Install the Aztec CLI

```
bash -i <(curl -s https://install.aztec.network)
```


* Lets Config it to your corrent Shell/Path

```
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc
```

```
source ~/.bashrc
```

* Verify the Installation with-

```
aztec -h
```


* Set the correct version for the testnet

```
aztec-up alpha-testnet
```


# Load your wallet with Sepolia Faucet 

https://sepolia-faucet.pk910.de/

https://www.alchemy.com/faucets/ethereum-sepolia



# Allow Incoming connections on Ports 

```
sudo ufw allow 22
sudo ufw allow ssh
sudo ufw enable
```

```
sudo ufw allow 40400
sudo ufw allow 8080
```

## Obtain RPC URLs (Please note: Incase of any warning by Phantom/Metamask while opening the below rpc urls, simply ignore and proceed forward as all the mentioned RPC urls are totally safe.)

*  Beacon + Sepolia Rpc + Other Network Endpoint 👇

• Rockx : https://tinyurl.com/ad9yp4ws

• BlockPi : https://tinyurl.com/mt396mx8

• Drpc : https://tinyurl.com/4wjxk2d8

• Ankr : https://tinyurl.com/2y4aw9ct

• Tenderly : https://tinyurl.com/46duvbhe

• Chainstack : https://tinyurl.com/dkwvmaas

Sepolia Rpc + Other Network Endpoint👇

• Alchemy : https://tinyurl.com/ryabsbwd

• Nodereal : https://tinyurl.com/3a6yb4jn

• Metamask : https://tinyurl.com/4d7h36m3

• Blast :  https://tinyurl.com/yn9tmvfz

• Getblock :  https://tinyurl.com/uuuv7t9p

## Generate Ethereum Keys (You can use your metamask to create a new wallet and use here)
Get an EVM Wallet with `Private Key` and `Public Address` saved.

## Get Sepolia ETH
Fund your Ethereum Wallet with `ETH Sepolia`
you can get sepolia eth from alchemy `https://www.alchemy.com/faucets/ethereum-sepolia`


<div  align="center">
   
#  Start Your Sequencer 🍥

</div>

* Create a Screen Session

```
screen -S aztec
```

  🔺🔺--- Execute below given command to Start Your node & Dont forget to make changes in it, now here is the catch, we will use multipacked RPC urls here so that in case one RPCs failed other RPCs work as a backup and which keep the nodes running.

```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls 'https://lb.drpc.org/ogrpc?network=sepolia&dkey=[API_KEY],https://sepolia-eth.w3node.com/[HASH]/api,https://eth-sepolia.blastapi.io/[API_KEY],https://eth-sepolia.g.alchemy.com/v2/[API_KEY],https://ethereum-sepolia.core.chainstack.com/beacon/[API_KEY],https://eth-sepolia.nodereal.io/v1/[API_KEY]' \
  --l1-consensus-host-urls 'https://sepolia-beacon.w3node.com/[HASH]/api,https://lb.drpc.org/rest/[API_KEY]/eth-beacon-chain-sepolia,https://ethereum-sepolia-beacon.blockpi.network/rpc/v1/[API_KEY]' \
  --sequencer.validatorPrivateKey [VALIDATOR_PRIVATE_KEY] \
  --sequencer.coinbase [ADDRESS] \
  --p2p.p2pIp [PUBLIC_IP] \
  --p2p.maxTxPoolSize 1000000000 \ 
  --sequencer.governanceProposerPayload 0x54F7fe24E349993b363A5Fa1bccdAe2589D5E5Ef
```

* Replace `[API_KEY] and [HASH]` with your actual one which you get once you signup with your gmail Ids, You need to login/signup with your gmail Ids in above given RPC urls and select eth sepolia and beacon chains to get your API Key.


* 👇👇For Example: Once you setup ur above command with multipacked RPCs your final command should look like this..(DONT COPY THIS 👇, AS ITS JUST FOR REFERENCE)👇👇

```
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls 'https://lb.drpc.org/ogrpc?network=sepolia&dkey=Aq78CYyrerer--uuNuIR8KmrbrRhIxXF,https://sepolia-eth.w3node.com/1fc8gdgttrtretgdgdabcb/api,https://frosty-damp-vineyard.ethereum-sepolia.quiknode.pro/a57bb2fghfhfghfh78c,https://eth-sepolia.blastapi.io/06e8f36c-9fhjg1b-4323-a3fffc5-ee27gggd2d89e24,https://eth-sepolia.g.alchemy.com/v2/tPYgggfpQFLxO5UFTJ-DWYYMncyFpYffwL2sha,https://ethereum-sepolia.core.chainstack.com/beacon/c07e43adb9ff3abcecef8d5198842f5cdf,https://eth-sepolia.nodereal.io/v1/2f9380ff72b1e7lkjjj6bbfd868e5564fa' \
  --l1-consensus-host-urls 'https://sepolia-beacon.w3node.com/3dc168631a62aa42ffff20ab18ajhhh5f0665532a2cabaaeefc6d50c/api,https://lb.drpc.org/rest/Aq78CYMMggghjhjhsrxF_5uB_-x5_4Ed9NuIRffff8KmrbrRhIxXF/eth-beacon-chain-sepolia,https://ethereum-sepolia-beacon.blockpi.network/rpc/v1/fff20sdsdsdsdsdsdsdab18ajhhh5f0665532a2c' \
  --sequencer.validatorPrivateKey 0x1826...........1feca832a \
  --sequencer.coinbase 0x3fC.......8997647 \
  --p2p.p2pIp 34......43 \
  --p2p.maxTxPoolSize 1000000000 \ 
--sequencer.governanceProposerPayload 0x54F7fe24E349993b363A5Fa1bccdAe2589D5E5Ef

```

* Replace `0xYourPrivateKey` with your actual EVM wallet pvt key    🔺 (dont forget to add 0x at starting)

* Replace `YourAddress` with your actual evm wallet address

* Replace `Your_ip` with your `VPS External IP`  ... 

     -U can get External IP by running  `curl ifconfig.me`


* It will take sometime(4-5 hrs) to download and Sync! 🥶


![Screenshot 2025-05-02 164041](https://github.com/user-attachments/assets/17dd3df2-3136-4dd0-8dde-70cf19291503)


* The Successfull Running Should Look like this 👇

  ```
  Downloaded L2 block 10032 {"blockHash":"0x09b279299f438717fbfecfe13d107f6163426b7c8d171d5ebb315a302fd7a257","blockNumber":10036,"txCount":0,"globalVariables":{"chainId":11155111,"version":4189337207,"blockNumber":10036,"slotNumber":13555,"timestamp":1748418684,"coinbase":"0xaa6a270b83acc94f1871b763b2899c6bd084d52a","feeRecipient":"0x0000000000000000000000000000000000000000000000000000000000000000","feePerDaGas":0,"feePerL2Gas":3420},"archiveRoot":"0x0fb65295d5466158df7798c08f5f5787e4c23552a41ce5d049f9313ab4d40db4","archiveNextLeafIndex":10037}
  ```
  
![Screenshot 2025-05-28 131915](https://github.com/user-attachments/assets/17bdcd0a-871b-4b51-9477-5d9443d097b2)

Please note: Once your node is up and running to verify whether it got fully synced or not and downloading latest blocks or not you can check your block number, for ex: here its 10032 with block number shown here - https://aztecscan.xyz/blocks



#######################################################

* 😱😱 Very Imp update about aztec node run ( for Users - Only if you are running your node in Google cloud VPS, if not then you can ignore the below steps ) 

----  START -----
•  Google cloud console link : https://console.cloud.google.com/compute/instances

•  Web Link (aztec explorer) : https://aztec.nethermind.io/

•  Find Peer id: (Copy below command and execute it in your VPS after deattaching your VPS screen)
```
sudo docker logs $(docker ps -q --filter ancestor=aztecprotocol/aztec:alpha-testnet | head -n 1) 2>&1 | grep -i "peerId" | grep -o '"peerId":"[^"]*"' | cut -d'"' -f4 | head -n 1
```

•  Add This + allow port (as per video): 0.0.0.0/0

*  For more details - check this aztec discord official link - https://discord.com/channels/1144692727120937080/1366896687800389734/1374428506288689383

---- END-----

#########################################################

# Detached and Attached From the Screen

* For detached from screen session - `ctrl` , `a` + `d`

* For Attach - 

```
screen -r aztec
```

<div  align="center">
   
# Get Apprentice Role In dc- 😙

</div>


📋 **Step 1: Get the latest proven block number**

```
curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' \
http://localhost:8080 | jq -r ".result.proven.number"
```

* Save this block number for the next steps

* Example output: `12345`

🔍 **Step 2: Generate your sync proof**

```
curl -s -X POST -H 'Content-Type: application/json' \
-d '{"jsonrpc":"2.0","method":"node_getArchiveSiblingPath","params":["BLOCK_NUMBER","BLOCK_NUMBER"],"id":67}' \
http://localhost:8080 | jq -r ".result"
```

* Replace both `BLOCK_NUMBER` with your: (check step1)

* This will output a long base64-encoded string - (Copy it completely)


✅ **Step 3: Register with Discord**


* join dc- https://discord.gg/aztec 

* Go to `#operators│start-here` Channel

* Type `/operator start` 

![image](https://github.com/user-attachments/assets/bb4985b0-f98a-43ed-b0c1-9f7e95f6de3c)

* Now it will promt u to enter `address` , `block number` , `proof`

* Place your evm wallet address in `address` section

* Place block-number From the `Step-1` 

* Place sync Proof from `Step-2` 


* Success message should look like this! & U will get the role!

![Screenshot 2025-05-02 180049](https://github.com/user-attachments/assets/cb25480d-01ae-45d7-9017-c269e2cc54a6)

KEEP YOUR NODE RUNNING, YOU WILL GET GUARDIAN ROLE ONCE THE TEAM TAKES SNAPSHOT. I ALREADY GRABBED GUARDIAN ROLE IN ALL MY 3 Accounts.

![-16249-Discord-operators│start-here-Aztec-Network-05-27-2025_11_23_PM](https://github.com/user-attachments/assets/9519cc2c-b94c-4aba-8b11-d3cfb217fbb3)

![-19677-Discord-operators│start-here-Aztec-Network-05-27-2025_11_25_PM](https://github.com/user-attachments/assets/7740ca2b-349f-40c3-aa2f-7016e45e6011)

![-2947-Discord-operators│start-here-Aztec-Network-05-27-2025_11_27_PM](https://github.com/user-attachments/assets/dbf019ba-ccb0-4be0-a59c-ff4116a4d99b)


This Readme will keep getting updated here and on my X https://x.com/ChetnaRai18


