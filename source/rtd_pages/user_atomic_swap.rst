.. _user_atomic_swap:
.. _user_atomic_swap:

Atomic swap
=========================

The idea of atomic swap was presented as solution for the next problem: two parties (Alice and Bob) want to exchange their coins without having to trust third party.

In a simplified way non-atomic approach consists of four steps:

1. Alice send her ACoins to Bob.
2. Bob receives ACoins.
3. Bob sends his BCoins to Alice.
4. Alice receives BCoins. 


The weakest part of this such approach is lurking in step #3. By malicious intent, Bob can avoid following his part of the agreement.
Atomic swap is provided to guarantee compliance of the agreement.

.. note::

   Atomic swap is available at Beam CLI wallet version 2.2.5635 or higher.

.. attention::

   You need to perform atomic swap with a person you trust.

Creating atomic swap transaction (LiteCoin example)
---------------------------------------------------

.. attention::

   For Litecoin atomic swap litecoin `v0.17.1 <https://litecoin.org/#download>`_ should be used.

To perform atomic swap between Beam and LiteCoin, Alice (BEAM) and Bob (LTC) need to follow the steps below:

1. Alice and Bob need to start nodes for Beam and Litecoin blockchains.
In order to run Litecoin node Alice and Bob are using following command:

For Alice:

::

   $ ./litecoind -server -datadir="Alice/path_to_litecoin_wallet_data" -port=10000
   -rpcuser=Alice -rpcpassword=123 -printtoconsole

For Bob:

::

   $ ./litecoind -server -datadir="Bob/path_to_litecoin_wallet_data" -port=10005
-rpcuser=Bob -rpcpassword=123 -printtoconsole

In order to run Beam node please see "Run Beam Node".


2. Now Alice and Bob need to check their Litecoin balance using the following commands:

For Alice

::

   $ ./litecoin-cli -rpcuser=Alice -rpcpassword=123 getbalance

For Bob

::

   $ ./litecoin-cli -rpcuser=Bob -rpcpassword=123 getbalance

4. It doesn't matter who will run the swap first. In current case Bob starts:

::

   $ ./beam-wallet swap_init --swap_coin=ltc -n 127.0.0.1:10005 --amount 50 -r <Alice_address> --swap_amount 100000000 --ltc_node_addr 127.0.0.1:9332 --ltc_user Bob --swap_feerate=90000


.. attention::

    Each coin has its own transaction fee (-swap_feerate). To avoid failure or transaction jamming due to inconsistent fee amount, it’s recommended to check appropriate fee amount for each coin, and set it as --swap_feerate value. LTC --swap_feerate = fee per 1 kb U+002A transaction size. Unlike Litecoin, Beam transaction fee_rate is static and doesn’t depend on transaction size. LTC value for swap amount (--swap_amount) is provided in “photon”, 1 LTC = 1000000 photons, BEAM value is provided in beams.

.. note::

   It’s recommended to create a new permanent Beam wallet address for Alice before the transaction.

Alice will use next command to participate in the swap:

::

   $ ./beam-wallet swap-listen --swap_coin=ltc -n 127.0.0.1:10000 --amount 50 --swap_amount=50000 ltc_node_addr 127.0.0.1:9332 --ltc_pass 123 --ltc_user Alice --swap_beam_side --swap_feerate=90000  --swap_beam_side

.. attention::

    Swap conditions in both Bob and Alice commands have to match each other, otherwise swap will be failed.

    ``--swap_beam_side`` flag is used to point out a party changin BEAM to LTC

5. If swap conditions match each other, a swap transaction will be created, and LTC UTXO will be locked on Bob’s blockchain.

6. Alice and Bob need to wait for 6 blocks confirmation (in each blockchain) till the coins will be unlocked.

.. note::

   Each blockchain has its own block generation time. For Litecoin average time equals 2.5 minutes, for Beam: 1 minute, for Bitcoin: 10 minutes.

7. After 6 blocks confirmation, Bob will redeem Alice’s beams and the swap will be completed.

8. Now Alice and Bob can check their Litecoin and Beam wallets accordingly to ensure the coins were transferred to them.
