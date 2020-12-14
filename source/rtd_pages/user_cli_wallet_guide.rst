.. _user_cli_wallet_guide:


.. _command line user guide:
.. _command_line_wallet_user_guide:

.. contents::

Command Line Wallet User Guide
==============================

The purpose of this document is to describe the process of setting up Beam node and command line wallet. 

.. attention::

    Beam blockchain does not store transaction history and SBBS addresses. These are only stored in local database inside the wallet data folder. 

    Please follow the guidelines below to avoid problems with sending are receiving Beam transactions.

    1. DO NOT run several wallet processes on the same wallet.db file. 

    2. Do not do listen and send at the same time using CLI wallet

    3. Do not copy the wallet.db to another machine and run another wallet simultaneously using the same wallet database
    
    4. Do not run two different wallets with the same seed at the same time

    5. SBBS messages sent between wallets expire after 12 hours. You have to connect within 12 hours of the transaction initiation to receive or send the funds.

    6. SBBS Addresses by default expire after 24 hours. Always use 'never' expiring addresses with pools and exchanges to make sure you receive payments.

Getting Started
---------------

Beam software runs on all operating systems: Linux, Mac OS and Windows. Before you start please verify that your operating system is supported by reviewing the :ref:`user_supported_platforms`.

All examples in this section are formatted for Linux / Mac platforms. If you are using Windows please substitute ./beam-wallet with beam-wallet.exe and run your commands using Windows Command Prompt.

.. _creating_new_cli_wallet:

Creating new wallet
-------------------

In order to create a new wallet run:

::

    ./beam-wallet init

You will be prompted to enter the Wallet Password, which is used to protect the wallet database 

.. warning:: Choose strong password for the wallet and keep it secret

   Anyone who knows your wallet password and can access your machine the wallet is stored on, will be able to spend **all your funds** and will have an access to all the metadata stored in the wallet, including transaction history!

Sample output for the ``init`` operation will look something like this:

::

    $ ./beam-wallet init
    I 2018-12-23.15:24:29.461 Rules signature: ddccf5d8d0f77bd2
    I 2018-12-23.15:24:29.462 starting a wallet...
    Enter password: ****************
    I 2018-12-23.15:24:32.524 Generating seed phrase...
    
    Generated seed phrase:
    
            despair;evoke;airport;seven;cricket;menu;current;ankle;require;monkey;maple;crawl;
    
            IMPORTANT
    
            Your seed phrase is the access key to all the cryptocurrencies in your wallet.
            Print or write down the phrase to keep it in a safe or in a locked vault.
            Without the phrase you will not be able to recover your money.
    
    I 2018-12-23.15:24:32.728 wallet successfully created...
    I 2018-12-23.15:24:32.750 New address generated:
    
    14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956
    
    I 2018-12-23.15:24:32.750 label = default


The ``Rules signature`` is a hash of current node configuration which is used to determine compatibility between different versions of nodes and wallets. 

Generated seed phrase is the :ref:`Seed Phrase <seed phrase>`. 

.. warning:: Copy the seed phrase to a secure location and keep it safe. 

   Seed phrase is the **most important secret** you need to keep to protect your funds. Anyone knowing the seed phrase will be able to control all your funds regardless of any other information. When generating new wallet each and every time, the safest scenario would be to make it on a secure air-gapped machine in a private environment and always keep the seed phrase in a secret and protected place.


The following line indicates that a new temporary :ref:`SBBS<sbbs>` address has been generated. This address is valid for the next 24 hours and can be used to receive coins. To generate new addresses see 'Creating new receive address' section below.

After wallet initialization is succeeded a ``wallet.db`` file is created in the same folder the wallet was run at. ``wallet.db`` is the wallet database file which is encrypted with the Wallet Password and contains the entire transaction history, keys and all the rest of the wallet metadata. If this file is deleted or lost, for any reason, you can always restore your funds using the Seed Phrase, however you will lose all transaction history and any additional metadata stored in the wallet database. To understand how to backup and restore the ``wallet.db`` file please check the :ref:`Backup and Restore` page.

In addition to the ``wallet.db file``, you will see the ``logs`` folder. A new log file is created every time you run the CLI wallet. Please attach logs to any support request you might send. See `Reporting Issues and Getting Support` section, for more details.


Restore a wallet from a Seed Phrase
-----------------------------------


For all the restore procedures see :ref:`Restore CLI wallet from Seed Phrase`

.. _exporting_miner_key:

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

It is important to **keep the Miner Key secret** since anyone who knows the miner key will be able to spend all the rewards mined by that miner.

.. _exporting owner key:

Exporting owner key
-------------------

The purpose of the ``Owner Key`` is to allow all nodes mining for you to be aware of all mining rewards mined by other nodes so that you would only need to connect to one node to collect all the rewards into your wallet. While in most other cryptocurrencies this is done by simply mining to a single address you control, in Mimblewimble it is not as simple since there are no addresses and the mining rewards should be coded with unique blinding factors which are deterministically derived from the ``Master Key``, and then tagged by the single ``Owner Key``. 

``Owner Key`` should be kept secret. ``Owner Key`` does not allow to spend coins, however it will allow to see all coins mined for you by all miners that use this ``Owner Кey``.

To export the ``Owner Key`` run the following command:

::

    ./beam-wallet export_owner_key

You will be prompted for the wallet password

Sample output for this command should look like this:

::

    $ ./beam-wallet export_owner_key
    I 2018-12-23.16:53:04.973 Rules signature: ddccf5d8d0f77bd2
    I 2018-12-23.16:53:04.974 starting a wallet...
    Enter password: *
    Owner Viewer key: dmVxtRCM3BH1VakviSB/XY86DsCKuWDLKk51eLDlibgMeL2fZ317Zdqx3E6oXbKtldqZz/lo5stTCSz9M1bDJdYUF4DG/ZaIuHHszi/H9wDmNDVboUdNtC/1Z/haWr9JxeIDtRSDBN+xpUbv


Printing the wallet info
------------------------

To print the current status of your wallet, run the following command:

::

    ./beam-wallet info

You will be prompted for the wallet password

A sample output for this command should look like this:

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

It is also possible to see the transaction history using the --tx_history flag

::

    ./beam-wallet  info --tx_history

You could also see the details of transaction using this command:

::

./beam-wallet tx_details --tx_id=<txid>

Receiving BEAMs
---------------

To receive BEAMs you need to connect to a specific node by running the following command:

::

    ./beam-wallet listen -n <node address and port, ex: 127.0.0.1:10000>

You will be prompted for the wallet password

A sample output for this command should look like:

::

    I 2018-12-23.17:07:55.526 Rules signature: ddccf5d8d0f77bd2                                                                        
    I 2018-12-23.17:07:55.527 starting a wallet...                                                                                     
    Enter password: ***************                                                                                                    
    I 2018-12-23.17:07:58.076 wallet sucessfully opened...                                                                             
    I 2018-12-23.17:07:58.078 WalletID 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956 subscribes to BBS channel 20 
    I 2018-12-23.17:07:59.297 Sync up to 8304-2dc4e5a393d6774b                                                                         
    I 2018-12-23.17:07:59.318 Current state is 8304-2dc4e5a393d6774b                                                                   

Once launched, the wallet will listen to updates from the server and any incoming transactions on the advertise SBBS address.

To receive funds you should send the address to the sending party via any available secure channel (Email, Telegram etc.)

When funds are sent you will see the incoming transaction in the wallet logs and on the screen. It should look similar to:

::

    I 2018-12-23.17:55:08.556 [7997ecd5c59e4865a6d938dbf339567e] Receiving 300 beams  (fee: 10 groth )
    I 2018-12-23.17:55:08.608 [7997ecd5c59e4865a6d938dbf339567e] Invitation accepted
    D 2018-12-23.17:55:09.203 Received PeerSig:     596857beae016ebd
    I 2018-12-23.17:55:09.216 [7997ecd5c59e4865a6d938dbf339567e] Transaction kernel: 95a8e48587c452b3
    D 2018-12-23.17:55:09.346 [7997ecd5c59e4865a6d938dbf339567e] has registered
    D 2018-12-23.17:55:09.367 Received PeerSig:     596857beae016ebd
    I 2018-12-23.17:55:09.428 Get proof for kernel: 95a8e48587c452b3

Sending BEAMs
-------------

To send beams you need to run the following command:

::

    ./beam-wallet send -n <node address and port, ex: 127.0.0.1:10000> -r <sbbs address> -a <amount (in Beams), ex: 11.3> -f <fee (in Groth) , ex: 0.2>

.. note:: 1 Groth equals 10^-8 Beam

The wallet log should look similar to something like:

::

    $ ./beam-wallet send -n 172.104.249.212:8101 -r 14a38140d8e66be9b8f1e8d770161fd33e35f7000053147b5a0f6a83178926b956 -a 10
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


Sending specific UTXO
---------------------

In some cases you might want to use specific UTXO for your transaction. To send funds using specific UTXO please follow the steps below:

1. Choose UTXOs you want to send using the `info` command

::

    ./beam-wallet info

In the output (as shown in the example below) choose the UTXOs you want to use

.. figure:: images/cli/choose_utxo.jpg
   :alt: Choose specific UTXO


2. in the `send` command, add --utxo parameter and specify a comma separated list of utxo ids:

::

    ./beam-wallet send -n <node address and port, ex: 127.0.0.1:10000> -r <sbbs address> -a <amount (in Beams), ex: 11.3> -f <fee (in Groth) , ex: 0.2> --utxo=<comma separated list of utxo ids>


.. figure:: images/cli/set_utxo.jpg
   :alt: Comma separated list of UTXOs

Cancelling and deleting of the transaction
------------------------------------------

Sometimes due to unsuccessful transaction or in different cases you need to cancel transaction. It is possible following the procedure below:

1.	Print the list of transactions using:

::

    ./beam-wallet  info --tx_history

2.	Get the id of the transaction you need and run:

::

    ./beam-wallet cancel_tx --tx_id=<txid, ex: f1e11512141a4f59b1c539ab1386ea84> -n <node address and port, ex: 127.0.0.1:10000>
    
Also you could delete useless transaction via first step and following command:

::

./beam-wallet delete_tx --tx_id=<txid, ex: f1e11512141a4f59b1c539ab1386ea84> -n <node address and port, ex: 127.0.0.1:10000>


Creating new SBBS address
-------------------------

In order to create new SBBS address, run the following command:

::

    ./beam-wallet new_addr --expiration_time=never|24h --comment="some comment"

You will be prompted for the wallet password

Sample output from this command should look like this:

::

    I 2018-12-23.18:16:44.112 Rules signature: ddccf5d8d0f77bd2
    I 2018-12-23.18:16:44.113 starting a wallet...
    Enter password: *
    I 2018-12-23.18:16:45.392 New address generated:

    646a773da4d4651f35fd75ca958b7859e89d8d8382b8155773bd396e2cc49cca

Creating address in new format
-------------------------

In order to create address in new format, run the following command:

::

    ./beam-wallet get_address --expiration_time=never --comment="some comment"

You will be prompted for the wallet password

Sample output from this command should look like this:

::

    I 2020-12-14.17:47:47.160 Rules signature: 0-ed91a717313c6eb0, 321321-6d622e615cfd29d0, 777777-1ce8f721bf0c9fa7
    Enter password: *
    I 2020-12-14.17:47:48.084 wallet sucessfully opened...
    I 2020-12-14.17:47:48.196 New address generated:

    3a92298f29cf61617a96749644cdcefb0b3a1c10beb52bc611ae7968116ae16b363

    I 2020-12-14.17:47:48.197 address: 8NmCQLhTTk2P7XeFZrHe1SNvAbpyfvrtgP1MJa7tx75fLDzcDeNqLTTxDfGg49wEfij8Z8i9qqfVR7jBiXnvQ2ousCBdTVdjgwuc4R6RYGZNTysNUGQei1vH42duGMFoB76fuKkCScran
 

Creating Offline address
-------------------------
In order to create new SBBS address, run the following command:

::

    ./beam-wallet get_address --offline 1

You will be prompted for the wallet password

Sample output from this command should look like this:

::

    I 2020-12-14.17:45:45.613 Rules signature: 0-ed91a717313c6eb0, 321321-6d622e615cfd29d0, 777777-1ce8f721bf0c9fa7
    Enter password: *
    I 2020-12-14.17:45:47.901 wallet sucessfully opened...
    I 2020-12-14.17:45:47.901 Generating offline address
    I 2020-12-14.17:45:48.028 New address generated:

    4185792e5691fafc4135355c343d0d7cf97d20fbdf20e1b020c21320e188e55327

    I 2020-12-14.17:45:48.030 address: 3XHPHapAXANcf3KT1LPMmzE4ADxkCAFyvU3767TiFWAtVukMVjwnHG9VnFcVevgptKmLLPXTAiw8MxX9tFTZ2SVe3CrDEzj6ShRk5ofhYJ6VHsrkJ5PwxP8mqcHcp3wH1qRcae5eeBXSHg7Z6pqyZS6LrxBU5rBdxddn2mwk7zrNwCZj4gk5NCXvLfuCaP6SmAkcbibcQN2oAmxfFW8J71YiuQ58gCki4QVoWXXt859hmPeobQ1qqDJMJo1M6Y8mmVhpLaismnWHxC42fuf1k6AmeJVtuf6hD2zVBCtu82AU9hDoXa1ieArPiPzRpopvDYYeKwsnGiTCf6Mwz4Q4ab5JC6Rb7bd7YbT7EkvycaLrzvzYyeDfbozP9BRJLvKYF4UycV9mvZV8DKT8UNHsLD75q3dQcbQc4dMoixHPcqKa4Jq5McmqqNCzzfwDDGbt7wTTHV

.. note:: It is important to provide number of payments(aka vouchers). When payments run out, the Sender wallet will automatically send request for more payments to the Receiver wallet using SBBS.If Receiver wallet is online within 12 hours of the request (until the SBBS message expires) it will send 30 more offline payment vouchers to the sender. Otherwise, Sender will receive notification that there are no more vouchers and will have to request another offline address via external channel.

Creating Public Offline address
-------------------------
In order to create new SBBS address, run the following command:

::

    ./beam-wallet get_address --public_offline

You will be prompted for the wallet password

Sample output from this command should look like this:

::

    I 2020-12-14.17:55:55.843 Rules signature: 0-ed91a717313c6eb0, 321321-6d622e615cfd29d0, 777777-1ce8f721bf0c9fa7
    Enter password: *
    I 2020-12-14.17:55:56.815 wallet sucessfully opened...
    I 2020-12-14.17:55:56.816 Generating public offline address
    I 2020-12-14.17:55:56.818 address: A4Y8nZvGgzE7hvGT5QX4P3VqEeWpxPe8PCQ5o5nhATNrtJbExhgbuwQHGavD5XaSTXPLAovgZXQPExW38A6Z5ZcovwqPkSVmWu2wEhGjv7dV4sDMpxFGFF1tiKJudJcZZNASeZTQ1ZTYBybiDENxbiH5gcqzBQhqC3P3ke3SxABPYqHL4pTSRmginWx2JJF7sVkiPTQAEoqCfU7C6v9uisjURNcvv4PdkG68QKf2GWRUqYEH9UPwKi7gFZxKpnfKToa1fDSRo3xqeMVEB2ZrYAw9k3wqb2seZHtVzACiTc

.. note:: Public Offline is used if you expect to receive offline transactions from another Beam wallets on regular basis.This address can be used in multiple transactions. Example: Used Public offline addresses for collecting donations while your wallet is completely offline

Print list of all addresses
---------------------------

To print the entire list of addresses use the following command:

::

    ./beam-wallet address_list

A sample ouput for this command will look something like this

::

    I 2019-02-25.19:41:26.839 Beam Wallet 1.2.4419 (mainnet)
    I 2019-02-25.19:41:26.839 Rules signature: ed91a717313c6eb0
    I 2019-02-25.19:41:26.841 starting a wallet...
    Enter password: *
    I 2019-02-25.19:41:27.718 wallet sucessfully opened...
    Addresses

     comment         |address                                                               |active  |expiration date     |created
                       14e191aaebace13b14e3ab41382280baff288faa312545eadd1a1bcfa3adaeac6ff    false    2019.02.25 12:34:07  2019.02.24 12:34:07
                       12908d7079a41ca9929ed33b965758f261030e766d3bcf0524ce1d21f55b88dc8ff    false    2019.02.20 12:32:11  2019.02.19 12:32:11
     default           d2fb05822407ca08d2dcc735894b63a26c6d2c1b88d6deddabaee887f6a668b086     false    2019.02.20 10:33:50  2019.02.19 10:33:50


Change address expiration
-------------------------

It is possible to extend the address expiration period to '24 hours' from the current time using the following command:

::

    ./beam-wallet change_address_expiration --address=14e191aaebace13b14e3ab41382280baff288faa312545eadd1a1bcfa3adaeac6ff

For specific address.

To change all existing addresses in the wallet just omit the `--address` parameter

You could also choose what specific period it would be:

::

./beam-wallet change_address_expiration --address=<sbbs address> --expiration_time=(never|24h|now)

There are three options: never,24 hours or now

- never - makes the address eternal (will never expire)
- 24h - extends the address by 24 hours from the current time
- now - makes the address expired immediately. Be careful as wallet stops listen this address.



Export and import SBBS addresses and transaction history
--------------------------------------------------------

Sometimes when upgrading the wallet or restoring from seed phrase you need to reimport the list of SBBS addresses and transaction history (the data) from the previous wallet. To do that use the commands below:

To export the data:

::

    ./beam-wallet export_data --file_location=<full path to addresses file, for example: C:\Users\user\addresses.dat>

To import the data
::

    ./beam-wallet import_data --file_location=<full path to addresses file, for example: C:\Users\user\addresses.dat>

.. note:: It is important that imported addresses were originally created by the wallet with the SAME seed phrase. Only addresses matching the wallet seed phrase will be imported. Other addresse will not be imported as shown in the screenshot below.


.. figure:: images/cli/wrong_address.jpg
   :alt: Choose specific UTXO



.. _proof_of_transaction_cli:

Proof of transaction
--------------------

Starting from 1.1.4194 version, receiver wallet automatically signs proof of received transaction and sends it to the sender. Upon request, sender can generate proof of transaction following the procedure below:

1. Print the list of transactions using:

::

    ./beam-wallet  info --tx_history

2. Get the id of the transaction we need and run:

::

    ./beam-wallet payment_proof_export --tx_id=<txid>

Sample output of the command above should look something like:

::

    I 2019-01-14.14:40:37.464 Payment tx details:
    Sender: 4bd0ca080bd8c3ec4b3061bf5916aa34266f0649a7c151c6777ffe492f15e09768
    Receiver: ebb27b5501213c84eb212ea276e8ced74f540fbcceb0f4c1c2da2c5108188651a1
    Amount: 6 groth
    KernelID: 4ac2f195ce9056c171fd0cd41e8a02dc9c0bb72861b2e03fbbbb5942e5e63d1a

    I 2019-01-14.14:40:37.465 Sender address own ID: 1547460707000004
    I 2019-01-14.14:40:37.465 Exported form: 000000000000004bd0ca080bd8c3ec4b3061bf5
    916aa34266f0649a7c151c6777ffe492f15e0976800000000000000ebb27b5501213c84eb212ea27
    6e8ced74f540fbcceb0f4c1c2da2c5108188651a1864ac2f195ce9056c171fd0cd41e8a02dc9c0bb
    72861b2e03fbbbb5942e5e63d1a7728a2954a10d3bfb9938f0c17509a6a0e870c6bb22ff2d1297f3
    dae7f54592b00e84c6b3c9ea3e3ad9bc43661b6dcf7dbd818ccc92707d1d75b429697e8492653

3. Send the contents of exported form only (proof) to the receiver, our case it will look like this:

::

    I 2019-01-14.14:40:37.465 Exported form: 000000000000004bd0ca080bd8c3ec4b3061bf5
    916aa34266f0649a7c151c6777ffe492f15e0976800000000000000ebb27b5501213c84eb212ea27
    6e8ced74f540fbcceb0f4c1c2da2c5108188651a1864ac2f195ce9056c171fd0cd41e8a02dc9c0bb
    72861b2e03fbbbb5942e5e63d1a7728a2954a10d3bfb9938f0c17509a6a0e870c6bb22ff2d1297f3
    dae7f54592b00e84c6b3c9ea3e3ad9bc43661b6dcf7dbd818ccc92707d1d75b429697e8492653

4. Receiver can verify that proof is correct by running :

::

    ./beam-wallet payment_proof_verify --payment_proof=<proof>


.. note:: Sender can require receiver to always send proof of transaction by using --payment_proof_required=1. Please note that this will prevent working with older wallets.


.. _cold_wallet:

Cold Wallet
-----------

To use the wallet in 'cold' mode you need to initialize it with ``--cold_wallet`` flag.

::

    ./beam-wallet init --cold_wallet

This command will create two databases: wallet.db and wallet.db.private.

.. _sending_from_cold_wallet:

Sending from cold wallet
------------------------

Pre-conditions: Make sure the cold wallet is synced. In order to do so, follow the next steps:

1. Copy the wallet.db file to the "hot" wallet's data folder.
2. Launch the "hot" wallet and wait till it's synced.
3. Stop the "hot" wallet, copy the wallet.db file into the "cold" wallet folder.
4. Launch the "cold" wallet for listening.

::

   ./beam-wallet listen --cold_wallet

Now as the "cold" wallet is synced, proceed with the next steps:

1. In the cold wallet run the command: 
   
::

   ./beam-wallet send -a <amount> -r <receiver address> -f <fee> --cold_wallet

.. note:: Here is no need in node address in this case.

2. Copy wallet.db file to "hot" wallet's data folder.
3. Launch "hot" wallet. It should send encrypted message to the node, also he may get encrypted message back.
4. Stop "hot" wallet, copy wallet.db file into "cold" wallet folder.
5. Launch "cold" wallet for listening beam-wallet listen ``--cold_wallet`` it should create a signed transaction kernel.
6. Copy wallet.db from "cold" to "hot" new transaction should go to the node and got confirmed.
7. Copy wallet.db from "hot" to "cold" "cold" wallet should have actual balance and transactions statuses.

.. _receiving_to_cold_wallet:

Receiving to cold wallet
------------------------

1. Generate new address in "cold" wallet and send it to the sender.
2. Copy wallet.db to "hot" wallet.
3. Launch "hot" wallet. Note there will be no new transactions, since "hot" wallet cannot decrypt incoming messages.
4. Stop "hot" wallet. copy wallet.db from "hot" to "cold".
5. Launch "cold" wallet for listening, it should get new transaction and accept it.
6. Copy wallet.db from "cold" to "hot".
7. Launch "hot", wait until new transaction becomes completed.
8. Copy wallet.db "hot" to "cold" balance and transactions statuses should be correct.

.. _rescan_cli:

Rescan wallet
-------------

During regular operation the wallet constantly monitors the blockchain and updates the information in the wallet.
However, if you suspect that your balance, transaction or UTXO status is not up to date or invalid, you can always 'rescan' the blockchain and update the information in your wallet with the latest state.

In order to rescan the CLI wallet please follow the steps below:

1. Run a node with your 'owner' key and make sure it has completed the synchronization with the network. See :ref:`exporting owner key`

::

    ./beam-node --peer=<ip or url of the peer> --owner_key=<your owner key>

2. Run 'rescan' command as follows:

::

    ./beam-wallet rescan -n <ip:port of the node with the owner key>

3. Run 'listen' command to get updated information from the node

::

    ./beam-wallet listen -n <ip:port of the node with the owner key>

4. Wait for the wallet to synchronize and check that balance and transactions were update using 'info' command

::

    ./beam-wallet info


.. _lelantus&onesidedpayment:

.. _lelantus :

LelantusMW Shielded Pool
------------------------


LelantusMW is a new protocol that was enabled during the 5.0 hard fork in order to augment the MW and allow to avoid UXTO linkability in transactions graph. To make UTXOs unlinked user should insert regular BEAM UTXO into *shielded pool*, converting these UTXOs into *shielded UTXOs* and then, after some time extract them back as *unlinked* UTXOs. *Shielded UTXO* belonging to the wallet could be detected by the node with owner key (as regular utxo), and user can use this info to extract these coins back.

To send coins in the pool and get from it using commands insert_to_pool and exctract_from_pool accordingly.

.. warning:: Minimal fee is 1000100 groth for commands insert_to_pool and exctract_from_pool


Sending to the pool
-------------------


To send in the pool, use the following command:

::

  ./beam-wallet insert_to_pool -a <amount in Beams> -f <fee in Groth> -n <node address and port>

Example:

::

  ./beam-wallet insert_to_pool -a 0.1 -f 1000100 -n 127.0.0.1:10000
  
The wallet log should look similar to something like:

::

  I 2020-06-08.16:50:41.289 [0b530328913649ae9edeb111eebfb0dd] Sending to shielded pool 10000000 groth (fee: 1000100 groth)
  I 2020-06-08.16:50:41.363 [0b530328913649ae9edeb111eebfb0dd][1] Transaction created. Kernel: a9ffbf4ccfe7bda2037fff64c12f4c9d6a31aaf6b9c8bc4edc027d2e5074fdb7, min height: 46068, max height: 46188
  D 2020-06-08.16:50:41.373 [0b530328913649ae9edeb111eebfb0dd][1] sending tx for registration
  D 2020-06-08.16:50:41.374 Async update finished!
  D 2020-06-08.16:50:41.392 [0b530328913649ae9edeb111eebfb0dd][1] register status 1
  D 2020-06-08.16:50:41.393 Async update started!
  I 2020-06-08.16:50:41.394 [0b530328913649ae9edeb111eebfb0dd][1] Get proof for kernel: a9ffbf4ccfe7bda2
  I 2020-06-08.16:51:25.797 [0b530328913649ae9edeb111eebfb0dd] Get proof of shielded output.
  D 2020-06-08.16:51:25.798 Async update finished!
  I 2020-06-08.16:51:25.798 Synchronizing with node: 100% (1/1)
  I 2020-06-08.16:51:25.798 Current state is 46070-053d21db8b61712f
  D 2020-06-08.16:51:25.799 Async update started!
  I 2020-06-08.16:51:25.800 [0b530328913649ae9edeb111eebfb0dd] Transaction completed


For assets you should specify your asset with ID (for example ``--asset_id 1``) and ``--enable_assets`` flag. 

::

  ./beam-wallet insert_to_pool -a 0.1 -f 1000100 -n 127.0.0.1:10000 –asset_id 1 –enable_assets
  
Checking UTXO in pool
---------------------

To see your coins in the pool use the following command:

::

  ./beam-wallet info --shielded_utxos
  
The wallet log should look similar to something like:

::

   SHIELDED COINS                 

  | ID    |BEAM|  GROTH |       createTxID                |spentTxID |confirmHeight|spentHeight|anonymitySet(approx)|targetAnonymitySet|
  | 14658 |  2 |   0    |                                 |          |       26074 |           |                 33 |               64 |
  | 14685 |  0 |20000000| 9f6d519d44104f89b8ee0c8ca4d41027|          |       44784 |           |                  6 |               64 |
  | 14686 |  0 |20000000| 7942ad47289742b6baccf5dfebc6a3e7|          |       44785 |           |                  5 |               64 |
  | 14687 |  0 |20000000| 34f648a4ac35423a8c6781ede84cf347|          |       44787 |           |                  4 |               64 |
  | 14689 |  0 |10000000| 28bde747b63e42c589aec1355cb64a6b|          |       45968 |           |                  2 |               64 |
  | 14690 |  0 |10000000| 0b530328913649ae9edeb111eebfb0dd|          |       46070 |           |                  1 |               64 |

Your coin is in the pool. When other users send coins in the pool, your coin will gain anonymity.

For assets you should add ``--assets`` flag:

::

  ./beam-wallet info --shielded_utxos --assets


Receiving from the pool
-----------------------

To get a coin from the pool, use the following command:

::

  ./beam-wallet extract_from_pool --shielded_id <id from info> -f <fee in Groth> -n <node address and port>
  
Example:

::

  ./beam-wallet extract_from_pool --shielded_id 14685 -f 1000100 -n 127.0.0.1:10000
  
The wallet log should look similar to something like:

::

  I 2020-06-08.19:52:31.961 [52a2b38b6bc047dd8d7a0f457153f782] Extracting from shielded pool: ID - 14686, amount - 20000000 groth, receiving amount - 18999900 groth (fee: 1000100 groth)
  D 2020-06-08.19:52:32.014 Async update finished!
  D 2020-06-08.19:52:32.022 Async update started!
  I 2020-06-08.19:52:32.024 [52a2b38b6bc047dd8d7a0f457153f782] Get shielded list, start_index = 14630, count = 64
  D 2020-06-08.19:52:32.024 Async update finished!
  D 2020-06-08.19:52:32.028 Async update started!
  I 2020-06-08.19:52:32.042 [52a2b38b6bc047dd8d7a0f457153f782][1] Transaction created. Kernel: 1140ff7c5f205e551585658f272fb474e722a211cc729714567bf7cbd6713057, min height: 46256, max height: 46376, shielded id: 14686, window start: 14630, window end: 14694, window size: 64, total shielded outs: 14705
  D 2020-06-08.19:52:32.053 [52a2b38b6bc047dd8d7a0f457153f782][1] sending tx for registration
  D 2020-06-08.19:52:32.054 Async update finished!
  D 2020-06-08.19:52:32.074 [52a2b38b6bc047dd8d7a0f457153f782][1] register status 1
  D 2020-06-08.19:52:32.077 Async update started!
  I 2020-06-08.19:52:32.078 [52a2b38b6bc047dd8d7a0f457153f782][1] Get proof for kernel: 1140ff7c5f205e55
  I 2020-06-08.19:53:49.749 [52a2b38b6bc047dd8d7a0f457153f782][1] Get proof for kernel: 1140ff7c5f205e55
  D 2020-06-08.19:53:49.752 Async update finished!
  D 2020-06-08.19:53:49.757 Async update started!
  I 2020-06-08.19:53:49.759 [52a2b38b6bc047dd8d7a0f457153f782] Transaction completed
  
Add ``--enable_assets`` flag to get assets from pool.

::

  ./beam-wallet extract_from_pool --shielded_id 14685 -f 1000100 -n 127.0.0.1:10000 –enable_assets

.. note:: For confidential assets don't forget to use appropriate info. You should take ``shielded_id`` from column ID from table called by this command: 

::

  ./beam-wallet info --shielded_utxos --assets
  
Make sure that coins are gone from pool using command ``beam-wallet info --shielded_utxos``:

::

  SHIELDED COINS                 

  | ID    |BEAM|  GROTH |       createTxID                |spentTxID                       |confirmHeight|spentHeight |anonymitySet(approx) |targetAnonymitySet|
  | 14685 |  0 |20000000| 9f6d519d44104f89b8ee0c8ca4d41027|3b9d77ea6fab490b86f55a46d0224746|       44784 |            |                   6 |               64 |
  | 14686 |  0 |20000000| 7942ad47289742b6baccf5dfebc6a3e7|52a2b38b6bc047dd8d7a0f457153f782|       44785 |            |                   5 |               64 |
 
 
One side payments
-----------------

In MW in order to create a valid transaction all the parties must collaborate. Here we'll present a one-side payment scheme, which, after initial setup, allows arbitrary senders to pay specified (fixed) values to a particular receiver, without any further collaboration from the receiver side.

With Lelantus we are able to without need to be online, this is also known as one-side payments. To make them we need to accomplish the following steps. 

1. Generating token

Receiver should generate a token with needed quantity of vouchers (allowed number of payments)

.. note:: ``--voucher_count`` - this is the number of payments that can be made for the issued token. The maximum number of vouchers is 20. if you specify more, only 20 vouchers will be printed

The wallet log should look similar to something like:

::

  $ beam-wallet get_token  --voucher_count 3
  I 2020-06-09.11:43:06.494 Beam Wallet 5.0.9065 (master)
  I 2020-06-09.11:43:06.496 Rules signature: 0-5547a592195f4cd4, 10-2fdbbbb74ac57c55, 20-67131c58aa9a6b85
  Enter password: *
  I 2020-06-09.11:43:07.258 wallet sucessfully opened...
  I 2020-06-09.11:43:07.423 New address generated:

  3d4cd7ad643d38293d44b7a55a2635bd4249a06de49ca13ef5191ebb0357b41d515

  I 2020-06-09.11:43:07.434 token:   5oCbHdCswvWWJhVg1aw5CjeovfSZrr8ykh9JhksjaxNacDHEKTtCAUqAawBNuSjY29kNYA5BRiozdRV9sW9eaWct4km9CwE6hUQzXWWGMpYspBvt7bTmknwiRbKHejzimzw8vqeksAPxnASPbV9C8xXvM4Svkxxsr3Xu42HL7RJHNYTGWAcjgyaPrLZYUEnDxgusBrcLP8jV8EsRyyaysB75up1jW1FFcNE3MJA1EMA3G3w7Gry9ZMGieFKgqB1DHfX2zmNt3PgYX73MUsAvmBiqtzVoFKnZ8DjhR3sg1RNQfYuJb6vhriNm22cjnBZekt1AXEm2ycbRcKYhxRK97RRojL9akAeNz5De2CzQwLvaUjLLxXCpUfbCS1QQ3vh5ZMQhAR3EkDsUkKgv9vbM63LfF3WGpYFAbJYeCmsnZjPUktMUGQwnoykQDMptgMBRh74rQXa6DwVXwRJiAyhaZFMirW6zc1gvnYZg6afsQhqCFXJmJJ7SRRPHimxpfQrakj6J7HdvktwRd43HdSXcXo8YQGiDmaphxrsKjja8fm7qikra5H6xrDghgfNNCgCeXpDR9qFiYB8tBmaZKs58H4WZvAsRM6w6wj1LqzL5hdnCwYXqgmcWkAZ2Ay5MXsAhEkyBdiXsaAaUrr4ievxFj25FD9JB429ofx62CCS6SHXY8MsxLcAqi7AACtNHRLTjgzCrVwoWqZxK6hxXGqpK9tnAELKQpGJrPY5HdfRH2JieSFpqCge5zmnkHYq1Y636Da5rZy5tBFfWBo2FXSsqprWJA1Pu4yHPamKzbf2i8LPfV4xUzVtSmg3YtrFbTYtyyPyj7kkW4KEPtUEy3kACMuJUJfCJ4qpgr226dVdhrgMsxkeMRph2vC6Rktsj4xbrp4WkHBJ7UJHbQh8ZwatbJLh4Sg7kTT9a3Re29kcGRHU6rEv1EqfpuuLigPiZPvSzQpmHynDx4AftXsrXt3mG9f6CSnt7MkdfKM34F6CejNknawueNzVtKziTnE7pLXnHv1o96BAcQdL1L1SASRYoNa3V1AN2


Send your token to the Sender person over a secure communication channel and go offline.

2. Sending payment

On this step sender has token and can make payments according to quantity of vouchers which this token has.
Payment should be sent in the pool with the following command:

::

  ./beam-wallet insert_to_pool -r <token> -n <node address> -a <amount> -f <fee>
  
Example:

::

  ./beam-wallet insert_to_pool  -r MRdCxZtQBBgen66NFHVvE43zrsXE2GL94jkNK4WB73aYzaNQLe2SpEHKbYUeo4UpY35biuCa48oAvr1r1LXm2CCZDv8Bav1VohqKMw3H277YRzmGdof1TQJfzFKnGK1GZYbJmEK5xWhBnqMxkWfWRNtKXSHwmB4dkAqK8cpqypk9PLgTjRDqze5JzYnDmkRN5DAuig2pAUMTm7ftthBhNBM15c3mSrcY1vYsvdjJYxLq8Jjy7toZHp9XsNWM58eYrfuQcDZrJwbcSraquw2X7qWZG3T2Z5ibvBDd8czUs27vAc8GNX7z3XEN5MqGAxB1UZC9ErmP1mMtBdKpBTMj15Mu2saqrpJ85x1ttgSe1T1rNZpDCRshEnSm5CmMctn2W16QrvuqYUTFJh83eJVoEqdvTLGcJSHcoe6drCvb7iS6NLJuU -a 0.2 -f 1000100 -n 127.0.0.1:1000
  
For assets you should specify your asset with ID  ``--asset_id`` and ``--enable_assets`` flag.

::
 
 ./beam-wallet insert_to_pool -r <token> -n <node address> -a <amount> -f <fee> --asset_id  --enable_assets

Example:

::

   beam-wallet insert_to_pool  -r 5oCbHdCswvWWJhVg1aw5CjeosV98DTD3oDmhWBnYWVmgoB6Gi8fQEeEWG8tpwthvYSuUasEmSi8jK8n8U128KorFH1C4Vu75NVqf2vTECcZ6npnRYsCaHWuqdqmDZKuBcwBm2yzzQKjTiAYEjseyLpFK5ruNc7TW9co37W8RM9Rf3WiJmoFywkEZT5JLgtFEP2fPAJyHZ6dJJ2iJqTyb1pD1kxeuP1udxa7uSzqGkhKpWCqgJjnxMXc8qKbQoTCLFoLrQeMApJYkouEwHaqhcAn9akrZ5YwMfNQVF53i2FVr7s4GfvSnStxkjSDLPawhahh933VD2UnwE4U1GKh5o4KcWwtL7dLJrd8BCmQCj35Q8yXNLcxyTrU31Ti19r4c7d3dRjAfQGKkQq2tXnuzJryBYLqx8nKZjbuYGTQ4dj3EJKP46DpxkTKuJJ9ZpAwaRptRtrhgW8nKf4a6jH22KZU1RpvuTGbwHas2hWWhuepTaPiy45tKffUHhPeAMLqh8MutnhYQYxCDH1dZGNtjuwiyFcTGhEdDUdnSmadpKbmasi6gzxvHU3PkUWcHpnPeXbR73ita4HyH8PNjJYkkVMZF2X3DJLUwvsaxZHx9TkxHqXD7HT3kKwYWqvE66jvbqT6q1UbVEnKKztwuZnFDJZb9XHgcmjZqfSgvf1fTdnxv9EFtq8rzwT6QzLCEX6xY9CgTPkhEJgjtHayWdEjrhxUK4KUYVe3L8GmYMCXBzFtHBKRwyUqpmmZgTbZYsiiVB2DPwKWfpkXJ7D4XzkaLMDsEbVawjowPpEn8giL8MUTjwoEXfMzVhs3iKdUe5XpZj4NZbgFNwGGdoAqE7T8vLAzjumWGhGcZGC8Z3NBfESgVCiuxniVNQsLf9YEW3eBayu59sMp5xEokzdyjRCjJer8nh6VgFJbjTLaVZF5kqbZfRVBiomCBG6zfg5A6k2PjnuS7fmosBTWQrK4hxmXnqmnoEWq6WoYcDZcEJufifaq6u6jyV7BukVyo5H3iJ5o1m9885LYtT86uVYczthV3xx4vPrKE -a 0.2 -f 1000100 -n 127.0.0.1:1000  --asset_id 8 --enable_assets
   

3. Checking the payment

.. attention:: In order for the recipient to see shielded UTXOs , the wallet must be connected to the node with its owner_key.

After a while rceiver became online and check if he has *shielded UTXOs* in pool.

::

  ./beam-wallet info --shielded_utxo
  
.. note:: for assets use command ``./beam-wallet info --shielded_utxos --assets``

All that remains is extract UTXOs from pool, using already known command:

::

  ./beam-wallet extract_from_pool --shielded_id <id from info> -f <fee in Groth> -n <node address and port>
 
.. note:: for assets use this command with appropriate info:

::

  beam-wallet  extract_from_pool --shielded_id <id from info --assets> -f <fee> -n <node address> –enable_assets
  




