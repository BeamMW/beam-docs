.. _user_cli_wallet_guide:

Command Line User Guide
=======================

The purpose of this document is to describe the process of setting up BEAM node and command line wallet. 

Getting Started
---------------

Beam software runs on all operating systems: Linux, Mac OS and Windows. Before you start please verify that your operating system is supported by reviewing the :ref: `user_supported_platforms`.

All examples in this section are formatted for Linux / Mac platforms. If you are using Windows please substitute ./beam-wallet with beam-wallet.exe and run your commands using Windows Command Prompt.

Creating new wallet
-----------------------

In order to create new wallet run:

::

	./beam-wallet init

You will be prompted to enter Wallet Password, which is used to protect the wallet database 

.. warning:: Choose strong password for the wallet and keep it secret

   Anyone who knows your wallet password and will have access to your machine will be able to spend your coins and will have access to all metadata store in the wallet, including transaction history.

Sample output for this operation will look something like this:

::
	 $ beam-wallet.exe init
	 I 2018-12-23.15:24:29.461 Rules signature: ddccf5d8d0f77bd2
	 I 2018-12-23.15:24:29.462 starting a wallet...
	 Enter password: ****************
	 I 2018-12-23.15:24:32.524 Generating wallet phrase...
	 
	 Generated wallet phrase:
	 
	         despair;evoke;airport;seven;cricket;menu;current;ankle;require;monkey;maple;crawl;
	 
	         IMPORTANT
	 
	         Your recovery phrase is the access key to all the cryptocurrencies in your wallet.
	         Print or write down the phrase to keep it in a safe or in a locked vault.
	         Without the phrase you will not be able to recover your money.
	 
	 I 2018-12-23.15:24:32.728 wallet successfully created...
	 I 2018-12-23.15:24:32.750 New address generated:
	 
	 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956
	 
	 I 2018-12-23.15:24:32.750 label = default


The Rules signature is a hash of current node configuration which is used to determine compatibility between different versions of nodes and wallets. 

Generated wallet phrase is the Seed Phrase (see :ref:`seed phrase`). 

.. warning:: Copy the seed phrase to a secure location and keep it safe. 

   Seed phrase is the most important secret you need to keep to protect your coins. Anyone knowing the seed phrase will be able to control all your coints regardless of any other infomation. Always generate new wallet you intend to use on a secure air gapped machine in a private environment and keep the wallet phrase safe and secret.


The following line indicates that a new temporary SBBS address has been generated (see :ref:`sbbs`). This address is valid for the next 24 hours and can be used to recive coins. To generate new addresses see 'Creating new receive address' section below.

After wallet initialization is complete a wallet.db file is created in the same folder. This is the wallet database file which is encrypted with the Wallet Password and contains transaction history, keys and all the rest of the metadata. If this file is deleted or lost, for any reason, you can always restore your coins using the Seed Phrase, however you will lose all transaction history and any additional metadata store in the wallet database. To understand how to backup and restore the wallet.db file please check the :ref:`backup and restore` page.

In addition to the wallet.db file, you will see `logs` folder. A new log file is created every time you run the CLI wallet. Please attach logs to any supports requests you might send. See `Reporting Issues and Getting Support`_ section, for more details.


Restore CLI wallet from Seed Phrase
-------------------------------

It is only possible to restore your coins by running your own node with your *owner key*

This process involves several steps

First you need to recreate your wallet using your `seed phrase`_ by running the following command: 

::

	./beam-wallet restore --wallet_phrase=<semicolod separated list of 12 seed phrase words>;

Now you need to export the owner key by running:

::

	./beam-wallet export_owner_key

(see `Exporting owner key` for more details)

Then you need to run your own node, providing the owner key as a parameter as follows:

::

	./beam-node --peer=<ip and port of peer node> --key_owner=<owner key exported from the wallet> 

Once the node has synchronized, you need to connect your wallet to the node to update the wallet database.

To do that run the following command:

::

	./beam-wallet listen -n <ip and port of your node, ex:127.0.0.1:10000>

After wallet syncrhonizes, use `info` command to check wallet status

:: 
	./beam-wallet info

Exporting miner key
-------------------

To generate a secret key used by the miner to attribute mining rewards to your wallet run the following command:

::

	./beam-wallet export_miner_key --subkey=<integer miner id, i.e 1,2,3...>

You will be prompted for the wallet password

The sample output for this command should look like this:

::

	$ beam-wallet.exe  export_miner_key --subkey=1
	I 2018-12-23.16:36:04.306 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-23.16:36:04.307 starting a wallet...
	Enter password: *******************
	Secret Subkey 1: OVBSdWQlOV3WuC6bLXRDJqyDfdxWSuzdA4jEGRAZ1zhy4gA3/KcBTEdcmN5wNOv0vQrBWwOlTdIxqyPFzFDFdaVYZPUDoXjqgUE=

It is important to keep the Miner Key secret since anyone who knows the miner key will be able to spend all rewards mined by that miner.

Exporting owner key
-------------------

The purpose of the Owner key is to allow all nodes mining for you to be aware of all mining rewards mined by other nodes so that you would only need to connect to one node to collect all rewards into your wallet. While in most other cryptocurrencies this is done by simply mining to a single address you control, in Mimblewimble it is not as simple since there are no addresses and the mining rewards should be coded with unique blinding factors which are deterministically derived from the Master Key, and then tagged by the single Owner key. 

Owner key should be kept secret. Owner does not allow to spend coins, however it will allow to see all coins mined for you by all miners that use this Owner key.

To export the owner key run the following command:

::

	./beam-wallet export_owner_key

You will be prompted for the wallet password

Sample output for this command should look like this:

::

	$ beam-wallet.exe  export_owner_key
	I 2018-12-23.16:53:04.973 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-23.16:53:04.974 starting a wallet...
	Enter password: *
	Owner Viewer key: dmVxtRCM3BH1VakviSB/XY86DsCKuWDLKk51eLDlibgMeL2fZ317Zdqx3E6oXbKtldqZz/lo5stTCSz9M1bDJdYUF4DG/ZaIuHHszi/H9wDmNDVboUdNtC/1Z/haWr9JxeIDtRSDBN+xpUbv


Receiving beams
---------------

To receive Beams you need to connect to a specific node by running the following command:

::

	./beam-wallet listen -n <node address and port, ex: 127.0.0.1:10000>

You will be prompted for the wallet password

Sample output for this command should look like:

::

	I 2018-12-23.17:07:55.526 Rules signature: ddccf5d8d0f77bd2                                                                        
	I 2018-12-23.17:07:55.527 starting a wallet...                                                                                     
	Enter password: ***************                                                                                                    
	I 2018-12-23.17:07:58.076 wallet sucessfully opened...                                                                             
	I 2018-12-23.17:07:58.078 WalletID 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956 subscribes to BBS channel 20 
	I 2018-12-23.17:07:59.297 Sync up to 8304-2dc4e5a393d6774b                                                                         
	I 2018-12-23.17:07:59.318 Current state is 8304-2dc4e5a393d6774b                                                                   

Once launched, the wallet will listen to updates from the server and any incoming transactions on the advertise SBBS address.

To receive funds you should send the address to the sending party via any available channel (Email, Telegram etc.)

When funds are sent you will see the incoming transaction in wallet logs and on the screen. It should look similar to:

::

	I 2018-12-23.17:55:08.556 [7997ecd5c59e4865a6d938dbf339567e] Receiving 300 beams  (fee: 10 groth )
	I 2018-12-23.17:55:08.608 [7997ecd5c59e4865a6d938dbf339567e] Invitation accepted
	D 2018-12-23.17:55:09.203 Received PeerSig:     596857beae016ebd
	I 2018-12-23.17:55:09.216 [7997ecd5c59e4865a6d938dbf339567e] Transaction kernel: 95a8e48587c452b3
	D 2018-12-23.17:55:09.346 [7997ecd5c59e4865a6d938dbf339567e] has registered
	D 2018-12-23.17:55:09.367 Received PeerSig:     596857beae016ebd
	I 2018-12-23.17:55:09.428 Get proof for kernel: 95a8e48587c452b3

Sending beams
------------------

To send beams you need to run the following command:

::

	./beam-wallet send -n <node address and port, ex: 127.0.0.1:10000> -r <sbbs address> -a <amount, ex: 11.3> -f <feed, ex: 0.2>


The wallet log should look like something like:

::

	$ beam-wallet.exe send -n 172.104.249.212:8101 -r 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956 -a 10
	I 2018-12-23.18:05:49.037 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-23.18:05:49.038 starting a wallet...
	Enter password: *
	I 2018-12-23.18:05:50.725 wallet sucessfully opened...
	I 2018-12-23.18:05:50.726 WalletID 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956 subscribes to BBS channel 20
	I 2018-12-23.18:05:50.775 [b21f08337dd94603bb038c82c1888eac] Sending 10 beams  (fee: 0 groth )
	I 2018-12-23.18:05:50.986 [b21f08337dd94603bb038c82c1888eac] Invitation accepted
	I 2018-12-23.18:05:51.053 [b21f08337dd94603bb038c82c1888eac] Transaction kernel: 71cf20c4c94f25ce


.. admonition:: Sending transactions to yourself

	It is possible, and sometimes necessary to create a transaction to your own SBBS address to split a large UTXO. To do that just issue a send command with required amounts to your own SBBS address. Please note that you will pay the fee for the transaction.


Printing wallet info
---------------------

To print the current status of your wallet, run the following command:

::

	./beam-wallet info

You will be prompted for the wallet password

Sample output from this command should look like this:

::

	I 2018-12-23.17:56:19.368 Rules signature: ddccf5d8d0f77bd2                                                                   
	I 2018-12-23.17:56:19.369 starting a wallet...                                                                                
	Enter password: *                                                                                                             
	I 2018-12-23.17:56:21.144 wallet sucessfully opened...                                                                        
	____Wallet summary____                                                                                                        
	                                                                                                                              
	Current height............8353                                                                                                
	Current state ID..........72329a2efa2ddad4                                                                                    
	                                                                                                                              
	Available.................300 beams                                                                                           
	Maturing..................0 groth                                                                                             
	In progress...............0 groth                                                                                             
	Unavailable...............0 groth                                                                                             
	Available coinbase .......0 groth                                                                                             
	Total coinbase............0 groth                                                                                             
	Avaliable fee.............0 groth                                                                                             
	Total fee.................0 groth                                                                                             
	Total unspent.............300 beams                                                                                           
	                                                                                                                              
	                  id |          Beam |         Groth |        height |          maturity |                  status |    type  
	    1545571472000001             300               0            8347                8351   [Available]                 norm   



Creating new SBBS address
-------------------------

In order to create new SBBS address, run the following command:

::

	./beam-wallet new_addr

You will be prompted for the wallet password

Sample output from this command should look like this:

::

	I 2018-12-23.18:16:44.112 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-23.18:16:44.113 starting a wallet...
	Enter password: *
	I 2018-12-23.18:16:45.392 New address generated:

	646a773da4d4651f35fd75ca958b7859e89d8d8382b8155773bd396e2cc49cca

