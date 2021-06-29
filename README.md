# Unit 18 - Proof of Authority Blockchain

This is a guide to setting up a Proof of Authority(PoA) consensys algorithm on the Ethereum testnet.

## Required Installations

### 1. MyCrypto App
MyCrypto allows you to manage Ethereum based tokens & send/receive transactions on the blockchain. Download MyCrypto open this link in your browser https://download.mycrypto.com/ and follow the installation instructions.

### 2. Go Ethereum Tools
Go Ethereum Tools will be used to create a blockchain, from the genesis block to mining tokens and making transactions. To download GoEthereum go to https://geth.ethereum.org/downloads/ scroll down to stable release and download Geth & Tools.

## Creating the Blockchain

**Step 1: Open Gitbash or terminal (for mac users)**
- navigate to the folder where you downloaded the Go Ethereum Tools.

**Step 2: Generating 2 nodes using the following commands in GitBash**

For Node1:
`./geth --datadir node1 account new`
- you will be prompted to enter a password and repeat it.
- also a public address key & a secret file key will be given to you. Save them into a txt document for later.

For Node2:
`./geth --datadir node2 account new`
- you will be prompted again for a password.
- save the public and secret keys given for node 2 to the txt document as well.

Here is a snip for reference
![](/Screenshots/1_Node1_Node2_creation.PNG)

**Step 3: Configuration of Genesis block**
- using GitBash run the code 
`./puppeth`
- give your network a name - (I choose 'neweth')
- enter the number corresponding to: *Configure new genesis*
- enter the number corresponding to: *Create new genesis from scratch*
- enter the number corresponding to: *Clique - proof-of-authority*
- select your choice of seconds each block takes (I left as default: just hit enter).
- paste node 1 account address that you saved from ealier into list of account to seal, then paste the node 2 account address as well.
- again paste both account addresses for nodes 1 & 2 into list of accounts to pre-fund. 
- enter yes or no for pre-funding the pre-compiled accounts (I went with no).

Here is a screenshot for reference
![](/Screenshots/2_Genesis_Config.PNG)

- enter a chain ID, it can be any random number that is at least 3 digit in length. (I chose 353)
- enter the number corresponding to: *Manage existing genesis*
- enter the number corresponding to: *Export genesis configurations*

Here is a screenshot for reference 
![](/Screenshots/3_Manage_Genesis.PNG)

**Step 4: Initializing nodes**
- using the following commands to initialize node 1 & 2.
`./geth --datadir node1 init yournetworkname.json`
`./geth --datadir node2 init yournetworkname.json`

Here is a screenshot to initialize both Node1 and Node2 for reference:
Node1:
![](/Screenshots/4_Initialize_Node1.PNG)
Node2:
![](/Screenshots/4_Initialize_Node2.PNG)

**Step 5: Begin minning blocks**
- using the following command for node 1.
`./geth --datadir node1 --unlock "Your Node 1 Public Address Here" --mine --rpc --syncmode "full" --snapshot=false --allow-insecure-unlock`
- you will be prompted to enter your password that you created earlier in step 2 and press enter, do not worry if you cant see it.

Here is a screenshot for reference:
Node1:
![](/Screenshots/5_Node1_Mine.PNG)
Node2:
![](/Screenshots/5_Node2_Mine.PNG)

- open a new Gitbash/terminal and change directories to the one the Go Ethereum Tools saved to.
- using the following command for node 2.

**-NOTE: you need to use your own Node 2 Public Address and enode address from node 1**

`./geth --datadir node2 --unlock "Your Node 2 Public Address Here" --mine --port 30304 --bootnodes "enode://of your Node 1" --ipcdisable --allow-insecure-unlock1`
- again you will be prompted to enter the password you created from step 2 and press enter.


**Step 6: Adding the blockchain to MyCrypto for testing**
- open MyCrypto and click Change Network at the bottom left, the select Add Custom Node on the left hand side.
- in the pop-up enter the name of your network from step 3 in the *Node Name* and *Network Name* fields.
- select custom from the *Network* dropdown menu.
- for currency enter *ETH*.
- in the *Chain ID* field enter the chain id you selected earlier in step 3.
- use *http:/127.0.0.1:8545* for the URL then hit Save & Use Custom Node.

Here is a screenshot for reference:
![](/Screenshots/6_Setup_Custom_Node.PNG)

**Step 7: Testing the custom network**
- restart the MyCrypto app and change your network to the custom one that was just created.
- select the *View & Send* tab on the left then at the bottom of the screen select the *Keystore File*.
- on this screen click on Select Wallet File and navigate to the to your Node 1 directory selecting the UTC file which is located there.
- you will be prompted to enter your password and click unlock.
- in the *To Address* box paste the account addrress from Node 2, and fill an arbitrary amount of ETH (I chose 271828). then *Send Transaction*

Here is a screenshot for reference
![](/Screenshots/7_TX_Init.PNG)

The transaction will be Pending until confirm on the next block:
Here is a screenshot for reference
![](/Screenshots/8_TX_Pending.PNG)


- on the left hand side of the MyCrypto app hit the *TX Status* tab and confirm the logout.
- you can see if the transaction was successful or not

Here is a screenshot for reference
![](/Screenshots/9_TX_Status.PNG)

The transfer should be complete and Status should be change to "SUCCESSFUL".


