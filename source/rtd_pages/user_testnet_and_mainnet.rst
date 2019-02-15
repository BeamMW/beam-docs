.. _user_testnet_and_mainnet:


.. _testnet and mainnet:


How to run Testnet and Mainnet on the same machine
==================================================

The following networks exist in Beam realm:
* **Mainnet**: the network with real money and actual transactions.
* **Testnet**: staging environments for trying new features and helping to find the early bugs in our wallet, node, and miner software. For advanced users only.
* **Masternet**: new features in the daily development cycle, if you find yourself on this network it means that you are either very early adopter or Beam code contributor.

Hence, sometimes you wanna play with the new features on Testnet while sending the “real money” over the Mainnet. It’s easy as most features work out-of-the-box and slight visual differentiations such as backgrounds or special messages will always hint whether you are on Mainnet or Testnet. In case you’d like to get a bit deeper into the tech details, here’s what you need to know:

Downloading binaries
--------------------

Mainnet address is https://beam.mw/downloads or https://beam.mw/downloads/mainnet, Testnet address is https://beam.mw/downloads/testnet
Testnet binaries will always include “testnet” in the filename, e.g. *Beam-Wallet-Testnet-x.y.zzz.dmg*

Desktop wallet app and CLI wallet
---------------------------------

* In case desktop wallets run integrated nodes, make sure that they use different ports. By default, the Mainnet node will use 10005 port, while Testnet will use 11005 port. 
* For desktop wallet, the port of the integrated node can be set in the Settings screen.
* Mainnet wallet files and logs are kept in the *Beam Wallet* folder, Testnet wallet files are in *Beam Wallet Testnet* folder by default.
* Desktop wallet and download pages on Testnet will have a dark violet background, Mainnet background will remain the same.

Node
----

* Mainnet node will use 10000 port, while Testnet will use 11000 port by default.
* Mainnet node will reject a connection request from a Testnet wallet, same applies for the Testnet node, rejecting a connection from a Mainnet wallet.

Miner
-----

* Currently, the miner is “just” a pure PoW calculation software. Hence, any Beam miner can work with either Mainnet or Testnet node. When configuring the miner-to-node connection, make sure your miner is connected to the network as intended. 
