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
   

It takes several seconds to create a new wallet.


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


Creating a password is the next step, which was describe in ::ref:`Easy onboarding` part. When the password was filled in, press the ‘Start using your wallet’ button 

Once your wallet is created, the main screen will show up without popup with the seed phrase verification.


.. figure:: images/web_wallet/create_with_seed/03.png
   :alt:  Generating seed phrase


For the extension view:

.. figure:: images/web_wallet/create_with_seed/extension_view/03.png
   :alt: Generating seed phrase
