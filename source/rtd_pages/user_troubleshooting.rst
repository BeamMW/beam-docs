.. _user_troubleshooting:

Wallet Troubleshooting (all wallets)
====================================

Where are the wallet files located?
-----------------------------------

When Beam Wallet desktop app is installed, the wallet data files are stored separately from the binaries. The locations of all the files are described here: :ref:`Files and Locations`

My transaction is stuck 'In Progress' for a long time
--------------------------------------------------------------

In progress means that the message sent to the other wallet address was not answered yet. Each message has a lifetime of 12 hours, so if the message will not be answered during that time transaction will be canceled automatically by the wallet. At this stage, the sender can cancel the transaction by clicking on transaction menu and selecting 'Cancel'.


My transaction is stuck in 'Synching with blockchain' for a very long time
--------------------------------------------------------------------------

In order to create a transaction Sender and Receiver should exchange messages with all the necessary information. After that, Sender creates the transaction and sends it to the network for distribution and mining.

'Synching with blockchain' is a state in which wallet waits for a message from the other side. For a 'Sender' it means that the message was sent and not answered yet. For a 'Receiver' it means that the answer was sent but the transaction is not yet visible in the blockchain either because it was not sent to the network or because it was not mined yet.

In any case, if the transaction does not appear in the blockchain after 2 hours it is automatically canceled by the wallet.

.. note: In older versions of the wallet (before 1.1.4201) the timeout was set to 24 hours.


I’ve forgot the local password for my wallet
--------------------------------------------

See :ref: `Restoring funds`


I’ve restored the wallet but my balance is zero
-----------------------------------------------

One or more the of the words is wrong or misspelled. Triple-check that all the words from the seed phrase are typed in correctly. You will need to repeate the :ref: `Restoring funds` procedure.


I've forgot my password
-----------------------

If you lost your password and cannot get into your wallet, you will have to remove ``wallet.db`` file and to `Restore funds` using your seed phrase to create a new password. 

Why is the seed phrase the only thing connecting me to my funds?
----------------------------------------------------------------

To ensure the utmost privacy, the only information we can use to link you to your wallet is your seed phrase. So, if you lose it we cannot recover it for you.

I've lost my seed phrase
------------------------

By design, the only way to access your funds (UTXO) is to have the seed phrase. If you still have access to your wallet, create another wallet with new seed phrase on another device and transfer funds to there. Any solution that would allow you to access your funds without the seed phrase would severely compromise the privacy of BEAM. Therefore, in case you don't have any active access to your funds there is nothing to do (the funds will be stored in the blockchain forever and no one will be able to access or spend them).

I've copied my ``wallet.db`` file to the new machine and I'd like to run wallets on both new and old machines simultaneously  
----------------------------------------------------------------------------------------------------------------------------

At the current implementation each ``wallet.db`` file should be managed by only a single wallet instance. Any case involving manual transfer of the wallet database **is not supported**.


I am trying to send Beam but transactions are failing 
-----------------------------------------------------

In certain cases, the wallet my get out of sync with the blockchain which might result in UTXOs that were already spent being incorrectly marked as available. When such UTXOs are selected for a transaction by the wallet, the transaction will be rejected by the blockchain.

To fix the situation, do the following:

1. Open the Wallet and open Settings tab

2. Switch to a local node

3. Click on 'Rescan' button 

4. Wait for the wallet to synchronize

In some cases this operation may result in change if your wallet balance, which was incorrectly displaying already spent UTXOs as available. 

If this does not help, you may try to resync the wallet completely by following the procedure below:

1. Erase the wallet.db (you can back it up), because it may continue to create duplicated coins. Then restore it via your secret phrase. No need to erase node.db.

2. After the sync is complete - send all your "visible" funds to yourself. You can set fee=0. Wait until transaction completes.

3. Wait for 2 days. Meanwhile you may use your wallet normally, but some of the funds may still look missing.

4. After 2 days: Erase both wallet.db AND node.db. Then - do a full restore.



Desktop Wallet Troubleshooting 
==============================

Why is my available balance lower than expected while I'm sending BEAM?
-----------------------------------------------------------------------

UTXO can be locked during active outgoing transaction. The locked amount is displayed as a change in 'Sending screen'. The change will become spendable when the transaction expires or completes.


I’ve restored the wallet but I can’t see my transaction list and/or my active addresses
---------------------------------------------------------------------------------------

As explained in `Restoring funds`, only your available balance (i.e. your UTXO) is kept on the blockchain, hence that’s all that can be restored.


I’ve restored the wallet using my seed phrase - can someone still send me money to the addresses created in the previous wallet?
--------------------------------------------------------------------------------------------------------------------------------

When a wallet is restored, *only the balance (UTXO) is restored*. Addresses (active and expired), contacts and transaction history are only stored locally, so they can't be restored from the blockchain. Each wallet is aware of only the active and expired addresses it displays. Therefore, all transactions sent to the addresses no wallet is aware of anymore will fail by timeout and the funds will be automatically released in Sender's wallet.


Why can't I just cancel the transaction in the 'Synching with blockchain' state?
--------------------------------------------------------------------------------

Your wallet has already disclosed enough information so that transaction can be created anyway and sent to the network even if you cancel it. 


Wallet is stuck in 'Downloading blocks' screen
----------------------------------------------

1. Close your wallet

2. Locate the Beam Wallet folder :ref:`Files and Locations`

3. Use any text editor to open settings.ini file

4. Check the contents of the 'peers' value

::

   [localnode]
   mining_threads=0
   port=10005
   run=true
   peers=@Invalid()

   [node]
   address=us-node01.mainnet.beam.mw:8100 

5. If the value is @Invalid() replace it with the following:


::

   [localnode]
   mining_threads=0
   port=10005
   run=true
   peers=eu-node02.mainnet.beam.mw:8100, eu-node01.mainnet.beam.mw:8100, us-node02.mainnet.beam.mw:8100, us-node04.mainnet.beam.mw:8100, ap-node01.mainnet.beam.mw:8100, ap-node02.mainnet.beam.mw:8100

   [node]
   address=us-node01.mainnet.beam.mw:8100 


My peers look ok but the wallet is still stuck during sync
----------------------------------------------------------

1. Close your wallet

2. Locate the Beam Wallet folder :ref:`Files and Locations`

3. Delete node.db file and all files starting with 'tempmb'

4. Restart the wallet



Command Line Wallet Troubleshooting
===================================

I am getting the ``error code=26, file is not a database`` error when starting the command line wallet
------------------------------------------------------------------------------------------------------

Notice how you were starting the wallet:

:: 

	I 2018-12-23.17:32:34.619 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-23.17:32:34.620 starting a wallet...
	Enter password: ***
	D 2018-12-23.17:32:36.664 sqlite error code=26, file is not a database
	E 2018-12-23.17:32:36.665 Wallet data unreadable, restore wallet.db from latest backup or delete it and reinitialize the wallet

You have submitted an incorrect password. The wallet can not decrypt the database file and hence reports that data is unreadable.
*Only if you are absolutely sure that password is correct, remove the database file and restore wallet from your Seed Phrase*


I am getting the ``Failed. No inputs`` exception when starting the command line wallet
--------------------------------------------------------------------------------------

Notice how you were starting the wallet:

::

	I 2018-12-23.17:45:12.529 Rules signature: ddccf5d8d0f77bd2
	I 2018-12-23.17:45:12.530 starting a wallet...
	Enter password: *
	I 2018-12-23.17:45:13.226 wallet sucessfully opened...
	I 2018-12-23.17:45:13.228 WalletID 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956 subscribes to BBS channel 20
	I 2018-12-23.17:45:13.271 [9edc454f2752461eb682f21c4efbd33e] Sending 10 beams  (fee: 0 groth )
	E 2018-12-23.17:45:13.272 You only have 0 groth
	E 2018-12-23.17:45:13.273 [9edc454f2752461eb682f21c4efbd33e] exception msg:
	E 2018-12-23.17:45:13.273 [9edc454f2752461eb682f21c4efbd33e] Failed. No inputs
	I 2018-12-23.17:45:13.293 [9edc454f2752461eb682f21c4efbd33e] Transaction failed. Rollback...


The most common cause of this error is trying to send a transaction with insufficient funds. You can not send a greater amount than you have.

Miscellaneous Troubleshooting
=============================

My question is not answered anywhere
------------------------------------

See `Reporting issues and getting support`


