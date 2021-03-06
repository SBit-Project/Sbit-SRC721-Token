# SRC721
SRC721 Token Template

# Introduction
This project is an implementation of NFT (non-fungible token) based on [ERC721](https://eips.ethereum.org/EIPS/eip-721) and [OpenZeppelin](https://github.com/OpenZeppelin/openzeppelin-solidity). You can use it to issue your own NFTs and build corresponding DApps on **Sbit**.

You can refer to [this article]() for a detailed description of NFT and ERC721.

# Deployment
## Prerequirements
1. Install the [Solidity compiler](https://solidity.readthedocs.io/en/latest/installing-solidity.html#building-from-source). You'd better install it from a binary package or the source code.
2. Install [Solar](https://github.com/SBit-Project/solar). Solar is a smart contract deployment tool of Sbit.
3. Download this project and install dependencies, like this:
```
git clone https://github.com/SBit-Project/Sbit-SRC721-Token.git
cd Sbit-SRC721-Token
npm install
```

## Deploy SRC721
1. Start a Sbit full node. For example, a testnet Sbit QT node can be started on Mac like follows. Here you'd better specify the user name, password and port for RPC interfaces. Moreover, you should have some Sbit coins in the node for contract gas.
```
$ /Applications/Sbit-Qt.app/Contents/MacOS/Sbit-Qt -testnet -server -rpcuser=user -rpcpassword=sbit -rpcport=22302
```
2. Deploy SRC721 using Solar. This command should be executed under the Sbit-SRC721-Token directory. The RPC parameters of the full node you start above should be specified here. You can replace the term *name* and *symbol* with anything you want.
```
$ solar deploy contracts/SRC721.sol '["name","symbol"]' --sbit_rpc=http://user:sbit@127.0.0.1:22302
exec: solc [contracts/SRC721.sol --combined-json bin,metadata --optimize --allow-paths /Users/sbit/Code/Sbit-SRC721-Token/Sbit-SRC721-Token]
cli gasPrice 40 40
🚀  All contracts confirmed
   deployed contracts/SRC721.sol => 780e2578b08dddc56ca518277a18a2fb6f14da61
```
3. After sucessful deployment, the contract address is shown in the command line. A file named *solar.development.json* is generated under current directory with information about the deployed contract, like the sender address, contract address, ABI and etc.
```
// part of solar.development.json
{
  "contracts": {
    "contracts/SRC721.sol": {
      "source": "contracts/SRC721.sol:SRC721",
      "abi": ...,
      "bin": "...",
      "binhash": "f9f27b8932c3bdfe03975201cbdd43c4058de166e737f044b43f53446d19468e",
      "name": "SRC721",
      "deployName": "contracts/SRC721.sol",
      "address": "780e2578b08dddc56ca518277a18a2fb6f14da61",
      "txid": "45f71bf4d95680e15a4d857e17be2a13aa8f85403a1e624db4151d8cfb98bf5b",
      "createdAt": "2021-11-12T16:21:33.205371334+08:00",
      "confirmed": true,
      "sender": "sK2ha4bbrVusPwDvM243mLg4SAke9RqUrv",
      "senderHex": "1022ba6fa5f2515857a5b226141144b74c3c7d85"
    }
    ...
  }
}
```

## Interact with SRC721
### Using js
See [example/cli](https://github.com/SBit-Project/Sbit-SRC721-Token/tree/master/example/cli).

### Using Sbit QT
1. Mint some SRC721 tokens. 
    1. Choose "Smart Contracts-Send To" in Sbit QT.
    2. Copy the contract address and ABI to the form.
    3. Choose the function *mint* and fill the form with specified "to address" and "token id". (Here the address is in hex format, which you can use the command "fromhexaddress" or "tohexaddress" in "Help-Debug Window-Console" to transfer it from or to a base58 format)
    4. Choose the contract sender address as "Sender Address", since only the contract owner can mint new tokens.
    5. Press "SEND TO CONTRACT" button and wait for the created transaction to be confirmed.

2. Call SRC721 functions.
    1. Choose "Smart Contracts-Call" in Sbit QT.
    2. Copy the contract address and ABI to the form.
    3. Choose any function you want execute and Press "CALL CONTRACT" button. Then you can see the result.

3. Check the contract in the **https://testnet.sbit.dev/contract/780e2578b08dddc56ca518277a18a2fb6f14da61**. You can find the token name, total supply and other information in the page. More information about SRC721 will be supported later when needed.
