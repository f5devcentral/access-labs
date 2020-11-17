Lab 2: Provisioning & Main Menu Navigation
===========================================

Objectives
----------

The lab steps through the provisioning process and various menu items for Access Policy Manager (APM).  The goal of this lab is to
instruct users on enabling the module from their BIG-IP platforms and examine the components of APM.

Lab Requirements
----------------

-  A pre existing virtual server at 10.1.10.101 or https://server1.acme.com

Task 1: Resource Provisioning
---------------------------------------
Access Policy Manager (APM) is another module available for use on the BIG-IP platform (Hardware and Virtual).  Unlike other modules, APM can be provisioned with
limited functionality on any BIG-IP platform without a specific license ('see F5 KB15854 <https://support.f5.com/csp/article/K15854>'__).  APM is licensed based on the number of Access Sessions
and Concurrent Users Sessions ('see APM Operations Guide <https://support.f5.com/csp/article/K72971039>'__). You can provision APM limited and immediately start using all the functions of APM with a
limitation of 10 Access and Concurrent user session.

#. Log in to bigip1.f5lab.local with administrative credentials provided
#. On the left menu navigate to **System** --> **Resource Provisioning**
#. Click box and on the drop down next to the module and choose Nominal

.. Note:: What do the options mean?
+---------------+---------------------------------------------------------------------------------------+
|Dedicated -    |Specifies that all resources are dedicated to the module you are provisioning. For all |
|               |other modules, the level option must be set to none.                                   |
+---------------+---------------------------------------------------------------------------------------+
|Minimum -      |Specifies that you want to provision the minimum amount of  resources for the module   |
|               |you are provisioning.                                                                  |
+---------------+---------------------------------------------------------------------------------------+
|Nominal -      |Specifies that you want to share all of the available resources equally among all of   |
|               |the modules that are licensed on the unit.                                             |
+---------------+---------------------------------------------------------------------------------------+

|image1|

#. Before you click on Submit note that this operation will halt operations while the module provisions.  Do not do this on an active unit processing traffic unless you are in an outage window. This
will not require a reboot but will take approximately 2 to 5 minutes to complete.

|image2|
|image3|

.. Note::  Resource Provisioning is not a synced item between HA pairs.  You will need to provision the module on all devices in the cluster.

Task 2: Guided Configuration
-----------------------------
Access Guided Configuration provides an easy way to create BIG-IP configurations for categories of Access use cases. This feature is written in iAppsLX so is independent release from TMOS.  To find
updates and expanded use cases it will be necessary to download and install updates from https://downloads.f5.com. In this task we are just going to explore the menu and take a look at the options.
We will not be deploying any of these solutions in this lab.

#. Click on **Access** --> **Guided Configuration** from the left Menu
#. In the upper right corner you will find the version.

|image4|

#. Click on Upgrade Guided configuration
#. Choose File
#. Navigate to blah and chose f5-iappslx-agc-usecase-pack-7.0-0.0.1481.tar.gz
#. Click Upload and Install

|image5|

#. Click Continue
#. A set of tiles appears at top listing the areas of use cases where Guided Configuration can be used

|image6|

#. Click on the Federation Tile.
#. Under this tile are several Identity Federation use cases available.  Each use case has an accompanying guide to walk you through the configuration.  This is not designed for already deployed
applications but used for new deployments.  All the components needed to create the configuration will be deployed on the BIG-IP through this guide.  Editing and configuring of the solution will
be maintained within this menu.
#. Click on **SAML Service Provider**
#. Here you will find there are couple topologies.  SAML SP Initiated and SAML IdP Initiated.

|image7|

#. If there are any required configuration pieces missing to complete guided configuration they will appear in the right pane

|image8|

#. Below the topologies you will find all the components that will be configured using the guided configured

|image9|

#.  From here you would click next to begin configuration. (We will explore this further in the 300 labs)

#. Click on the Guide Configuration bread crumb at the top of the screen to return to the main menu.

#. Zero Trust is the next tile.  This configuration deploys the Identity Aware Proxy. An Identity Aware Proxy is how the BIG-IP platform can be used as a Gatekeeper to your applications.  With little
to no change to the application infrastructure this Gatekeeper can interrogate every request made to the application to verify user rights and credentials.  This is will little friction to users as
single sign on.



Task 3: Overview
-----------------



Task 4: Profile/Policies
------------------------



Task 5: Authentication
----------------------------


Task 6: Single Sign-On
----------------------------


Task 7: Federation
----------------------------


Task 8: Connectivity/VPN
----------------------------



Task 9: API Protection
----------------------------


Task 10: Secure Web Gateway
----------------------------



Task 11: Access Control Lists
-----------------------------



Task 12: Webtops
----------------------------





Lab 2 is now complete.

.. |image1| image:: media/001.png
.. |image2| image:: media/002.png
.. |image3| image:: media/003.png
.. |image4| image:: media/004.png
.. |image5| image:: media/005.png
.. |image6| image:: media/006.png
.. |image7| image:: media/007.png
.. |image8| image:: media/008.png
.. |image9| image:: media/009.png
.. |image10| image:: media/010.png
.. |image11| image:: media/011.png
.. |image12| image:: media/012.png
.. |image13| image:: media/013.png
.. |image14| image:: media/014.png
.. |image15| image:: media/015.png
.. |image16| image:: media/016.png
.. |image17| image:: media/017.png
.. |image18| image:: media/018.png
.. |image19| image:: media/019.png
.. |image20| image:: media/020.png
.. |image21| image:: media/021.png
