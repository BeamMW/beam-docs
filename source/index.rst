.. _root:

.. image:: rtd_pages/images/beam-logo.jpg
   :scale: 15
   :align: right


Welcome to Beam documentation!
==============================

.. _rules_signature:

.. note:: Beam is currently in Mainnet.

   Rules Signature: 1ce8f721bf0c9fa7 (for height >= 777777)

	Download binaries from: `Beam Downloads Page <https://www.beam.mw/downloads>`_

	Source code: `Beam Github <https://github.com/BeamMW>`_


Current release
===============

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


**TL;DR**

:ref:`I want to Mine Beam<mining_beam>`

:ref:`I want to learn how to use Beam Desktop Wallet<desktop_wallet_guide>`

:ref:`I want to learn how to use Beam Command Line Wallet<command_line_wallet_user_guide>`



What is Beam?
--------------

`Beam <https://beam.mw/>`_ is a next generation scalable, confidential cryptocurrency based on an elegant and innovative `Mimblewimble protocol <https://scalingbitcoin.org/papers/mimblewimble.txt>`_ and `LelantusMW protocol <https://github.com/BeamMW/beam/wiki/Lelantus-MW>`_.

Things that make BEAM special include:

* Users have complete control over privacy - a user decides which information will be available and to which parties, having complete control over his personal data in accordance to his will and applicable laws.

* Beautiful and usable `wallets <https://beam.mw/downloads>`_ for all platforms

* Confidentiality without penalty - in BEAM confidential transactions do not cause bloating of the blockchain, avoiding excessive computational overhead or penalty on performance or scalability while completely concealing the transaction value.

* No trusted setup.

* Blocks are mined using `BeamHash III <https://docs.beam.mw/beamHash_III_spec.pdf>`_ Proof-of-Work algorithm.

* Limited emission using periodic halving.

* No addresses are stored in the blockchain - no information whatsoever about either the sender or the receiver of a transaction is stored in the blockchain.

* Superior scalability through compact blockchain size using the “cut-through” feature of Mimblewimble.

* No premine. No ICO. Backed by a treasury, emitted from every block during the first five years.

* Implemented from scratch in C++.

.. _start:

Getting Started
---------------

The simplest way to get started with Beam is by visiting the `Beam website <https://beam.mw>`_, `downloading wallets <https://beam.mw/downloads>`_ and joining `Beam Community <https://t.me/BeamPrivacy>`_ on Telegram for updates and discussions.

.. danger:: Beam is extremely new and experimental technology. No guarantees can be provided by anyone whatsoever. Use it at your own risk. Make sure you know what you are doing, especially if there is money involved.

Just like any other cryptocurrency, using Beam requires learning and understanding what this all is about. If real money is involved, it also requires concern with security of the process.

That said, you can always safely play with Beam by connecting to the permanent `Testnet <https://beam.mw/downloads/testnet>`_  and following instructions in :ref:`desktop_wallet_guide`.

To lean more about how cryptocurrencies work in general and Beam in particular please visit our :ref:`Resources` page


Important differences from other cryptocurrencies
-------------------------------------------------

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



Reporting Issues and Getting Support
------------------------------------

To report issues and get support please perform the following steps:

1. Gather all relevant information including:

   * Detailed description of the problem you have encountered and steps to reproduce it
   * Version of the binaries you are running
   * Logs (see :ref:`log locations` for information where to find the logs files)
   * Relevant configuration files (please check for private information before sending)
   * Your system configuration
   * Screen shots or any additional information you think is relevant


2. Send an email to support@beam.mw (or testnet@beam.mw for testnet related issues).

   You can also open an issue in github and follow the provided template.

.. attention:: Providing all the information described above will allow us to quickly and efficiently analyze and resolve the issue for you and everyone else.


.. toctree::
   :caption: User's Guide
   :hidden:

   rtd_pages/user_desktop_wallet_guide.rst
   rtd_pages/user_mobile_wallet_guide.rst
   rtd_pages/user_cli_wallet_guide.rst
   rtd_pages/user_beam_node_guide.rst
   rtd_pages/user_backup_restore.rst
   rtd_pages/user_mining_beam.rst
   rtd_pages/user_atomic_swap.rst
   rtd_pages/user_atomic_swap_cli.rst
   rtd_pages/ca.rst
   rtd_pages/laser.rst
   rtd_pages/user_web_wallet.rst
   rtd_pages/user_blockchain_explorer.rst
   rtd_pages/user_supported_platforms.rst
   rtd_pages/user_files_and_locations.rst
   rtd_pages/user_testnet_and_mainnet.rst
   rtd_pages/user_reporting_issues.rst
   rtd_pages/user_troubleshooting.rst
   rtd_pages/user_resources.rst
   rtd_pages/user_glossary.rst

.. toctree::
   :caption: Developer's guide
   :hidden:

   rtd_pages/dev_building_beam.rst
   rtd_pages/dev_understanding_logs.rst
   rtd_pages/dev_consensus_rules.rst
   rtd_pages/dev_local_setup.rst

