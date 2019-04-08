.. _user_local_setup:

Local Setup
===========

In some cases you would want to start a local network for testing and development purposes.


Starting a new network
----------------------

To start a new Beam Network follow the steps below:

1. Download or build Beam binaries for node and CLI wallet

From this point the folders containing node and wallet binaries will be called 'node folder' and 'wallet folder' respectively

2. Initialize new wallet by running the following command in the wallet folder:

::

	./beam-wallet init

See :ref:`creating_new_cli_wallet` for more details

3. Export miner key, by running the following command in the wallet folder:

::

	./beam-wallet export_miner_key --subkey=1

.. note:: If you are running more than one mining node repeat step 3 with --subkey=N (where N is the id of the mining nodes 1,2,3...)

4. Export owner key by running the following command in the wallet folder:

::

	./beam-wallet export_owner_key

5. Locate sample Beam treasury file treasury.bin (it is located in the root of Beam source folder) and copy it to the same folder as beam-node binary.


6. Launch the first node using the following command:

::

	./beam-node --mining_threads=1 --treasury_path=treasury.bin --owner_key=<owner key> --miner_key=<miner key> --pass=<wallet password>

Sample output printed by the node to the console (and in the logs) should look like this:

::

	I 2018-12-25.09:43:56.712 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-25.09:43:56.925 starting a node on 10000 port...
	I 2018-12-25.09:43:56.930 Treasury size: 584661
	I 2018-12-25.09:43:56.955 Node ID=a82306ff757cca58
	I 2018-12-25.09:43:56.955 Initial Tip: 0-0000000000000000
	I 2018-12-25.09:43:56.955 Sync mode
	I 2018-12-25.09:43:56.955 Searching for the best peer...
	I 2018-12-25.09:43:56.959 GenerateNewBlock: size of block = 294; amount of tx = 0
	I 2018-12-25.09:43:56.960 Block generated: Height=1, Fee=0, Difficulty=02-000000(4), Size=294
	I 2018-12-25.09:43:56.960 Mining nonce = 428dcf03b88fa57d

As new blocks are mined, the console will indicate this as follows:

::

	I 2018-12-25.09:46:00.513 New block mined: 1-a690c8aa7e14225c
	I 2018-12-25.09:46:00.520 1-a690c8aa7e14225c Header accepted
	I 2018-12-25.09:46:00.520 1-a690c8aa7e14225c Block received
	I 2018-12-25.09:46:00.523 1-a690c8aa7e14225c Block interpreted. Fwd=1
	I 2018-12-25.09:46:00.524 My Tip: 1-a690c8aa7e14225c, Work = 4
	I 2018-12-25.09:46:00.527 GenerateNewBlock: size of block = 294; amount of tx = 0
	I 2018-12-25.09:46:00.527 Block generated: Height=2, Fee=0, Difficulty=02-000000(4), Size=294
	I 2018-12-25.09:46:00.528 Mining nonce = 32d6ce8dba24d0dd


.. note:: For GPU mining, add --miner_type=gpu parameter

7. Launch additional nodes

To launch more mining nodes either for the same wallet or different ones, just repeat the relevant portions of steps 1 through 6. For validating nodes set mining_threads parameter to 0. 

In addition add --peer=<ip:port of the first node> to connect new nodes to the first node, thus extending the network

.. attention:: Beam Nodes have automatic discovery mechanism that will find and automatically connect to the other running nodes on the local network. If you do not want the networks to mix, just change any of the  :ref:`consensus rules` to intentionally break compatibility between the networks and avoid unwanted behavior. The simplest way to achieve this is to set 'Prehistoric' parameter to a random hash value, i.e Prehistoric=1234
