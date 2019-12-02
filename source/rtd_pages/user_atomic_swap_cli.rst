.. _user_atomic_swap_cli:

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

   
   
3. Initialize swap settings:

::

   $ ./beam-wallet set_swap_settings --swap_coin=ltc --swap_wallet_addr=<litecoin node ip:rpc_port> --swap_wallet_user=<litecoin RPC username> --swap_wallet_pass=<litecoin RPC password> --swap_feerate=<Litecoin fee rate(Photons/Kb)> --active_connection=core
   
Alice example:

::

   $ ./beam-wallet set_swap_settings --swap_coin=ltc --swap_wallet_addr=127.0.0.1:13300 --swap_wallet_user=Alice --swap_wallet_pass=123 --swap_feerate=90000 --active_connection=core
   
Bob example:

::

   $ ./beam-wallet set_swap_settings --swap_coin=ltc --swap_wallet_addr=127.0.0.1:13400 --swap_wallet_user=Bob --swap_wallet_pass=123 --swap_feerate=90000 --active_connection=core
   
   
.. attention::

    Each coin has its own transaction feerate (``--swap_feerate``). To avoid failure or transaction jamming due to inconsistent fee amount, it’s recommended to check appropriate fee amount for each coin, and set it as ``--swap_feerate`` value. 

    LTC ``--swap_feerate`` = fee per 1 kb transaction size. Unlike Litecoin, Beam transaction feerate is static and doesn’t depend on transaction size. LTC value for swap amount (``--swap_amount``) is provided in “photon”, 1 LTC = 1000000 photons, BEAM value is provided in beams.
  


4. It doesn't matter who will run the swap first. In current case Bob starts:

::

   $ ./beam-wallet swap_init -n <beam node ip:port> --amount=<amount of Beam> --swap_coin=ltc --swap_amount=<amount of Photons> --swap_beam_side

.. attention::

  ``--swap_beam_side`` flag is used to point out a party changing BEAM to LTC (in this case Alice).   

   
.. note::

   The result of the swap_init command is a swap token.  


Example:

::

  $ ./beam-wallet swap_init  -n "eu-node01.mainnet.beam.mw:8100" --amount=10 --swap_coin=ltc --swap_amount=2000000000


Bob copys swap token from console and send it to Alice. After that Bob should run wallet with listen command.

Example:

::

   $ ./beam-wallet listen -n "eu-node01.mainnet.beam.mw:8100"
  

Alice will use next command to participate in the swap:

::

   $ ./beam-wallet swap_accept  -n <beam node ip:port> --swap_token=<Bob's swap token>

Example:
   
::

   $ ./beam-wallet swap_accept  -n "eu-node01.mainnet.beam.mw:8100" --swap_token=316sveQtJrhxzuBy2zJHTp8aHfPgdz2FycrR8n9fs5CbXqoq1Be4Z9qEPnz5HjxuBZgmQpxWd8Dy9icQYKVn1e23cP7x5FHcteyEXk11QQ6CQLQJ3ERk653xgzXnBNfiiX8Pw8acyuNqCHPsF699oiDkxgEAXtV5mrKmYWh1zW



5. If Alice accepts swap conditions, a swap transaction will be created, and LTC UTXO will be locked on Bob’s blockchain.

6. Alice and Bob need to wait for 6 blocks confirmation (in Litecoin blockchain) till the coins will be locked.

.. note::

   Each blockchain has its own block generation time. For Litecoin average time equals 2.5 minutes, for Beam: 1 minute, for Bitcoin: 10 minutes.

7. After 6 blocks confirmation, Bob will redeem Alice’s beams and will reveal secret. After that the swap will be completed for Bob.

8. Alice will redeem Bob's litecoins using secret. After that the swap will be completed for Alice.

9. Now Alice and Bob can check their Litecoin and Beam wallets accordingly to ensure the coins were transferred to them.



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



3. Initialize swap settings:

::

   $ ./beam-wallet set_swap_settings --swap_coin=btc --swap_wallet_addr=<bitcoin node ip:rpc_port> --swap_wallet_user=<bitcoin RPC username> --swap_wallet_pass=<bitcoin RPC password> --swap_feerate=<Bitcoin fee rate(Satoshs/Kb)> --active_connection=core
   
Alice example:

::

   $ ./beam-wallet set_swap_settings --swap_coin=btc --swap_wallet_addr=127.0.0.1:13300 --swap_wallet_user=Alice --swap_wallet_pass=123 --swap_feerate=90000 --active_connection=core
   
Bob example:

::

   $ ./beam-wallet set_swap_settings --swap_coin=ltc --swap_wallet_addr=127.0.0.1:13400 --swap_wallet_user=Bob --swap_wallet_pass=123 --swap_feerate=90000 --active_connection=core
   
   
.. attention::

    Each coin has its own transaction feerate (``--swap_feerate``). To avoid failure or transaction jamming due to inconsistent fee amount, it’s recommended to check appropriate fee amount for each coin, and set it as ``--swap_feerate`` value. 

    BTC ``--swap_feerate`` = fee per 1 kb transaction size. Unlike Bitcoin, Beam transaction feerate is static and doesn’t depend on transaction size. BTC value for swap amount (``--swap_amount``) is provided in “satoshi”, 1 BTC = 1000000 photons, BEAM value is provided in beams.
  


4. It doesn't matter who will run the swap first. In current case Bob starts:

::

   $ ./beam-wallet swap_init -n <beam node ip:port> --amount=<amount of Beam> --swap_coin=btc --swap_amount=<amount of Satoshi> --swap_beam_side

.. attention::

  ``--swap_beam_side`` flag is used to point out a party changing BEAM to BTC (in this case Alice).   

   
.. note::

   The result of the swap_init command is a swap token.  


Example:

::

  $ ./beam-wallet swap_init  -n "eu-node01.mainnet.beam.mw:8100" --amount=10 --swap_coin=btc --swap_amount=100000000


Bob copys swap token from console and send it to Alice. After that Bob should run wallet with listen command.

Example:

::

   $ ./beam-wallet listen -n "eu-node01.mainnet.beam.mw:8100"
  

Alice will use next command to participate in the swap:

::

   $ ./beam-wallet swap_accept  -n <beam node ip:port> --swap_token=<Bob's swap token>

Example:
   
::

   $ ./beam-wallet swap_accept  -n "eu-node01.mainnet.beam.mw:8100" --swap_token=316w4oB5hCz2qeVNrtteAEZXhxxx2HBX8v1Ped1FhveJor5JbChz2xXGfi2LkKqVLu8kU4vEoZCV3UbmwoBZX2ABJzmbxLPxpCTVZr1oefwsJDzYU2BUXXDTf4VjtBJfsP3yrozPT4bz1ZTdDTzRS2yU3VYvnamuSRSfEPatha



5. If Alice accepts swap conditions, a swap transaction will be created, and BTC UTXO will be locked on Bob’s blockchain.

6. Alice and Bob need to wait for 6 blocks confirmation (in Bitcoin blockchain) till the coins will be locked.

.. note::

   Each blockchain has its own block generation time. For Bitcoin average time equals 2.5 minutes, for Beam: 1 minute, for Bitcoin: 10 minutes.

7. After 6 blocks confirmation, Bob will redeem Alice’s beams and will reveal secret. After that the swap will be completed for Bob.

8. Alice will redeem Bob's bitcoins using secret. After that the swap will be completed for Alice.

9. Now Alice and Bob can check their Bitcoin and Beam wallets accordingly to ensure the coins were transferred to them.

