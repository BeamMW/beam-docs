.. _user_files_and_locations:


.. _files and locations:

Files and Locations
===================

Desktop Wallet app
------------------

General points to mention:

* The default location of the Desktop Wallet app can be modified during the installation process (Windows only).
* The default Database location for the Desktop Wallet app can be changed setting the `appdata` parameter to `beam-wallet.cfg` (Windows only).
* Memory dump files are generated on Windows only. A dedicated memory dump file is created per each crash case.
* Each version of the wallet keeps the wallet database file (`wallet.db`) in the dedicated sub-folder, designated by the version number. On each wallet update the new folder is created to which and the wallet database file from previous version is copied into (and updated if necessary).

Windows
-------

+-------------------------+---------------------------------------------------------------------------------------------+
| **File**                | **Location**                                                                                |
+-------------------------+---------------------------------------------------------------------------------------------+
| Main Executable         | `\\Program Files\\Beam Wallet\\Beam Wallet.exe`                                             |
+-------------------------+---------------------------------------------------------------------------------------------+
| Configuration           | `\\Program Files\\Beam Wallet\\beam-wallet.cfg`                                             |
+-------------------------+---------------------------------------------------------------------------------------------+
| Logs                    | `\\Users\\{your User name}\\AppData\\Local\\Beam Wallet\\logs`                              |
+-------------------------+---------------------------------------------------------------------------------------------+
| Database                | `\\Users\\{your User name}\\AppData\\Local\\Beam Wallet\\<version>\\wallet.db`              |
|                         |                                                                                             |
|                         | `\\Users\\{your User name}\\AppData\\Local\\Beam Wallet\\node.db`                           |
+-------------------------+---------------------------------------------------------------------------------------------+
| Settings                | `\\Users\\{your User name}\\AppData\\Local\\Beam Wallet\\settings.ini`                      |
+-------------------------+---------------------------------------------------------------------------------------------+
| Dumps                   | `\\Users\\{your User name}\\AppData\\Local\\Beam Wallet\\Beam Wallet.exe0.dmp`              |
+-------------------------+---------------------------------------------------------------------------------------------+

Mac
---

+-------------------------+--------------------------------------------------------------------------------------------+
| **File**                | **Location**                                                                               |
+-------------------------+--------------------------------------------------------------------------------------------+
| Main Executable         | `/Applications/Beam Wallet.app`                                                            |
+-------------------------+--------------------------------------------------------------------------------------------+
| Configuration           | N/A                                                                                        |
+-------------------------+--------------------------------------------------------------------------------------------+
| Logs                    | `/Users/{your User name}/Library/Application Support/Beam Wallet/logs`                     |
+-------------------------+--------------------------------------------------------------------------------------------+
| Database                | `/Users/{your User name}/Library/Application Support/Beam Wallet/<version>/wallet.db`      |
|                         |                                                                                            |
|                         | `/Users/{your User name}/Library/Application Support/Beam Wallet/node.db`                  |
+-------------------------+--------------------------------------------------------------------------------------------+
| Settings                | `/Users/{your User name}/Library/Application Support/Beam Wallet/settings.ini`             |
+-------------------------+--------------------------------------------------------------------------------------------+

Linux
-----

+-------------------------+----------------------------------------------------------------------------------+
| **File**                | **Location**                                                                     |
+-------------------------+----------------------------------------------------------------------------------+
| Main Executable         | `/usr/bin/BeamWallet`                                                            |
+-------------------------+----------------------------------------------------------------------------------+
| Configuration           | `/usr/bin/beam-wallet.cfg`                                                       |
+-------------------------+----------------------------------------------------------------------------------+
| Logs                    | `/home/{your User name}/.local/share/Beam Wallet/logs`                           | 
+-------------------------+----------------------------------------------------------------------------------+
| Database                | `/home/{your User name}/.local/share/Beam Wallet/<version>/wallet.db`            |
|                         |                                                                                  |
|                         | `/home/{your User name}/.local/share/Beam Wallet/node.db`                        |
+-------------------------+----------------------------------------------------------------------------------+
| Settings                | `/home/{your User name}/.local/share/Beam Wallet/settings.ini`                   |
+-------------------------+----------------------------------------------------------------------------------+


Node or CLI wallet
------------------

All Platforms (small differences apply, see below)

User can unpack the archive in any folder to his convenience. All files mentioned below are located within this folder

+-------------------------+----------------------------------------------------------------------------------+
| **File**                | **Location**                                                                     |
+-------------------------+----------------------------------------------------------------------------------+
| Main Executable         | `beam-node` or `beam-wallet`                                                     |
+-------------------------+----------------------------------------------------------------------------------+
| Configuration           | `beam-node.cfg` or `beam-wallet.cfg`                                             |
+-------------------------+----------------------------------------------------------------------------------+
| Logs                    | logs                                                                             | 
+-------------------------+----------------------------------------------------------------------------------+
| Database                | `node.db` or `wallet.db`                                                         |
+-------------------------+----------------------------------------------------------------------------------+
| Dumps (windows only)    | `beam-node.exe0.dmp`                                                             |
+-------------------------+----------------------------------------------------------------------------------+


