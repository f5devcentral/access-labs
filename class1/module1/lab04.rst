Lab 4: Access Logs Overview
=============================================

Access Policy Manager (APM) provides a default-log-setting. When you create an access profile, the default-log-setting is automatically assigned to it. The default-log-setting can be retained, removed, or replaced for the access profile. The default-log-setting is applied to user sessions only when it is assigned to an access profile.

Regardless of whether it is assigned to an access profile, the default-log-setting applies to APM processes that run outside of a user session. Specifically, on a BIG-IP system with an SWG subscription, the default-log-setting applies to URL database updates

Lab Requirements
----------------

A working configuration from Lab 1 or deploying the lab environment via Task 1: Setup Lab Enviroment below  



Task 1 - Setup Lab Environment
-----------------------------------

To access your dedicated student lab environment, you will require a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Lab Training Portal. The RDP client will be used to connect to the Jump Host, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumpohost.f5lab.local

   |image001|

#. Select your RDP solution.  

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#. Login with the following credentials:

         - User: **f5lab\\user1**
         - Password: **user1**

#. After successful logon the Chrome browser will auto launch opening the site https://portal.f5lab.local.  This process usually takes 30 seconds after logon.

	|image002|

#. Click the **Classes** tab at the top of the page.

#. Scroll down the page until you see **101 Intro to Access Foundational Concepts** on the left

   |image003|

#. Hover over tile **Access Logs Overview**. A start and stop icon should appear within the tile.  Click the **Play** Button to start the automation to build the environment

   |image004|

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image005|



Task 2 -  Active Sessions
---------------------------------------

#. Refresh Rate
#. Total Active sessions
#. Search
#. Examine Session
#. Kill Selected sessions



Task 2: Access Reports
--------------------------------------

#. Report Parameters
#. Session ID
    - Log messages
#. View Session Variables
#. Build in Reports


Task 3: Log Settings
--------------------------------------------------


https://support.f5.com/csp/article/K24826763

#. General information
#. Access System Logs
#. URL Request Logs
#. Access Profiles
#. SSO Objects


Task 4: Dashboard
------------------



Task 5 - Lab CleanUp
------------------------

#. This concludes lab 4.

   |image000|



.. |image000| image:: ./media/lab04/000.png
.. |image001| image:: ./media/lab04/001.png
.. |image002| image:: ./media/lab04/002.png
