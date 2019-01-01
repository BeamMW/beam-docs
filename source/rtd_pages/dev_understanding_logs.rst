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

A log will start with the Rules signature. Rules signature is the hash of the Consensus Rules and it should be compatible with the network you are connecting to. It will be different between the Testnet and Mainnet. The relevant Rules signature for each network can be seen here: :ref: `rules_signature`

Beam Logs have a simple structure. First field is the severity level, followed by a timestamp and the log message. 

Log Severity 
+--------------------+-----------------+
| I                  | Info            |
+--------------------+-----------------+
| W                  | Warning         |
+--------------------+-----------------+
| E                  | Error           |
+--------------------+-----------------+
| D                  | Debug           |
+--------------------+-----------------+

The sample below shows a start of the new node

::

	I 2018-12-31.16:48:58.838 Rules signature: 7e16d65b64ef2fbb
	I 2018-12-31.16:48:58.986 starting a node on 10000 port...
	I 2018-12-31.16:48:58.996 Node ID=5c8f92a1cfaee337
	I 2018-12-31.16:48:58.996 Initial Tip: 0-0000000000000000
	I 2018-12-31.16:48:58.996 Requesting block 0-0000000000000000
	I 2018-12-31.16:48:58.997 PI 0000000000000000--0.0.0.0 New
	I 2018-12-31.16:48:58.997 PI 0000000000000000--0.0.0.0 Address changed to 23.239.24.209:8201
	I 2018-12-31.16:48:58.999 stratum server listens to 0.0.0.0:10002


The node connects to the first peer, in this case 23.239.24.209:8201 and downloads the initial Tip at hight 0. It then requests the matching block. In this specific example the node also starts the Stratum server.




CLI Wallet logs
---------------



Desktop Wallet logs
-------------------




