Lab 1: ADFS Proxy using ADFS Auth
=============================================


Task 1 - Setup Lab Environment
-----------------------------------

To access your dedicated student lab environment, you will require a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Lab Training Portal. The RDP client will be used to connect to the Jump Host, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumpohost.f5lab.local

   |image001|

#. Select your RDP resolution.

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#. Login with the following credentials:

         - User: **f5lab\\user1**
         - Password: **user1**

#. After successful logon the Chrome browser will auto launch opening the site https://portal.f5lab.local.  This process usually takes 30 seconds after logon.

#. Click the **Classes** tab at the top of the page.

	|image002|


#. Scroll down the page until you see **203 Microsoft Integrations** on the left

   |image003|

#. Hover over tile **ADFS proxy using ADFS Authentication**. A start and stop icon should appear within the tile.  Click the **Play** Button to start the automation to build the environment

   +---------------+-------------+
   | |image004     | |image005|  |
   +---------------+-------------+

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image006|

Task 2 - Access the Microsoft ADFS guided configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the webbrowser, click on the **Access** tab located on the left side.

    |image007|

#. Click **Guided Configuration**

    |image008|

#. Click **Microsoft Integration**

    |image009|

#. Click **ADFS Proxy**

    |image010|

#. Click **Next**

    |image011|

Task 3 - ADFS Proxy Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Task 4 - Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Task 5 - ADFS Pool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



Task 6 - Summary
~~~~~~~~~~~~~~~~~~~~~~~~




Task 7 - Testing
~~~~~~~~~~~~~~~~~~~~
