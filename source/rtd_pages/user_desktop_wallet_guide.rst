.. _user_desktop_wallet_guide:


.. _desktop_wallet_guide:

Desktop Wallet User Guide
=========================

Using Beam Dekstop Wallet is the simplest way to start using Beam. It is available for Linux, Mac and Windows platforms (see :ref:`supported platforms` for details). 

To download the Desktop Wallet for your platform go to http://beam.mw/downloads and follow instructions there.

Once the wallet is installed on your platform follow this guide 


Creating new wallet
-------------------

One you launch the wallet for the first time, you will be suggested to either create a new wallet or restore from existing seed phrase

.. figure:: images/desktop/1_create_restore_screen.png
   :alt: Choosing between new and restore


Click 'Create new wallet'. 

.. attention:: Restoring flow is covered in :ref:`restore desktop wallet from seed phrase` section of the :ref:`backup and restore` document



Generating seed phrase
----------------------

Wallet will generate a new :ref:`seed phrase` for you. Seed phrase is your secret that will allow you to restore your coins. It's the most important secret you have to keep.

.. figure:: images/desktop/2_new_wallet_screen.png
   :alt: Before generating seed phrase


.. warning:: Be careful when generating the seed phrase. It's for your eyes only. Always do it on a clear and air gapped machine.

.. figure:: images/desktop/3_new_wallet_phrase_screen.png
   :alt: Generating seed phrase


.. warning:: Always store your seed phrase in a safe and secure location. Write it on a piece of paper. Do not store electronically as plain text

.. figure:: images/desktop/4_new_wallet_phrase_confirm_screen.png
   :alt: Keeping seed phrase safe warning

In order to make sure that you have really wrote down your :ref:`seed phrase<seed phrase>`, the wallet will ask you to enter a selection of words from your phrase in random order.

.. figure:: images/desktop/5_new_wallet_repeat_screen.png
   :alt: Repeat your seed phrase 


When you type all the words correctly you will be allowed to proceed to the next step

.. figure:: images/desktop/7_new_wallet_repeat_screen_3.png
   :alt: Indicate correct words 


Setting Wallet Password
-----------------------

Next thing you need to do is to set Wallet Password


.. figure:: images/desktop/8_new_wallet_password_screen_1.png
   :alt: New wallet password 

Wallet Password protects your wallet in case someone has access to your computer or has stolen your wallet database file. It is important to choose strong password that you can remember. The wallet will provide some indication of password strength for your convenience. Do not count on it however. Choose password that is at least 8 symbols long with combination of characters from different types, such as letters numbers and special symbols

.. figure:: images/desktop/9_new_wallet_weak_password_screen.png
   :alt: Example of weak password 


.. figure:: images/desktop/10_new_wallet_strong_password_screen.png
   :alt: Example of strong password

Choosing Wallet Mode
--------------------

Beam Desktop Wallet can be run in one of three modes.

To run a local node from within the wallet choose the first option (recommended)

.. figure:: images/desktop/11_new_wallet_mode_local_screen.png
   :alt: Start wallet in local mode  


You can change the default port the node will be listening on, if necessary and, in case of CPU mining, set the amount of mining threads. You will be probably provided at least one default peer to connect to but you can always add more peers from the list of bootstrap nodes published in the `downloads section of Beam website <http://beam.mw/downloads>`_. 


Random mode allows you to automatically connect to random bootstrap node. In this mode Beam Wallet acts like 'light client', it will create transactions but will have to trust the remote node for blockchain verification. It is recommened for weaker devices.

.. figure:: images/desktop/12_new_wallet_mode_random_screen.png
   :alt: Start wallet in random mode  


If you are running your own node somewhere and want to connect specifically to it, use the third option by providing the IP and port the node is listening on.

.. figure:: images/desktop/13_new_wallet_mode_remote_screen.png
   :alt: Start wallet in remote mode  

Wallet Synchronization
----------------------

Once the Wallet is connected, it synchronizes the current blockchain data from the network. In case Beam Wallet is running with local node this process might take some time. The wallet will first download and validate the latest :ref:`macroblock` and then all the rest of the blockchain. 

.. figure:: images/desktop/14_new_wallet_sync_screen.png
   :alt: Start wallet in local mode  


Main Screen
-----------

Main Screen of the wallet shows the current balance of both available and unconfirmed Beams as well as the transaction history.  

.. figure:: images/desktop/15_main_screen_empty.png
   :alt: Main screen  

In the top left corner, under the screen title, you see connection indicator which shows whether the wallet could successfully connect to peers. In brackets, it specifies the network to which the wallet is connected. In the screenshot above it says '(master)' which means the wallet is connected to internal developers network, called masternet. In case of Testnet 4, it will say '(testnet4)'. If the wallet is unable to connect to the peer it will be shown by red indicator.

.. figure:: images/desktop/15_main_screen_empty.png
   :alt: Main screen  

Address Screen
--------------

.. figure:: images/desktop/16_address_screen_default.png
   :alt: Address screen

UTXO Screen
-----------

In Beam, like in most other cryptocurrencies, your balance is constructed as a result of...

.. figure:: images/desktop/17_utxo_screen_empty.png
   :alt: UTXO Screen

Settings screen
---------------

.. figure:: images/desktop/18_settings_local_node.png
   :alt: Address screen