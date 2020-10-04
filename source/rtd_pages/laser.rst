Laser Beam
==========

Introduction
------------

Laser Beam is an implementation of direct payment channels between two Beam wallets. As of now this feature is only implemented in Beam CLI wallets. 

When channel is opened each party commits some amount of Beam into the channel. Then it is possible to perform instant transactions between the wallets with values within the locked sum. When the channel is closed the last state of the channel is committed on chain. 

Create channel
--------------

Alice and Bob must agree on the amount to be blocked for options

+--------------------------------------------------+-----------------------------------------------+
| **Alice's side**                                 | **Bob’s side**                                |
+==================================================+===============================================+
| laser_my_locked_amount 1(amount of Alice)        | laser_my_locked_amount 2(amount of Bob)       |
|                                                  |                                               |
| laser_remote_locked_amount 2(amount of Bob)      | laser_remote_locked_amount 1(amount of Alice) |
|                                                  |                                               |
| laser_fee 100 (should be identical)              | laser_fee 100 (should be identical)           |
+--------------------------------------------------+-----------------------------------------------+

To open a lasser channel between Alice's and Bob's wallets follow these
steps

1. To create channel, Alice uses the following command
::
   
   $ ./beam-wallet laser --laser_receive --laser_my_locked_amount <amount in beam> --laser_remote_locked_amount <amount in beam> --laser_fee <amount in groth

Example:

::
  
   $ ./beam-wallet-masternet.exe laser --laser_receive --laser_my_locked_amount 1 --laser_remote_locked_amount 2 --laser_fee 100 -n 127.0.0.1:1000
  
Alice's wallet generates a new address and she send’s it to Bob

::

    I 2020-06-04.13:23:35.342 Beam Wallet 
    I 2020-06-04.13:23:35.343 Rules signature: 0-5547a592195f4cd4, 10-2fdbbbb74ac57c55, 20-67131c58aa9a6b85
    Enter password: *
    I 2020-06-04.13:23:36.039 wallet sucessfully opened...
    I 2020-06-04.13:23:36.260 New address generated:

    333133cddf316e40f3352e9dae6bae568e97052c1b73531b263a695170658cd13e6 
  
2. To open channel, Bob uses the following command and inserts Alice's
address in the option «laser_address»

::

    $ ./beam-wallet laser --laser_open --laser_address <address> --laser_my_locked_amount <amount in beam> --laser_remote_locked_amount <amount in beam> --laser_fee <amount in groth>

Example:

::

    $ ./beam-wallet laser --laser_open --laser_address 333133cddf316e40f3352e9dae6bae568e97052c1b73531b263a695170658cd13e6 --laser_my_locked_amount 2 --laser_remote_locked_amount 1 --laser_fee 100 -n 127.0.0.1:1000

If Bob incorrectly entered the values in the channel opening options, then Alice will see the message  "Incoming connection with incorrect …"              

3. Сhannel will be opened and a table with the open channel will appear.

Alice’s side

::

    Laser Channels:
    channel Id                        |aMy    |aTrg     |state     |fee       |valid till
    7a0f1a491fe95f3fe453a298dd62ba12  |1      |2        |Open      |0.000001  |55966

Bob’s side

::

    Laser Channels:
    channel Id                        |aMy    |aTrg     |state     |fee       |valid till
    7a0f1a491fe95f3fe453a298dd62ba12  |2      |1        |Open      |0.000001  |55966

Sending BEAMs
-------------

Alice and Bob use an open channel to send beams

1. Bob should listen to this channel using the following command

::

    $ ./beam-wallet laser --laser_listen [channel id 1,channel id 2, ... channel id N]

Example:

::

    $ ./beam-wallet laser --laser_listen 7a0f1a491fe95f3fe453a298dd62ba12 -n 127.0.0.1:1000»

2. To send coins Alice uses the following command:

::

    $ ./beam-wallet-masternet laser --laser_send <amount in beam> --laser_channel <channel id>

Example:

::

    $ ./beam-wallet laser --laser_send 0.2 --laser_channel 7a0f1a491fe95f3fe453a298dd62ba12 -n 127.0.0.1:1000

3. When the transfer is completed, you will receive a message about
changing your channel balance

Alice’s side

::

    D 2020-06-04.14:19:35.166 ### Bbs mesage out ###
    D 2020-06-04.14:19:35.166 Channel:7a0f1a491fe95f3fe453a298dd62ba12 state Open. Last Revision: 2. My balance: 220000000 / Total balance: 300000000
    D 2020-06-04.14:19:35.167 Save channel: 7a0f1a491fe95f3fe453a298dd62ba12
    I 2020-06-04.14:19:35.200 Update finished: 7a0f1a491fe95f3fe453a298dd62ba12
    D 2020-06-04.14:19:35.487 OnMined() diff: 0
    D 2020-06-04.14:19:35.488 Receiver::OnComplete

Bob’s side

::

    D 2020-06-04.14:19:35.166 ### Bbs mesage out ###
    D 2020-06-04.14:19:35.166 Channel:7a0f1a491fe95f3fe453a298dd62ba12 state Open. Last Revision: 2. My balance: 220000000 / Total balance: 300000000
    D 2020-06-04.14:19:35.167 Save channel: 7a0f1a491fe95f3fe453a298dd62ba12
    I 2020-06-04.14:19:35.200 Update finished: 7a0f1a491fe95f3fe453a298dd62ba12
    D 2020-06-04.14:19:35.487 OnMined() diff: 0
    D 2020-06-04.14:19:35.488 Receiver::OnComplete

Channels list
-------------

To see a list of all open channels and checks for balance changes, use
the following command:

::

    $ ./beam-wallet laser --laser_channels_list »

The wallet log should look similar to something like:

::

    Laser Channels:

    channel Id                        |aMy       |aT        |state     |fee       |valid till
    7a0f1a491fe95f3fe453a298dd62ba12  |2.2       |0.8       |Open      |0.000001  |57464
    b9236abe78ab5747ca955189df079d2b  |1.0000005 |1.0000005 |Closed    |0.000001  |0

Close channel
-------------

To close channel, use the following commands

+----------------+--------------------------------------------------------+
| laser_close   | before lock time is up, only if other side is online    |
+================+========================================================+
| Laser_drop    |  after lock time is up or if other side is offline      |
+----------------+--------------------------------------------------------+

1. Bob should listen to this channel using the following command

::

    $ ./beam-wallet laser --laser_listen 7a0f1a491fe95f3fe453a298dd62ba12 -n 127.0.0.1:1000


2. To close channel, Alice uses the following command

::

    $./beam-wallet laser --laser_close <channel id 1,channel id 2, ... channel id N
    
Example:

::

    $ ./beam-wallet laser --laser_close 7a0f1a491fe95f3fe453a298dd62ba12 -n 127.0.0.1:1000 

::

    $. /beam-wallet laser --laser_close 7a0f1a491fe95f3fe453a298dd62ba12, 4bd5ee31b264f6102709dc145cf37b5 -n 127.0.0.1:1000
    
.. note:: If you use «laser_close» and the 2nd side was not online, your channel will return to the open status . Then you can use the «laser_drop» command

::

    $ ./beam-wallet laser --laser_drop <channel id 1,channel id 2, ... channel id N

Example:
::

    $ ./beam-wallet laser --laser_drop 7a0f1a491fe95f3fe453a298dd62ba12 -n 127.0.0.1:1000
    
::

    $ ./beam-wallet laser --laser_drop 7a0f1a491fe95f3fe453a298dd62ba12, 4bd5ee31b264f6102709dc145cf37b5 -n 127.0.0.1:1000

.. note:: Using «laser_drop» command, the channel will close after 1440 blocks

Delete channel
--------------

To delete a channel from the wallet database, use the following command:

::

    $ ./beam-wallet-masternet laser --laser_delete <channel id 1,channel id 2, ... channel id N

Example:

::

    $ ./beam-wallet laser --laser_delete 7a0f1a491fe95f3fe453a298dd62ba12 -n 127.0.0.1:1000

You can delete channel only after the channel gets the "closed" status and passes > 1440

.. note:: Channels with the “Waiting” and “OpenFailed” status can be deleted immediately
