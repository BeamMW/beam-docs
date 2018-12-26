.. _user_backup_restore:


.. _backup and restore:

Backup and Restore
==================

This document lists all backup and restore procedures necessary to keep your data safe.


.. _restore desktop wallet from seed phrase:

Restore Desktop wallet from Seed Phrase
---------------------------------------

To be completed...



.. _restore cli wallet from seed phrase:

Restore CLI wallet from Seed Phrase
-----------------------------------

It is only possible to restore your coins by running your own node with your *owner key*

This process involves several steps

First you need to recreate your wallet using your :ref:`seed phrase<seed phrase>` by running the following command: 

::

    ./beam-wallet restore --wallet_phrase=<semicolod separated list of 12 seed phrase words>;

Now you need to export the owner key by running:

::

    ./beam-wallet export_owner_key

(see :ref:`exporting owner key` for more details)

Then you need to run your own node, providing the owner key as a parameter as follows:

::

    ./beam-node --peer=<ip and port of peer node> --key_owner=<owner key exported from the wallet> 

Once the node has synchronized, you need to connect your wallet to the node to update the wallet database.

To do that run the following command:

::

    ./beam-wallet listen -n <ip and port of your node, ex:127.0.0.1:10000>

After wallet syncrhonizes, use `info` command to check wallet status

:: 

    ./beam-wallet info