.. _web_wallet:

.. _web wallet:


Web Wallet (Testnet) User Guide
===============================


.. note::

  Known limitations:

  * Web Wallet is used only for Testnet.
  * Web Wallet doesn’t support old SBBS addresses for transactions, only new type of  addresses.
  * The restore from seed phrase is yet to be implemented
  * Only single-use addresses are supported: once issued, the address will remain active for 12 hours.


How to install Beam Web Wallet
------------------------------


User can download Web wallet from [Chrome Webstore] (https://chrome.google.com/webstore/detail/beam-web-wallet-testnet/ilhaljfiglknggcoegeknjghdgampffk?utm_source=chrome-ntp-icon) 


.. figure:: images/web_wallet/01_install.png
   :alt: Download Web wallet

or load unpacked extension here chrome://extensions/ (to download packed extension, please, check our [Github] (https://github.com/BeamMW/web-wallet/releases) ) 


.. figure:: images/web_wallet/02_install.png
   :alt: Chrome Extension
      

.. figure:: images/web_wallet/03_install.png
   :alt: Download Web wallet

Creating new wallet
-------------------

There are two ways of how user can create new wallet: ::ref:`Easy onboarding` and ::ref:`Create a new wallet with seed phrase`

.. _easy_onboarding: 

Easy onboarding
---------------

The easiest way. After installation and clicking on the button “Create new wallet”, a user can skip the step about verifying seed by clicking on “I will do it later”. Take a look at the following screenshots. 


.. figure:: images/web_wallet/easy_onboarding/01.png
   :alt: Creating page


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/01.png
   :alt: Creating page
   

.. figure:: images/web_wallet/easy_onboarding/02.png
   :alt:  Before generating seed phrase


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/02.png
   :alt: Before generating seed phrase
   

.. attention:: Seed phrase in the Beam wallet is *not* linked to email, phone number or any other identifier. You will need this phrase to restore your wallet when you lose or reformat your device, or want to access your funds from another device.


.. figure:: images/web_wallet/easy_onboarding/03.png
   :alt:  Generating seed phrase


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/03.png
   :alt: Generating seed phrase
   
On the next step user needs to enter a password for his wallet and confirm it. This password is not the same as the seed phrase. Seed phrase identifies a wallet and enables access to all the funds stored in Beam blockchain from any device. Your wallet password provides with a second security layer in case someone gains access to your computer or has stolen your wallet database file. 

.. figure:: images/web_wallet/easy_onboarding/04.png
   :alt:  Creating a password


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/04.png
   :alt: Creating a password
   

It is important to choose a strong password. The wallet will provide some indication of password strength for your convenience. Do not count on it, however. Choose a password that is at least 8 characters long with a combination of letters, numbers, and symbols.


.. figure:: images/web_wallet/easy_onboarding/05.png
   :alt:  Creating with a strong password
   

The screen with the loading bar is opened. It takes a few seconds/minutes (depends on your connection) to finish the creation of the wallet.


.. figure:: images/web_wallet/easy_onboarding/06.png
   :alt:  Creating screen with loading bar


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/05.png
   :alt: Creating screen with loading bar
   

Once your wallet is created, the main screen will show up.

.. figure:: images/web_wallet/easy_onboarding/07.png
   :alt:  Main screen


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/06.png
   :alt: Main screen
   

Create a new wallet with the seed phrase verification
-----------------------------------------------------

Once you launch the wallet for the first time, click the ‘Create new wallet’ button.

.. figure:: images/web_wallet/easy_onboarding/01.png
   :alt: Creating page


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/01.png
   :alt: Creating page
   

As a part of creating a new wallet, a new seed phrase will be generated for you.

Attention
Seed phrase is the most important secret you have to keep. Knowing the seed phrase enables you (or anyone else) to access all your funds.


.. figure:: images/web_wallet/easy_onboarding/02.png
   :alt:  Before generating seed phrase


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/02.png
   :alt: Before generating seed phrase
   


.. attention:: Did you wrote down your seed phrase correctly? Triple-check your handwriting again. The difference between _F_unnel and _T_unnel can be crucial when trying to restore a wallet with valuable funds in the far or near future.
Did you verified your handwriting? Now go find a safe space for the paper!


.. figure:: images/web_wallet/easy_onboarding/03.png
   :alt:  Generating seed phrase


For the extension view:

.. figure:: images/web_wallet/easy_onboarding/extension_view/03.png
   :alt: Generating seed phrase
   
.. important:: Storing the seed phrase on your computer makes your funds prone to cyber attacks (read: much *less* secure). 'Creative' approaches like saving a screenshot of the wallet or your handwriting on your computer or in the cloud *may* sound like a good idea, but it is absolutely **not recommended**. If hackers get the access to your computer, network drive etc., they can can potentially steal your seed phrase by using OCR programs (which can scan pictures and transform them into plain text) and, therefore, get access to your funds.

.. figure:: images/web_wallet/create_with_seed/01.png
   :alt:  Generating seed phrase


For the extension view:

.. figure:: images/web_wallet/create_with_seed/extension_view/01.png
   :alt: Generating seed phrase


Always store your seed phrase in a safe and secure location (and better more than one in different geo locations). Write it on a piece of paper. Do not store electronically neither as plain text nor in any other form!

In order to ensure that you have really written down your seed phrase, you will be asked to fill in the specific words from your seed phrase in random order. Only when you typed all the selected words correctly, you will be allowed to proceed to the next step.

.. figure:: images/web_wallet/create_with_seed/02.png
   :alt:  Generating seed phrase


For the extension view:

.. figure:: images/web_wallet/create_with_seed/extension_view/02.png
   :alt: Generating seed phrase


Creating a password is the next step, which was described in ::ref:`Easy onboarding` part. When the password was filled in, press the ‘Start using your wallet’ button 

Once your wallet is created, the main screen will show up without popup with the seed phrase verification.


.. figure:: images/web_wallet/create_with_seed/03.png
   :alt:  Generating seed phrase


For the extension view:

.. figure:: images/web_wallet/create_with_seed/extension_view/03.png
   :alt: Generating seed phrase


Seed verification
-----------------


.. attention:: You can close the popup until your balance will not exceed 100 beams. When your balance exceeds 100 beams the popup becomes to be unclosing. It will be closed only after the seed verification


If you decide to use an easy onboarding feature you need to verify your seed phrase later to be able to restore your wallet on other devices later. You can several options to do it:

**1.	Through popup Secure your seed**

.. attention:: The seed phrase is for your eyes only! Make sure no one is looking over your shoulder. For the best security always generate it on a clean air-gapped machine.

Press on the “Secure your phrase” button to start verification.


.. figure:: images/web_wallet/seed_verification/01.png
   :alt:  Seed verification through the popup


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/01.png
   :alt: Seed verification through the popup
   

The wallet will ask your password to be sure that you are the owner.


.. figure:: images/web_wallet/seed_verification/02.png
   :alt:  The seed verification popup require the password


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/02.png
   :alt: The seed verification popup require the password
   
   
After that you will be able to verify your seed phrase in a regular way.


.. figure:: images/web_wallet/seed_verification/03.png
   :alt:  Seed verification


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/03.png
   :alt: Seed verification
   
::attention: The seed phrase is for your eyes only! Make sure no one is looking over your shoulder. For the best security always generate it on a clean air-gapped machine.

Read carefully information on the popup and confirm it.


.. figure:: images/web_wallet/seed_verification/04.png
   :alt:  Seed verification confirmation


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/04.png
   :alt: Seed verification confirmation

   
On the next screen enter six required words to finish seed verification

.. figure:: images/web_wallet/seed_verification/05.png
   :alt:  Confirm seed verification with six words


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/05.png
   :alt: Confirm seed verification with six words
   
   
After successful verification popup is closed and never shown again


.. figure:: images/web_wallet/seed_verification/06.png
   :alt:  Main screen without seed verification popup


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/06.png
   :alt: Main screen without seed verification popup


**2.	Through Settings**


To initiate verification in another way, open the Settings by action menu


.. figure:: images/web_wallet/seed_verification/07.png
   :alt:  Choose settings in action menu


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/07.png
   :alt: Choose settings in action menu
   

In the Settings menu choose Privacy submenu and then choose Complete seed verification.

.. figure:: images/web_wallet/seed_verification/08.png
   :alt:  Choose seed verification in settings


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/08.png
   :alt: Choose seed verification in settings
   

The Wallet will ask your password to be sure that you are the owner.


.. figure:: images/web_wallet/seed_verification/09.png
   :alt:  Seed verification confirmation


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/09.png
   :alt: Seed verification confirmation

After that you will be able to verify your seed phrase in a regular way.


On the next screen enter six required words to finish seed verification

.. figure:: images/web_wallet/seed_verification/05.png
   :alt:  Confirm seed verification with six words


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/05.png
   :alt: Confirm seed verification with six words
   
   
After successful verification popup is closed and never shown again


.. figure:: images/web_wallet/seed_verification/06.png
   :alt:  Main screen without seed verification popup


For the extension view:

.. figure:: images/web_wallet/seed_verification/extension_view/06.png
   :alt: Main screen without seed verification popup
   
   
Restoring the Web Wallet
------------------------


Restore is not supported in the Beta version.


Main screen
-----------

The main screen of the wallet shows the current balance in the Amount status field as well as the transaction history and statuses. There are several transactions tabs All, In progress, Sent, Receive. On the left, under wallet status, there is a toolbar that provides navigation between two wallet screens - Main Screen and UTXO Screen.
In the right top corner there is an action menu which includes some functions: Security Mode, Payment proof, Where to buy beam, Settings and Logout. All of these functions will be explored below. 
Under the action menu there are two buttons Send and Receive which lead to according screens.


.. figure:: images/web_wallet/01_main_screen.png
   :alt:  Main screen elements


For the extension view:

.. figure:: images/web_wallet/01_main_screen_ev.png
   :alt: Main screen elements
   
   
In the right top corner there is an action menu which includes some functions: Security Mode, Payment proof, Where to buy beam, Settings and Logout. All of these functions will be explained below.


Receiving funds
---------------


Here is how the process of receiving BEAM looks like from a Receiver’s perspective:

*Generate an address
*Send your address to the Sender person over a secure communication channel
*Both Sender and Receiver’s Wallet must be online at the same time to complete a transaction.

It’s possible to reuse an address that already exists, more on that later.

**Generate an address**

Proceed to the main screen and click the blue ‘Receive’ button at the top right corner. This will open the receive screen.


.. figure:: images/web_wallet/receiving/01.png
   :alt:  Go to receiver screen


For the extension view:

.. figure:: images/web_wallet/receiving/extension_view/01.png
   :alt:  Go to receiver screen
   
Copy and paste the newly generated Beam address to send to Sender over a **secure communication channel**. There are three ways to do it:

* By selecting the address and clicking ``Command-C`` or ``Ctrl-C`` (depending on your platform)
* By right-click on the address and choosing 'Copy' from the drop-down menu
* By clicking the 'Copy transaction address' button

.. figure:: images/web_wallet/receiving/02.png
   :alt:  A receiver screen


For the extension view:

.. figure:: images/web_wallet/receiving/extension_view/02.png
   :alt:  A receiver screen

Each time the Receive Beam dialog is open, a new Beam address is generated. By default, the address is valid for 24 hours.
If you want make the address active, you should close Receive screen. You can do it by clicking on ‘Close’ button or ‘Copy transaction address’.


Sending funds
-------------


Here is how the process of sending BEAM looks like from a Sender’s perspective:
* Receive the address the funds should be sent to
* Send BEAM to Receiver
* Stay online until Receiver confirms the transaction

::attention: When sending the address make sure you use a secure communication channel.

::attention: Make sure the entire address is sent to the Sender as it’s longer than it appears on the screen. Don’t forget to double check the value in whichever messenger app of your choice because viruses and malware on your computer may change your address while it’s in the clipboard.

In order to send BEAM, you will need to click the magenta ‘Send’ button at the top right corner. This will open the Send screen.
Make sure you have the correct address and paste the Receiver’s Beam address in the ‘Send To’ field.

To help to identify the transaction, you may also choose to fill in the optional Comment field. The comment will remind you what or who the transaction is for. The comment is stored locally, thus it will only be visible in your wallet for bookkeeping purposes.


.. figure:: images/web_wallet/sending/01.png
   :alt:  Go to Sender screen


For the extension view:

.. figure:: images/web_wallet/sending/extension_view/01.png
   :alt:  Go to Sender screen
   

The comment is also displayed in the extended transaction view on Main Screen:

Select the transaction amount in BEAM you want to send. Transaction amount is in BEAM and may contain fractional values such as 1.25 BEAM or 11.3 BEAM and the like. Keep in mind you also have to pay a transaction fee, hence the amount to send plus the fee must be equal to or less than the available balance.
Transaction fees are specified in GROTH (100 millionths of BEAM).The minimum fee is 100 GROTH, it’s set by default but the higher transaction fee will help miners to prioritize your transaction.

You can see the remaining amount of BEAM in your wallet and the change that will be received after the transaction. 

After you click ‘Send’ you will see a confirmation transaction details popup with the most important transaction details:

.. figure:: images/web_wallet/sending/02.png
   :alt:  Sender screen


For the extension view:

.. figure:: images/web_wallet/sending/extension_view/02.png
   :alt: Sender screen

It also can require the password if this function was turned on in the settings.


Completing the transaction
--------------------------

Once you confirm, the transaction is sent to the Receiver’s wallet. If Receiver’s wallet is currently offline or if the network is loaded, you might see the transaction appear ‘Waiting for receiver’ accordingly on your transaction list. Once the transaction is starting, it will be sent to the nodes and shown as ‘sending’.


.. figure:: images/web_wallet/01_completing.png
   :alt:  Go to Sender screen
   
   
.. figure:: images/web_wallet/02_completing.png
   :alt:  Go to Sender screen


While a transaction is in ‘Waiting for receiver’ you can cancel it by clicking on the dropdown to the right of the transaction row and then select ‘Cancel’. The other party will receive notification that the transaction was either ‘Cancelled’ or ‘Expired,’ and funds plus fee that were allocated for this transaction will become available again. It is not possible to cancel a transaction in ‘In progress’ or ‘Sent’ states.
If your transaction appears as ‘Waiting for receiver’ for a long time, it means the Receiver is not online. 

::attention: If the transaction was not sent to the nodes, for any reason, it will expire after 720 blocks, or roughly 12 hours. This is done to avoid a situation in which UTXO is locked forever.


Beams from Faucet
-----------------

For best understanding how the wallet is worked you can receive some amount from Beam Community Faucet. 
1. First of all, copy an address from the Receiver screen (read Receiving funds for more information)

.. figure:: images/web_wallet/receiving/01.png
   :alt:  Go to receiver screen


For the extension view:

.. figure:: images/web_wallet/receiving/extension_view/01.png
   :alt:  Go to receiver screen
   
   
.. figure:: images/web_wallet/receiving/02.png
   :alt:  A receiver screen


For the extension view:

.. figure:: images/web_wallet/receiving/extension_view/02.png
   :alt:  A receiver screen
   
   
2. Then on the main screen press on get coins button from the popup. It should link you to the [Beam Community Faucet] (https://faucet.beamprivacy.community/) 


.. figure:: images/web_wallet/beam_faucet/01.png
   :alt:  Go to Faucet


For the extension view:

.. figure:: images/web_wallet/beam_faucet/extension_view/01.png
   :alt:  Go to Faucet
   
   
3. On this website enter your address below to get some free Beam for testing to appropriate field, do a captcha and press on ‘Get beams’ button


.. figure:: images/web_wallet/beam_faucet/02.png
   :alt:  Beam Community Faucet
   

4. When the transaction is approved on Beam Community Faucet you need to return to the Wallet. The transaction with a small amount should have receiving status (or received).


.. figure:: images/web_wallet/beam_faucet/03.png
   :alt:  Receiving from Faucet


For the extension view:

.. figure:: images/web_wallet/beam_faucet/extension_view/02.png
   :alt:  Receiving from Faucet
   
   
.. figure:: images/web_wallet/beam_faucet/04.png
   :alt:  Received from Faucet
    
   
UTXO screen
-----------


UTXO (Unspent Transaction (TX) Output) is like a banknote of a specific amount. Simply said, if BEAM is the currency, any UTXO can be considered a ‘bill’. You can have multiple ‘bills’ in your wallet at the same time.
On the technical level, in Beam, like in most other cryptocurrencies, your balance emerges as a result of multiple incoming and outgoing transactions. Each transaction uses some existing inputs and creates new outputs. All the outputs controlled by the wallet are shown in the UTXO screen.
There are several transaction tabs Available, In progress, Spent, Unavailable which include UTXO with appropriate statuses.
The type of UTXO can be:
*	Regular - UTXO received as a result of a transaction. It is immediately available for spending
*	Change - UTXO received as a result of change from a transaction. It is immediately available for spending
In the following screenshots you can see how this screen is displayed.If you push to a certain UTXO you see details. This function is available only for full screen view. 
Also, in this screenshot, transactions are finished and have status available.
