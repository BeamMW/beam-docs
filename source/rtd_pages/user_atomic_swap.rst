.. _user_atomic_swap:

Introduction to Atomic Swap
===========================

The idea of atomic swap was presented as solution for the next problem: two parties (Alice and Bob) want to exchange their coins without having to trust а third party.

In a simplified way non-atomic approach consists of four steps:

1. Alice send her A Coins to Bob.
2. Bob receives A Coins.
3. Bob sends his B Coins to Alice.
4. Alice receives B Coins. 


The weakest part of this such approach is lurking in step #3. By malicious intent, Bob can avoid following his part of the agreement.
Atomic swap is provided to guarantee compliance of the agreement.

The way this really works in practice is as follows

1. Alice and Bob create three transactions between their wallets: Lock Transaction, Redeem transaction and Refund transaction.

2. Both parties lock their coins on the respective chain using the Lock Tx. In this state the coins belong to both parties and can not be spent.

3. Once the lock is confirmed, the parties exchange secret used to lock funds and send the Redeem Tx to the chain, effectively getting the swapped coins.

4. If the swap fails for any reason, Refund Tx can be sent to the network after some significant period of time to get the locked coin back for each party. 


.. note::

  Atomic Swaps are an advanced feature and are currently in beta. 

  DO NOT USE SWAPS FOR LARGE AMOUNTS OF MONEY  

  For Bitcoin use version `Bitcoin Core v0.17.1 <https://bitcoin.org/en/download>`_ .

  For Litecoin use version `Litecoin v0.17.1 <https://litecoin.org/#download>`_ .



Atomic Swaps using Desktop Wallet
=================================

To enable swap functionality Beam wallet should first connect to the node and wallet of the other currency. This can be done using either your own instance of a full node via RPC or by using an Electrum service.

Connecting to BTC / LTC / QTUM full node
----------------------------------------


To connect to your own node perform the following steps (Litecoin example shown, for additional information and settings please use original documentation for Bitcoin, Litecoin and QTUM respectively)

1. Configure the litecoind to run with JSON RPC using the following commands in litecoin.conf configuration file

::

  # server=1 tells litecoin-QT to accept JSON-RPC commands.
  server=1

  rpcport=9432
  
  # You must set rpcuser and rpcpassword to secure the JSON-RPC api
  rpcuser=liteuser
  rpcpassword=123

.. note:
  If you are connecting to testnet network, the rpcport setting should be put in the 'test' section

  [test]
  rpcport=9432

Make sure the node is running and fully synchronised

2. Connect Beam wallet to the node

Open Settings tab in the Beam Wallet and open the Swap section using the 'Swap' toggle in the top right corner of the screen

.. figure:: images/swaps/swap_settings.png
   :alt: Open Swap Settings

In the Litecoin section, fill in the node details, including ip:port of the node and the RPC username and password. The default fee parameter specifies the fee paid on the respective chain per Kb of transaction size and can be left at the default value.

.. note: Add description on how to calculate fees

Once the settings for the node are specified click 'Apply' and then 'Connect'

If the connection is successful the green light will be shown near the section title

.. figure:: images/swaps/connection_successful_local.png
   :alt: Connection to the node is successful


Connecting using Electrum Wallet
--------------------------------

Another simpler option to connect to a remote node using Electrum wallet service. First you need to find an address of an Electrum node, or run your own. To connect to Electrum you need to turn on the 'Electrum' toggle in the appropriate section and specify the required parameters.

.. figure:: images/swaps/electrum_settings_btc_new.png
   :alt: Connection to the Electrum wallet

At this point you need to either enter an existing seed phrase for the wallet or create a new one. 

.. note:
  If you create a wallet using official Electrum wallet software make sure you use 'Legacy' mode and not 'Segwit'

You can later edit or create new wallet at any time

.. figure:: images/swaps/electrum_settings_btc_edit.png
   :alt: Connection to the Electrum wallet


Once the seed is set you can connect to the Electrum wallet

.. figure:: images/swaps/electrum_settings_btc.png
   :alt: Connection to the Electrum wallet


Once you have connected, you should be able to see the list of wallet addresses by clicking the 'Show wallet addresses'.

.. figure:: images/swaps/electrum_wallet_addresses.png
   :alt: Electrum wallet addresses


Afer you have completed the configuiration, you are able to accept swap offers from the Atomic Swaps tab

.. figure:: images/swaps/swaps_tab.png
   :alt: Atomic swaps tab

Before we discuss how to create and accept offers we need to understand the concepts of balance and UTXO


Understanding balances and UTXOs
--------------------------------

Since Beam, Bitcoin, Litecoin and QTUM are all UTXO based cryptocurencies, understanding the difference between balance and UTXO is crucial for correct operation of the swap (and also regular) transactions.

Let's say that you see available balance of 200 Beam in your wallet and decide to swap half of it for a matching amount of Bitcoin. Once you initiate the swap, amount of free coins left in your wallet depends on the UTXOs that you had in the first place before the transcation started. 

For example, if you had one UTXO of 200 Beam, you will have 0 Beam left until the swap is completed (even though you are only actually swapping 100). If you had two UTXO, 100 each, then you will have exactly 

Creating swap offer
-------------------

Click on 'Create offer' button in the top right corner of the swaps screen to create a new offer. 

.. figure:: images/swaps/create_offer.png
   :alt: Create offer dialog

You can specify what amount and of which currency you want to trade to which amount of another currency. If you want to use the rate instead of explicitly setting the received amount, you can use the rate selector.

Once you have specified the swap details, you can either copy the swap token and send it to the opposite party using secure channel or publish the swap offer so that it can be accepted to anyone.

If you choose to publish the offer you can cancel it at any time before it was accepted by clicking Cancel on the offer. To view only your offers, click on the 'Only my offers' checkbox.


Accepting swap offer
--------------------

An Active offers table lists all currently offered swaps. The 'Send' column indicates what amount of which coin you will send in the swap and the 'Receive' column specifies what you will receive in return. 

You can select the coin you want to swap in the dropdown list in the top right part of the list, and then toggle whether you are about to send or receive Beam to see the matching offers. 

Once you have seen the offer you like, and provided you have enough funds for the swap you can click the 'Accept' button near the offer to review the swap details.

.. figure:: images/swaps/accepting_offer.png
   :alt: Accept offer

Click 'Swap' to accept the conditions and initiate the swap itself.






Afer you have completed the configuiration, you are able to create swap offers from the Atomic Swaps tab







Understanding swap transactions
-------------------------------




Atomic Swaps using Command Line Wallet
======================================


Performing atomic swap with LiteCoin
------------------------------------


To perform atomic swap between Beam and LiteCoin, Alice (who has BEAM) and Bob (who has LTC) need to follow the steps below:

1. Alice and Bob need to start full nodes for Beam and Litecoin blockchains.

Litecoin node should be configured to allow RPC access using either command line or config file as described in the `Litecoin documentation <https://litecoin.info/index.php/Litecoin.conf>`_.

In order to run Litecoin node Alice and Bob are using following command:

::
   
   $ ./litecoind -server -datadir="path_to_litecoin_wallet_data" -rpcuser=<litecoin_RPC_username> -rpcpassword=<password> -printtoconsole

Alice example:

::

   $ ./litecoind -server -datadir="Alice/path_to_litecoin_wallet_data" -rpcuser=Alice -rpcpassword=123 -printtoconsole

Bob example:

::

   $ ./litecoind -server -datadir="Bob/path_to_litecoin_wallet_data" -rpcuser=Bob -rpcpassword=123 -printtoconsole

In this example we are using standard node and RPC ports.

.. attention::
  
  The nodes should be sync up to current blockchain height before any swap operations.

In order to set up Beam node and command line wallet, please follow instructions :ref:`Command Line User Guide`


2. You can check your Litecoin balance using the following commands:
   
   ::

   $ ./litecoin-cli -rpcuser=<rpc_user_name> -rpcpassword=<password> getbalance

Alice example:

::

   $ ./litecoin-cli -rpcuser=Alice -rpcpassword=123 getbalance

Bob example:
::

   $ ./litecoin-cli -rpcuser=Bob -rpcpassword=123 getbalance



3. It doesn't matter who will run the swap first. In current case Bob starts:

::

   $ ./beam-wallet swap_init -n <beam node ip:port> --amount=<amount of Beam> -r <Alice SBBS address> --swap_coin=ltc --swap_amount=<amount of Photons> --swap_feerate=<Litecoin fee rate(Photons/Kb)> --ltc_node_addr=<litecoin node ip:rpc_port> --ltc_user=<litecoin RPC username> --ltc_pass=<litecoin RPC password>


Example:

::

  beam-wallet swap_init  -n 127.0.0.1:10005 --amount=50 -r <Alice SBBS address> --swap_coin=ltc --swap_amount=100000000  --swap_feerate=90000 --ltc_node_addr=127.0.0.1:9332 --ltc_user=Bob --ltc_pass=123


.. attention::

    Each coin has its own transaction feerate (``--swap_feerate``). To avoid failure or transaction jamming due to inconsistent fee amount, it’s recommended to check appropriate fee amount for each coin, and set it as ``--swap_feerate`` value. 

    LTC ``--swap_feerate`` = fee per 1 kb transaction size. Unlike Litecoin, Beam transaction feerate is static and doesn’t depend on transaction size. LTC value for swap amount (``--swap_amount``) is provided in “photon”, 1 LTC = 1000000 photons, BEAM value is provided in beams.

.. note::

   It’s recommended to create a new permanent SBBS address for Alice before the transaction using ``beam-wallet new_addr --expiration_time=never`` command in Beam CLI wallet.

Alice will use next command to participate in the swap:

::

   $ ./beam-wallet swap_listen --swap_coin=ltc -n <beam node ip:port> --amount=<amount of Beam> --fee=<Beam fee> --swap_amount=<amount of Photons> --swap_feerate=<Litecoin fee rate(Photons/Kb)> --ltc_node_addr=<litecoin node ip:rpc_port> --ltc_user=<litecoin RPC username> --ltc_pass=<litecoin RPC password> --swap_beam_side 

Example

::

   $ ./beam-wallet swap_listen --swap_coin=ltc -n 127.0.0.1:10005 --amount 50 --fee=100 --swap_amount=50000 ltc_node_addr 127.0.0.1:9332 --ltc_pass 123 --ltc_user Alice --swap_beam_side --swap_feerate=90000 

.. attention::

  Swap conditions such as `swap_coin`, `amount` and `swap_amount` in both Bob and Alice commands have to match each other, otherwise swap will be failed.

  ``--swap_beam_side`` flag is used to point out a party changing BEAM to LTC (in this case Alice).

4. If swap conditions match each other, a swap transaction will be created, and LTC UTXO will be locked on Bob’s blockchain.

5. Alice and Bob need to wait for 6 blocks confirmation (in Litecoin blockchain) till the coins will be unlocked.

.. note::

   Each blockchain has its own block generation time. For Litecoin average time equals 2.5 minutes, for Beam: 1 minute, for Bitcoin: 10 minutes.

6. After 6 blocks confirmation, Bob will redeem Alice’s beams and the swap will be completed.

7. Now Alice and Bob can check their Litecoin and Beam wallets accordingly to ensure the coins were transferred to them.

.. note::

    A parameter ``--swap_network=testnet`` can be used to play with the swap feature on Litecoin testnet or regtest. It is important to set the same value on BOTH sides of the swap.


Performing atomic swap with Bitcoin
------------------------------------


To perform atomic swap between Beam and Bitcoin, Alice (who has BEAM) and Bob (who has BTC) need to follow the steps below:

1. Alice and Bob need to start full nodes for Beam and Bitcoin blockchains.

Bitcoin node should be configured to allow RPC access using either command line or config file as described in the documentation `here <https://en.bitcoin.it/wiki/Running_Bitcoin>`_.

In order to run Bitcoin node Alice and Bob are using following command:

For Alice:

::

   $ ./bitcoind -server -datadir="Alice/path_to_litecoin_wallet_data" -rpcuser=Alice -rpcpassword=123 -printtoconsole

For Bob:

::

   $ ./bitcoind -server -datadir="Bob/path_to_litecoin_wallet_data" -rpcuser=Bob -rpcpassword=123 -printtoconsole

In this example we are using standard node and RPC ports.

.. attention::
  
  The nodes should be synce up to current blockchain height before any swap operations.


In order to set up Beam node and command line wallet, please follow instructions :ref:`Command Line User Guide`


2. You can check your Bitcoin balance using the following commands:

For Alice

::

   $ ./bitcoin-cli -rpcuser=Alice -rpcpassword=123 getbalance

For Bob

::

   $ ./bitcoin-cli -rpcuser=Bob -rpcpassword=123 getbalance



3. It doesn't matter who will run the swap first. In current case Bob starts:

::

   $ ./beam-wallet swap_init -n <beam node ip:port> --amount=<amount of Beam> -r <Alice SBBS address> --swap_coin=btc --swap_amount=<amount of Satoshi> --swap_feerate=<Bitcoin fee rate(Satoshi/Kb)> --btc_node_addr=<bitcoin node ip:rpc_port> --btc_user=<bitcoin RPC username> --btc_pass=<bitcoin RPC password>


Example:

::

  beam-wallet swap_init  -n 127.0.0.1:10000 --amount=50 -r <Alice SBBS address> --swap_coin=btc --swap_amount=100000000  --swap_feerate=90000 --btc_node_addr=127.0.0.1:8332 --btc_user=Bob --btc_pass=123


.. attention::

    Each coin has its own transaction feerate (``--swap_feerate``). To avoid failure or transaction jamming due to inconsistent fee amount, it’s recommended to check appropriate fee amount for each coin, and set it as ``--swap_feerate`` value. 

    BTC ``--swap_feerate`` = fee per 1 kb transaction size. Unlike Bitcoin, Beam transaction fee_rate is static and doesn’t depend on transaction size. BTC value for swap amount (``--swap_amount``) is provided in satoshi, 1 BTC = 100000000 satoshi, BEAM value is provided in beams.

.. note::

   It’s recommended to create a new permanent SBBS address for Alice before the transaction using `new_addr` command in Beam CLI wallet.

Alice will use next command to participate in the swap:

::

   $ ./beam-wallet swap_listen --swap_coin=btc -n <beam node ip:port> --amount=<amount of Beam> --fee=<Beam fee> --swap_amount=<amount of satoshi> --swap_feerate=<Bitcoin fee rate(Satoshi/Kb)> --btc_node_addr=<bitcoin node ip:rpc_port> --btc_user=<bitcoin RPC username> --btc_pass=<bitcoin RPC password> --swap_beam_side 

Example

::

   $ ./beam-wallet swap_listen --swap_coin=btc -n 127.0.0.1:10000 --amount 50 --fee=100 --swap_amount=50000 btc_node_addr 127.0.0.1:9332 --btc_pass 123 --btc_user Alice --swap_beam_side --swap_feerate=90000 

.. attention::

  Swap conditions such as `swap_coin`, `amount` and `swap_amount` in both Bob and Alice commands have to match each other, otherwise swap will be failed.

  ``--swap_beam_side`` flag is used to point out a party changing BEAM to BTC (in this case Alice).

4. If swap conditions match each other, a swap transaction will be created, and BTC UTXO will be locked on Bob’s blockchain.

5. Alice and Bob need to wait for 6 blocks confirmation (in Bitcoin blockchain) till the coins will be unlocked.

.. note::

   Each blockchain has its own block generation time. For Litecoin average time equals 2.5 minutes, for Beam: 1 minute, for Bitcoin: 10 minutes.

6. After 6 blocks confirmation, Bob will redeem Alice’s beams and the swap will be completed.

7. Now Alice and Bob can check their Litecoin and Beam wallets accordingly to ensure the coins were transferred to them.

.. note::

    A parameter ``--swap_network=testnet`` can be used to play with the swap feature on Bitcoin testnet or regtest. It is important to set the same value on BOTH sides of the swap.

