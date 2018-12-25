:orphan:

.. _dev_consensus_rules:


.. _consensus_rules:

Consensus Rules
================

The following parameters allow to configure consensus rules in Beam Node and Wallet

.. admonition:: WARNING: Used for development and testing only

   Consensus parameters are only relevant for testing and development purposes. Changing these parameters will change the Rule Signature and hence break the compatibility of the Node and Wallet with running Mainnet or Testnet servers.

Rules
------------------------

+---------------------------+----------------------------------------------------------------------------------------------------------+
|**Parameter**              | **Description & Example**                                                                                |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| EmissionValue0            | Initial coinbase emission in a single block (in Groth, 10^-8 of Beam)                                    |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    EmissionValue0=800000000                                                                              |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| EmissionDrop0             | Height of the last block that still has the initial emission. Emission drops by half in the next block.  |
|                           | Default equals 1 year, assuming 1 block per minute                                                       |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    EmissionDrop0=525600                                                                                  |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| EmissionDrop1             | Number of blocks in halving cycle (defaults to four years, assuming 1 block per minute )                 |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    EmissionDrop1=2102400                                                                                 |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| MaturityCoinbase          | Number of blocks that should be mined (confirmations) before coinbase UTXO can be spent.                 |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    MaturityCoinbase=240                                                                                  |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| MaturityStd               | Number of blocks that should be mined (confirmations) before normal (non coinbase) UTXO can be spent.    |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    MaturityStd=0                                                                                         |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| MaxBodySize               | Block body size (in bytes)                                                                               |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    MaxBodySize=0x100000                                                                                  |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| DesiredRate_s             | Target block rate (in seconds)                                                                           |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    DesiredRate_s=60                                                                                      |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| DifficultyReviewWindow    | Number of blocks in the window for the mining difficulty adjustment                                      |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    DifficultyReviewWindow=1440                                                                           |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| TimestampAheadThreshold_s | Block timestamp tolerance (in seconds)                                                                   |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    TimestampAheadThreshold_s=7200                                                                        |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| WindowForMedian           | Number of blocks considered in calculating the timestamp median                                          |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    WindowForMedian=25                                                                                    |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| AllowPublicUtxos          | Flag allowing regular (non-coinbase) UTXO to have non-confidential signature                             |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    AllowPublicUtxos=0                                                                                    |
+---------------------------+----------------------------------------------------------------------------------------------------------+
| FakePoW                   | Flag to disable verification of PoW. Mining is simulated by timer.                                       |
|                           |                                                                                                          |
|                           | .. code-block:: bash                                                                                     |
|                           |                                                                                                          |
|                           |    FakePoW=0                                                                                             |
+---------------------------+----------------------------------------------------------------------------------------------------------+

Below is an example of corresponding .cfg fie section:

::

	################################################################################
	# Rules configuration:
	################################################################################

	# initial coinbase emission in a single block
	# EmissionValue0=800000000

	# height of the last block that still has the initial emission, the drop is starting from the next block
	# EmissionDrop0=525600

	# Each such a cycle there's a new drop
	# EmissionDrop1=2102400

	# num of blocks before coinbase UTXO can be spent
	# MaturityCoinbase=240

	# num of blocks before non-coinbase UTXO can be spent
	# MaturityStd=0

	# Max block body size [bytes]
	# MaxBodySize=0x100000

	# Desired rate of generated blocks [seconds]
	# DesiredRate_s=60

	# num of blocks in the window for the mining difficulty adjustment
	# DifficultyReviewWindow=1440

	# Block timestamp tolerance [seconds]
	# TimestampAheadThreshold_s=7200

	# How many blocks are considered in calculating the timestamp median
	# WindowForMedian=25

	# set to allow regular (non-coinbase) UTXO to have non-confidential signature
	# AllowPublicUtxos=0

	# Don't verify PoW. Mining is simulated by the timer
	# FakePoW=0
