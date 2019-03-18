.. _user_glossary:


Glossary
========

.. _address:
.. _addresses:
.. _sbbs address:
.. _sbbs addresses:

Address
-------
    In Beam, addresses are only used by SBBS system to connect between Wallets during transaction creation. Unlike most other blockchains, addressses are not recorded in the blockchain and are not used to prove ownership of the coins. Each address has a default expiration time of 24 hours (which can be changed using Wallet UI). In general, it is recommened to generate fresh receiving address for each transaction. 

.. _blinding factor:

Blinding factor

	Blinding factor is a secret key that is deterministically derived from a `master key`_ and is used to 
	
.. _block:
.. _blocks:

Block
    A block is a record in the Beam blockchain that contains a set of transactions sent on the network. Pending inclusion in a block, a transaction is kept in the `mempool`_ in an `unconfirmed`_ state. Roughly every 2.5 minutes, on average, a new block is appended to the `blockchain`_ through `mining`_ and the transactions included receive their first `confirmation`_.

.. _block reward:
.. _block rewards:

Block reward
    A block reward is new `beams`_  created after the successful `mining`_ of a block. For the first five years, the block reward in Beam is split into a `miners' reward` and a `treasury`. During this time, miners receive 80% per block with the remaining 20% split between `Beam Foundation`,  founders, employees, investors and advisors. Block reward is subjected to periodic halving and is halved for the first time after about one year (in blocks) and then every four years.
    
.. _blockchain:

Blockchain
    The blockchain is a public record of Beam transactions. The blockchain can be downloaded and verified by all Beam nodes to make sure the transaction history is valid and no `double spending <https://en.wikipedia.org/wiki/Double-spending>`_ occurs. In Beam, a compacted version of the blockhain is maintained by each node using the `cut through`_ feature of `mimblewimble`_ which enables new nodes to only download minimal amount of information to start mining and verifying new blocks.

.. _blockchain explorer:

Blockchain Explorer
	The Blockchain explorer is a website showing the current status of Beam blockchain and history of mined blocks. 

.. _cut through:

Cut through
	In `mimblewimble`_ protocol, cut through feature enables creation of compacted, yet still verifiable, blockchain history by removing all intermediate transactions and thus significantly reducing the amount of information required by a new node in the system to start mining or verifying new blocks. 



.. _macroblock:

Macroblock
----------
	A macroblock is a compressed version of blockchain history implementing the cut-through feature of Mimblewimble protocol. Each node generates macroblocks in the background and stores them on the local disk. When new node connects to the system it first downloads the latest Macroblock and then updates more recent blocks in the blockchain one by one. This allows to significantly reduce the time of onboarding new nodes into the system.


.. _master key:

Master key
	Master key (or master secret key) is the key used to generate all blinding factors in a single wallet. Master key is also used to generate Miner Keys and Owner key used to mine coins for a specific wallet. In general

.. _dificulty:
.. _mining difficulty:

Mining difficulty

	Mining difficulty is a dynamic parameter which determines amount of calculations necessary to solve Beam Proof of Work puzzle. It is designed to ensure that blocks are created once a minute (on average) regarless of number of miners in the network. Current block creation time and difficulty can be seen using the `blockchain explorer`_.

.. _seed phrase:

Seed Phrase

	A list of 12 words that hold all information necessary to generate Master Key and hence to recover all Beam UTXOs belonging to a wallet created using this phrase. Seed  phrase is generated during wallet initialization and should be kept secret at all times. If lost, the Seed Phrase CAN NOT BE RECOVERED by any means. Keep it safe.

.. _mimblewimble:

Mimblewimble
	Mimblewimble is the protocol used by Beam to provide confidentiality of transactions and scalability in terms of compact blockchain size. `Mimblewimble white paper <https://scalingbitcoin.org/papers/mimblewimble.txt>`_ was published in July 2016 by an anonymous author under the pseudonym Tom Elvis Jedusor.  


.. _sbbs:

SBBS

	SBBS (abbreviation of Secure Bulletin Board System) is a subsystem within Beam Node that allows wallets to securely exchange encrypted messages and create transactions without having to be online at the same time.

.. _wallet password:

Walet Password
	
	Wallet Password is a password that protects wallet and encrypts wallet database used to store information about UTXOs, transactions and any additional metadata stored by the wallet. Wallet Password is NOT used for or has any relation to ownership of the coins. If Wallet Password is lost, the wallet database can no longer be accessed and the transaction history and metadata will be lost. However it is possible to recover all the currently owned UTXOs, by creating a new wallet and initializing it using the same `seed phrase`_ as the original one. 

.. _transaction:
.. _transactions:

Transactions

	In `mimblewimble`_ protocol transactions contain of Inputs, Outputs and Kernels. Each input and output are represented by Pedersen Commiments in a form: P = v*H + b*G, where v is transaction value, b is the `blinding factor`_ and G and H are two known 'nothing up my sleeve' generator points on the same elliptic curve.
