.. _user_local_setup:

Local Setup
===========


Starting a new network
----------------------

To start a new Beam Network follow the steps below:

1. Download or build Beam binaries for node and CLI wallet

From this point the folders containing node and wallet binaries will be called 'node folder' and 'wallet folder' respectively

2. Initialize new wallet by running the following command in the wallet folder:

::

	./beam-wallet init

See :ref:`creating_new_cli_wallet` for more details

3. Export miner key, by running the following command in the wallet folder:

::

	./beam-wallet export_miner_key --subkey=1

.. note:: If you are running more than one mining node repeat step 3 with --subkey=N (where N is the id of the nodes 1,2,3...)

4. Export owner key by running the following command in the wallet folder:

::

	./beam-wallet export_owner_key

5. Locate sample Beam treasury file treasury.bin (it is located in the root of Beam source folder) and copy it to the same folder as beam-node binary.

6. Launch Node0 using the following command:

::

	./beam-node 