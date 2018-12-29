.. _user_mining_beam:


.. warning:: The following document is still under construction and is subject to changes



Mining Beam
===========

Alike most cryptocurrencies, Beam relies on miners to add transactions to the blockchain. While all nodes in the Beam network confirm the validity of transactions, Beam counts on miners to take on the massive heavy lifting to guard the network.

Beam is a Mimblewimble implementation. We use classic Proof-of-Work (PoW) consensus.

We welcome everyone to join our mining community to support the network and earn Beam coins.

Mining Algorithm
----------------

To secure the network, Beam uses the `Equihash <https://www.cryptolux.org/index.php/Equihash>`_ proof-of-work mining algorithm). Miners compete against each other using their computing power produce a new block on the chain. The first miner that gets to complete the precise computation for each block is granted with a network standard block reward and any fees for transactions added to that block.

At Mainnet launch, we will use the following Equihash parameters: n=150, k=5. In addition, we will introduce a small change to the datapath to further reduce the chance of zero-day ASICs.

.. note:: Testnet 3 is still using n=144, k=5

The minimal memory requirement for the GPU will be 4 GB. The most up-to-date list of supported GPUs will be available here.


Block Size and Time
-------------------

A Beam block will be generated approximately every minute and contain about 1000 transactions. Block size will be roughly 1MB.

Miner Rewards
-------------

During the first year of Beam existence, miner reward will be 80 coins per block. In years 2-5 the reward will be 40 coins per block. In year 6 the reward will be to 25 coins, and then halving will occur every 4 years until year 129. After year 133, Beam emission will stop.

Mining reward (coinbase UTXO) has 4 hours maturity, meaning that it will be available for spending 4 hours after it was mined.

Treasury
--------

In the first five years of existence, additional coins will be issued to Beam Treasury with each newly mined Beam block.

In the first year, the Treasury will receive additional 20 Beams per block, and in the years 2-5 the Treasury will receive 10 coins per block.

The Treasury will be used to repay Beam investors, Incentivize the Core Team and to support the Beam Foundation (largest single beneficiary of the Treasury).

The distribution of the Treasury Coins is performed on a quarterly basis in the following proportion:

* Investors: 40%
* Core Team: 40%
* Beam Foundation: 20% (Biggest single beneficiary)


ASIC Resistance
---------------

To ensure better decentralization, Beam plans to stay ASIC resistance in the first 12-18 months. To achieve this, we plan to perform one or two hard forks – first after approximately 6 months of existence and another one after approximately 12 months. Each hard fork will change the mining algorithm. The exact modifications will be revealed several weeks before the actual hard fork.

Mininig Guide
-------------

The following section describes how to set up mining for Beam Network

Mining using Desktop Wallet
---------------------------

Our official Desktop Wallet supports both CPU and GPU mining.

.. attention:: Testnet 4 does not support built in GPU miner. It will be added back for Mainnet release

To mine Beam using the Wallet, go to the Settings screen, select “Run Local Node” and set the number of Mining Threads to a value that is greater than zero. Note: the more threads you dedicate to mining, the more strain on your CPU. If you have a supported GPU, turn the “Use GPU” switch to On. If you have a supported GPU, you can also choose “Use GPU” in the Wallet settings. Thread count is not relevant for GPU. Make sure your GPU has the latest drivers installed.

Please bear in mind that since GPUs are much more capable of parallel computations than CPUs, mining with GPUs is much more efficient.


If you want to setup a stand alone mining node and use either built in or external miner, follow sections below.

Creating CLI wallet for mining rewards
--------------------------------------

Before you can start mining using Beam you should create a wallet to collect mining rewards. Follow the steps in :ref:`command_line_user_guide` to perform the following operations

1. Create new wallet (see :ref:`creating_new_cli_wallet`)
2. Export miner key and owner key (see :ref:`exporting_miner_key` and :ref:`exporting owner key`)


.. attention:: Testnet 4 does not support built in GPU miner. It will be added back for Mainnet release

Using Beam Stratum Server
-------------------------

Beam node implements Stratum protocol for connecting external miner clients. Clients open a TCP connection to the node though which they receive jobs to mine blocks using Equihash mining protocol.

.. important:: Stratum server connections are protected using Transport Layer Security (TLS) protocol and require TLS certificates in order to work properly. You can either buy the certificates or create self signed certificates on your local machine.
	
	In addition a text file called 'statum.api.keys' should be created and contain one or more *API keys* - random strings of 8 characters or more. 


You will need to download the following components for your platforms:

1. Beam Node
2. Beam CLI Wallet
3. Beam mining client for your platform and GPU

In addition you will have to create a folder with the following files:

+-------------------------+----------------------------------------------------------------------------------+
| stratum.crt             | TLS certificate                                                                  |
+-------------------------+----------------------------------------------------------------------------------+
| stratum.key             | Private key for TLS certificate                                                  |
+-------------------------+----------------------------------------------------------------------------------+
| stratum.api.keys        | Text file with list of allowed API keys                                          |
|                         |                                                                                  |
|                         | Each key should have 8 symbols or more. example: abcd1234                        |
+-------------------------+----------------------------------------------------------------------------------+


For testing purposes ONLY stratum.crt and stratum.key can be downloaded from:

	https://github.com/BeamMW/beam/blob/master/utility/unittest/test.crt
	https://github.com/BeamMW/beam/blob/master/utility/unittest/test.key



Sample folder for running Stratum server can look something like this:

.. figure:: images/stratum_folder.png
   :alt: Sample contents of stratum folder


To run Beam Node with Stratum server you are required to provide the following parameters:

+-------------------------+----------------------------------------------------------------------------------------------------------+
|**Parameter**            | **Description & Example**                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| port                    | Port to start the server on                                                                              |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    port=10000                                                                                            |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| stratum_port            | Port the stratum server is listening for incoming connections                                            |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --stratum_port=10002                                                                                  |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| peer                    | Comma separated list of peer ip:port (must have at least one peer)                                       |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --peer=127.0.0.1:10003                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| stratum_secrets_path    | Path to a folder which holds TLS Certificate and API keys files described above.                         |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --stratum_secrets_path=.                                                                              |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| key_mine                | Miner key, exported by CLI wallet (see :ref: `Creating CLI wallet for mining rewards`)                   |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --key_mine=c3C9TVdEgza7w8p9na/B9rNeC8FvQAbJSPBfLZpW0sw                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| key_owner               | Owner key, exported by CLI wallet                                                                        |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --key_owner=mW9ItV9dUsSY9hN/dH19GEbzIUHQPw6VgDaCPYZiAsNL1LU                                           |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| pass                    | Wallet password.                                                                                         |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --pass=1234                                                                                           |
+-------------------------+----------------------------------------------------------------------------------------------------------+


Example command line. Please substitute your parameters

::

	./beam-node --port=<node port> --peer=<ip:port of the peer node --stratum_port=<port stratum server will listen to> --stratum_secrets_path=<folder with stratum key files> --key_mine=<miner key exported by wallet> --key_owner=<owner key exported by wallet> --pass=<wallet password>

Connecting Miner Client
-----------------------

Beam provides two mining clients for Equihash 150,5 with data path change: one for OpenCL and one for CUDA

.. attention:: Only OpenCL mining client will be available in Testnet 4

.. note:: Mining clients are only supported on Linux and Windows platforms

Miner clients are available for download from Beam download page. 

After extracting the client on a machine with supported GPU run the following parameter:

+-------------------------+----------------------------------------------------------------------------------------------------------+
|**Parameter**            | **Description & Example**                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| server                  | IP and port of the Stratum server to connect to                                                          |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --server 127.0.0.1:10001                                                                                  |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| key                     | API key you have set in your Stratum server (In stratum.api.keys file)                                   |
|                         |                                                                                                          |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --key abcd1234                                                                                        |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| devices                 | Only specify this flag to use specific GPU                                                               |
|                         |                                                                                                          |
|                         | By default, miner will use all available GPUs                                                            |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    --devices 0                                                                                           |
+-------------------------+----------------------------------------------------------------------------------------------------------+

Example command line:

::

	beamMiner.exe --server <ip and port of *stratum* server> --key <API key for the stratum server> --devices <id of the GPU device, if the flag not specified client will try to mine on all devices>



GPU Support
-----------

OpenCL Miner

+----------------+-----------------+----------------------------------------------------------------+
| **GPU**        | **Supported**   | **Reported Sol/s rate**                                        |
+----------------+-----------------+----------------------------------------------------------------+
|                |                 |                                                                |
+----------------+-----------------+----------------------------------------------------------------+

