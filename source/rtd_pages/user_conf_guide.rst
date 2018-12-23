:orphan:

.. _beam_conf_guide:

Beam Configuration
================


General
------------------------

The following parameters are common to both Beam Node and Beam Wallet

+-------------------------+----------------------------------------------------------------------------------------------------------+
|**Parameter**            | **Description & Example**                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| port                    | Port to start the server on                                                                              |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    port=10000                                                                                            |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| log_level               | Log level [info|debug|verbose]                                                                           |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    log_level=info                                                                                        |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| file_log_level          | File log level [info|debug|verbose]                                                                      |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    file_log_level=info                                                                                   |
+-------------------------+----------------------------------------------------------------------------------------------------------+


Node Settings
------------------------


+-------------------------+----------------------------------------------------------------------------------------------------------+
|**Parameter**            | **Description & Example**                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| storage                 | Path to node database file (defaults to node.db in the same folder)                                      |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    storage=node.db                                                                                       |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| history_dir             | Path to folder where compressed (cut-through) history files are stored. Defaults to same folder.         |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    history_dir=. 																						 |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| temp_dir                | Path to temp folder for compressed (cut-through) history files. Must be on the same volume as history_dir|
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    temp_dir=.                                                                                            |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| miner_type              | Type of built in miner [cpu|gpu]. Only relevant for Linux and Windows builds which support GPU mining.   |
|                         | In case of CPU mining uses number of threads specified in the mining_threads parameter (see below).      |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    miner_type=cpu                                                                                        |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| mining_threads          | Number of concurrent threads used in CPU mining (if set to 0, mining is disabled)                        |
|                         | Relevant for CPU mining only                                                                             |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    mining_threads=0                                                                                      |
+-------------------------+----------------------------------------------------------------------------------------------------------+

.. admonition:: Using CPU mining is not recommended

   Beam uses Equihash mining algorith with (150,5) parameters and customized data path. It is efficiently mined on GPUs. Using CPU is most likely to be not cost effective.

+-------------------------+----------------------------------------------------------------------------------------------------------+
|**Parameter**            | **Description & Example**                                                                                |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| key_mine                | Secret key to attribute mining rewards to your wallet                                                    |
|                         | Created using CLI walelt `key_export` command with --subkey=<miner id> parameter                         |
|                         | See :ref:`development_guidelines` for more details                                                            |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    storage=node.db                                                                                       |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| history_dir             | Path to folder where compressed (cut-through) history files are stored. Defaults to same folder.         |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    history_dir=. 																						 |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| temp_dir                | Path to temp folder for compressed (cut-through) history files. Must be on the same volume as history_dir|
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    temp_dir=.                                                                                            |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| miner_type              | Type of built in miner [cpu|gpu]. Only relevant for Linux and Windows builds which support GPU mining.   |
|                         | In case of CPU mining uses number of threads specified in the mining_threads parameter (see below).      |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    miner_type=cpu                                                                                        |
+-------------------------+----------------------------------------------------------------------------------------------------------+
| mining_threads          | Number of concurrent threads used in CPU mining (if set to 0, mining is disabled)                        |
|                         | Relevant for CPU mining only                                                                             |
|                         |                                                                                                          |
|                         | .. code-block:: bash                                                                                     |
|                         |                                                                                                          |
|                         |    mining_threads=0                                                                                      |
+-------------------------+----------------------------------------------------------------------------------------------------------+