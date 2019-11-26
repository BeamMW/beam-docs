.. _root:

.. image:: rtd_pages/images/beam-logo.jpg
   :scale: 15
   :align: right


Welcome to Beam documentation!
==============================

.. _rules_signature:

.. note:: Beam is currently in Mainnet.

   Rules Signature: 6d622e615cfd29d0 (for height >= 321321)

	Download binaries from: `Beam Downloads Page <https://www.beam.mw/downloads>`_

	Source code: `Beam Github <https://github.com/BeamMW/beam>`_


Current release
===============

**Double Dopple 4.0**

This release includes desktop wallet support for Atomic Swaps

**Known limitations:**

1. Inconsistent transaction statuses when running two or more wallets that use the same wallet.db file, cloned manually.
2. If multiple wallets are restored from the same seed phrase, transaction history and addresses will not be shared among the wallets.

**Points to mention:**

In case a mobile wallet is connected to a random node and the user has both mobile and a desktop wallets which are using the same seed phrase, the funds sent to the desktop wallet won’t appear on the mobile wallet. If the desktop wallet is running a local node, it will see funds sent to both wallets. The reason is that the local node (integrated into desktop wallet) always monitors the blockchain for UTXOs related to the seed of the wallet. The mobile wallet does not run a local node and thus can only monitor transactions sent to its specific SBBS addresses. Of course, no funds will be lost in any event.


**TL;DR**

:ref:`I want to Mine Beam<mining_beam>`

:ref:`I want to learn how to use Beam Desktop Wallet<desktop_wallet_guide>`

:ref:`I want to learn how to use Beam Command Line Wallet<command_line_wallet_user_guide>`



What is Beam?
--------------

`Beam <https://beam.mw/>`_ is a next generation scalable, confidential cryptocurrency based on an elegant and innovative `Mimblewimble protocol <https://scalingbitcoin.org/papers/mimblewimble.txt>`_.

Things that make BEAM special include:

* Users have complete control over privacy - a user decides which information will be available and to which parties, having complete control over his personal data in accordance to his will and applicable laws.

* Confidentiality without penalty - in BEAM confidential transactions do not cause bloating of the blockchain, avoiding excessive computational overhead or penalty on performance or scalability while completely concealing the transaction value.

* No trusted setup required.

* Blocks are mined using Equihash Proof-of-Work algorithm.

* Limited emission using periodic halving.

* No addresses are stored in the blockchain - no information whatsoever about either the sender or the receiver of a transaction is stored in the blockchain.

* Superior scalability through compact blockchain size using the “cut-through” feature of Mimblewimble.

* No premine. No ICO. Backed by a treasury, emitted from every block during the first five years.

* Implemented from scratch in C++.

.. _start:

Getting Started
---------------

The simplest way to get started with Beam is by visiting the `Beam website <https://beam.mw>`_, reading and understanding the materials posted there and joining `Beam Community <https://t.me/BeamPrivacy>`_ on Telegram for updates and discussions.

.. danger:: Beam is extremely new and experimental technology. No guarantees can be provided by anyone whatsoever. Use it at your own risk. Make sure you know what you are doing, especially if there is money involved.

Just like any other cryptocurrency, using Beam requires learning and understanding what this all is about. If real money is involved, it also requires concern with security of the process.

.. hint:: That said, you can always safely play with Beam by connecting to the permanent Testnet.


To lean more about how cryptocurrencies work in general and Beam in particular please visit our :ref:`Resources` page

Once you familiarized yourself with key ideas and concepts, it is recommended to start from connecting to our Testnet. The simplest way to do that is by downloading and installing our Desktop Wallet and following instructions in :ref:`desktop_wallet_guide`.




Important differences from other cryptocurrencies
-------------------------------------------------

Mimblewimble has several important differences from most other existing cryptocurrencies which are very important to understand. Please review the following information carefully.

**The concept of Address is completely different**

In most cryptocurrencies Address is a hashed public key for which the owner of that Address knows the corresponding private key. In order to transfer funds, the Sender should only know the Address of the Receiver in order to create a unilateral transaction. *The Sender is not aware of whether the Receiver is online or not or whether it even exists*. Once transaction to an Address is complete and added to the blockchain, Receiver that can prove knowledge of the private key corresponding the Address can control this UTXO (short for Unspent Transaction Output).

In Mimblewimble there are no addresses at all and transaction are created **interactively** by both Sender and Receiver wallets. This means that in order to create a transaction, both wallets have to participate in the creation process and eventually co-sign the transaction before it is sent to the blockchain.

.. attention:: In Beam it is not possible to create a transaction unilaterally. Both Sender and Receiver have participate in transaction creation.

To allow Sender and Receiver wallets to create transactions without having to be online at the same time and directly connected to each other, Beam added a module called :ref:`SBBS<sbbs>` that allows wallets to securely communicate using encrypted messages to create a transaction. SBBS Addresses are merely private / public key pairs used to encrypt and decrypt these messages.

.. important:: SBBS Addresses are not recorded in the blockchain and are not used to control funds

You are encouraged to create a new SBBS Address for each transaction.

**Wallet and Node concepts are slightly different**

Beam documentation mentions terms Wallet and Node quite a lot and it sometimes causes confusion with users of other cryptocurrencies.

Beam Wallet is a *light client* which stores information about UTXO that belong to it and has an ability to create new transactions by connecting to other wallets via :ref:`SBBS<sbbs>`. It does not store or verify the entire blockchain and can thus only work if connected to a Node.

Beam Node, is a *full node* that downloads, validates and updates the entire blockchain state.

.. note:: Beam Desktop Wallet, provides options to run both as just the Wallet (connected to a remote node) and as a full node.

.. attention:: It is always recommended to run a full node

**Information that can be restored from the blockchain is completely different**

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

