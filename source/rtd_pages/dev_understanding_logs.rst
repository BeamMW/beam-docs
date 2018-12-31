.. _dev_understanding_logs:

.. warning:: The following document is still under construction and is subject to changes

Understanding Beam logs
==========================


.. _log locations:

Log locations
-------------

For CLI wallet and Node logs are usually located in the same folder as the binary file.

For Desktop Wallet logs are located in the following folders:



:fa:`apple` Mac: /Users/{your_user_name}/Library/Application Support/Beam Wallet/

:fa:`windows` Windows: :\\Users\\{your_user_name}\\AppData\\Local\\Beam Wallet

:fa:`linux` Linux: /home/{your_user_name}/.local/share/Beam Wallet

For a complete list of file locations see :ref: `Files and Locations`


Node logs
---------

A log will start with the Rules signature. Rules signature is the hash of the Consensus Rules and it should be compatible with the network you are connecting to. It will be different between the Testnet and Mainnet. The relevant Rules signature for each network can be seen here: `rules_signature`_



Wallet logs
-----------
