.. _lelantus&onesidedpayment:

.. _lelantus :

LelantusMW Shielded Pool
========================


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
=================

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
  




