# ETH_PoA_Testnet
## Overview
- Create your own blockchain using GETH and Puppeth and send test transactions via MyCrypto application
### Steps
1.Create accounts for two nodes for the network with a separate datadir for each using geth.
- ./geth --datadir node1 account new
- ./geth --datadir node2 account new
2.Next, generate your genesis block.
- Run puppeth, name your network, and select the option to configure a new genesis block.
- Choose the Clique (Proof of Authority) consensus algorithm.
- Paste both account addresses from the first step one at a time into the list of accounts to seal.
- Paste them again in the list of accounts to pre-fund. There are no block rewards in PoA, so you'll need to pre-fund.
- You can choose no for pre-funding the pre-compiled accounts (0x1 .. 0xff) with wei. This keeps the genesis cleaner.
- Complete the rest of the prompts, and when you are back at the main menu, choose the "Manage existing genesis" option.
- Export genesis configurations. This will fail to create two of the files, but you only need networkname.json.
3. With the genesis block creation completed, we will now initialize the nodes with the genesis' json file.
- Using geth, initialize each node with the new networkname.json.
- ./geth --datadir node1 init networkname.json
- ./geth --datadir node2 init networkname.json
4. Now the nodes can be used to begin mining blocks.
- Run the nodes in separate terminal windows with the commands:
- ./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock
- ./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock
5. Your private PoA blockchain should now run!
6. Create a MyCrypto custom node using the chain id inputed during configuration.
7. Send test transaction from one node on your private network to the other. 

#### NOTES
Wasn't able to connect to the MyCrypto custom network. Initially after creating the network I wasn't able to connect to it at all. The following day it was connecting me to the network but the account balance would be stuck loading.
