.. _user_atomic_swap:

Atomic swap
=========================

The idea of atomic swap was presented as the solution for the next problem: two parties (Alice and Bob) want to exchange their coins without having to trust а third party.

In a simplified way non-atomic approach consists of four steps:

1. Alice sends her A Coins to Bob.
2. Bob receives A Coins.
3. Bob sends his B Coins to Alice.
4. Alice receives B Coins. 


The weakest part of this approach is lurking in step #3. By malicious intent, Bob can avoid following his part of the agreement.
Atomic swap is provided to guarantee the compliance of the agreement.

.. note::

   Atomic swap is available at Beam CLI wallet version 2.2.5635 or higher.

   For Bitcoin use version `Bitcoin Core v0.17.1 <https://bitcoin.org/en/download>`_ .

   For Litecoin use version `Litecoin v0.17.1 <https://litecoin.org/#download>`_ .


Performing atomic swap with LiteCoin
------------------------------------


To perform atomic swap between Beam and LiteCoin, Alice (who has BEAM) and Bob (who has LTC) need to follow the steps below:

1. Alice and Bob need to start full nodes for Beam and Litecoin blockchains.

Litecoin node should be configured to allow RPC access using either command line or config file as described in the documentation `here <https://litecoin.info/index.php/Litecoin.conf>`_.

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
  
  The nodes should be synced up to current blockchain height before each swap operation.

In order to set up Beam node and command line wallet, please follow instructions :ref:`Command Line User Guide`


2. You can check your Litecoin balance using the following command:
   
   ::

   $ ./litecoin-cli -rpcuser=<rpc_user_name> -rpcpassword=<password> getbalance

Alice example:

::

   $ ./litecoin-cli -rpcuser=Alice -rpcpassword=123 getbalance

Bob example:
::

   $ ./litecoin-cli -rpcuser=Bob -rpcpassword=123 getbalance



3. It doesn't matter who runs the swap first. In current case Bob starts:

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

