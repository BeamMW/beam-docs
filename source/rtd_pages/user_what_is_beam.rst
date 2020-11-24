.. _what_is_beam:

What is Beam?
=============

.. contents::

Project overview
----------------

`Beam <https://beam.mw/>`_ is a scalable, confidential cryptocurrency based on an elegant and innovative `Mimblewimble protocol <https://scalingbitcoin.org/papers/mimblewimble.txt>`_ and `LelantusMW protocol <https://github.com/BeamMW/beam/wiki/Lelantus-MW>`_.

Beam development started in March 2018, and only nine and a half month later Beam Mainnet was launched on January 3rd 2019, the ten year annyversary of the Bitcoin genesis block.

Today Beam is one of the leading confidential cryptocurrencies listed on over fifty exchanges and accepted in several hunderd online stores and services.

Key features
------------

* All Beam transactions are confidential by default. There are no publicly visible transactions in Beam.

* Beautiful and usable `wallets <https://beam.mw/downloads>`_ for all platforms.

* Uses cryptograhical protocols that do not require trusted setup.

* Used `BeamHash III <https://docs.beam.mw/beamHash_III_spec.pdf>`_ Proof-of-Work conensus algorithm.

* Limited emission using periodic halving.

* No addresses are stored in the blockchain - no information whatsoever about either the sender or the receiver of a transaction is stored in the blockchain.

* Superior scalability through compact blockchain size using the “cut-through” feature of Mimblewimble.

* No premine. No ICO. Backed by a treasury, emitted from every block during the first five years.

* Implemented from scratch in C++.

* Supports decentralized Atomic Swaps with BTC, LTC, QTUM and other cryptocurrencies

* Supports direct payment channels

* Supports confidential assets

* Supports Offline transactions

* Supports Max Privacy transctions with 64K anonymity set


Latest release
--------------

**Eager Electron 5.1.9898**

This release includes:

Features:

* Enabled Offline transactions by implementing LelantusMW protocol
* For Offline transactions new “offline” addresses are supported: it includes all the necessary information for 10 payments so that a receiver doesn’t need to talk to the sender to create a transaction. Once the ten payments run out, the sender wallet will automatically request more payments from the receiver using SBBS. In case the Receiver is not online and not responding, the Sender wallet will show an indication that there are no more payments left and the user will request a new address using external channel.
* Atomic swaps are significantly cheaper now due to SegWit support and a minimal fee rate is nicely recommended so that transactions will complete within a reasonable time
* Confirmation count is implemented for CLI wallet and in API to better align with exchanges

Improvements:

* Confidential Assets metadata is standardized. Read more here.
* Settings were restructured for better usability

**Known limitations:**

1. Offline transactions are only supported when Desktop wallets run their own node
2. In case a mobile wallet is connected to a random node and the user has both mobile and desktop wallets that are using the same seed phrase, the funds sent to the desktop wallet won’t appear on the mobile wallet. If the desktop wallet is running a local node, it will see funds sent to both wallets. The reason is that the local node (integrated into the desktop wallet) always monitors the blockchain for UTXOs related to the seed of the wallet. The mobile wallet does not run a local node and thus can only monitor transactions sent to its specific SBBS addresses. Of course, no funds will be lost in any event.
3. BEAM wallets won’t display received Confidential Assets and amounts kept in the shielded pool. Please use CLI ar API till the future notice.


**Important differences from other cryptocurrencies**


Mimblewimble has several important differences from most other existing cryptocurrencies which are very important to understand. Please review the following information carefully.

**The concept of Address is completely different**

In most cryptocurrencies Address is a hashed public key for which the owner of that Address knows the corresponding private key. In order to transfer funds, the Sender should only know the Address of the Receiver in order to create a unilateral transaction. *The Sender is not aware of whether the Receiver is online or not or whether it even exists*. Once transaction to an Address is complete and added to the blockchain, Receiver that can prove knowledge of the private key corresponding the Address can control this UTXO (short for Unspent Transaction Output).

In Beam, Addresses are not recorded in the blockchain and are not related to coin ownership. They are just containers of transaction related information between Sender and Receiver wallets, are only stored locally and can be discarded at any time.

Beam supports two types of transactions: Regular and Offline. 

**Regular** (Mimblewimble interactive) transactions go through the following steps:

1. **Generating address** - Receiver generates a 'Regular' address by using 'Receive' operation in the wallet and sends it to the Sender via external channel (i.e Telegram, email etc...)
2. **Initiating transaction** - Sender initiates transction by pasting the address into the 'Send' dialog in the wallet and fills in the required amount, fee and optionally additional details. 
3. **Receiver response** - Receiver wallet must be online within 12 hours of the moment transaction was initiated. It signs the receiver part and sends it back to the sender.
4. **Finalize** - Sender walelt must be online within 12 hours of Receiver response to finalize the transaction, generate payment proof (store locally) and send the transaction to the network.

**Offline** (LelantusMW non-interactive) transactions go through the following steps:

1. **Generating address** - Receiver generates a 'Offline' address by using 'Receive' operation in the wallet and sends it to the Sender via external channel (i.e Telegram, email etc...). 
2. **Sending transaction** - Sender pastes the Address into the 'Send' dialog in the wallet, specifies the amount and clicks 'Send'. The transaction is immediately sent to the network and no additional interactions are required


.. note:: The 'Offline' address are valid for 10 offline payments, since each offline payment spends a unique identifier. When payments run out the Sender wallet automatically attempts to get more payments from the Receiver through SBBS. If the Receiver is online payments are automatically replenished, otherwise the Sender wallet indicates that there are no more payments left and the Sender needs to contact the Receiver via external channel to get new Offline address.

.. note:: Offline transaction fees are signicantly higher (minimum ~0.01 BEAM) than 'Regular' transactions (minimum 100 Groth). This is due to the fact that Offline transactions leave more permanent information in the blockchain.

**Wallet and Node concepts are slightly different**

Beam documentation mentions terms Wallet and Node quite a lot and it sometimes causes confusion with users of other cryptocurrencies.

Beam Wallet is a *light client* which stores information about UTXO that belong to it and has an ability to create new transactions by connecting to other wallets via :ref:`SBBS<sbbs>`. It does not store or verify the entire blockchain and can thus only work if connected to a Node.

Beam Node, is a *full node* that downloads, validates and updates the entire blockchain state.

.. note:: Beam Desktop Wallet, provides options to run both as just the Wallet (connected to a remote node) and as a full node.

.. attention:: It is always recommended to run a full node

**Only the total balance for your seed phrase can be restored from the blockchain**

In most blockchains, information about current UTXOs and the transaction history can be recovered from the blockchain using only the :ref:`Seed Phrase<seed phrase>`.

In Beam, only UTXOs can be recovered from the blockchain. All other information, including transaction history and any other meta data are only stored locally in the Beam Wallet database and encrypted by :ref:`Wallet Password<wallet password>`.

This means that if you run Beam Wallet on two different machines, transaction history **WILL NOT** be synchronized.

This also means, that to preserve transaction history, or any additional meta data, it is necessary to regularly backup Beam Wallet database file.

For more information about backup and restore procedure see :ref:`backup and restore`

.. _supported platforms:

Supported Platforms
-------------------

Beam Node and Beam Wallet are currently supported on the following platforms:

	:fa:`linux` ``64-bit`` Linux OS Ubuntu 14.04 LTS Trusty Tahr, Ubuntu 16.04 LTS Xenial Xerus, Ubuntu 18.04 LTS Bionic Beaveр
	:fa:`microchip` ``64-bit`` Processor
	:fa:`database` ``5GB`` of free RAM
	:fa:`hdd-o` ``10GB`` of free Disk (*the size of the block chain increases over time*)

	:fa:`apple` ``64-bit`` Mac OS 10.13 or higher
	:fa:`microchip` ``64-bit`` Processor
	:fa:`database` ``5GB`` of free RAM
	:fa:`hdd-o` ``10GB`` of free Disk (*the size of the block chain increases over time*)

	:fa:`windows` ``64-bit`` Windows 8 or higher
	:fa:`microchip` ``64-bit`` Processor
	:fa:`database` ``5GB`` of free RAM
	:fa:`hdd-o` ``10GB`` of free Disk (*the size of the block chain increases over time*)


.. attention:: At the moment Beam only works on processors that support AVX instruction set. 


.. note:: Please report any issues you might encounter while running BEAM software on your system. 



.. _rules_signature:

Mainnet Rule Signature
----------------------

Beam Mainnet Rule signature: 1ce8f721bf0c9fa7 (for height >= 777777)
