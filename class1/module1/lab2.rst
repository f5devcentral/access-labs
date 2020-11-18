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
limited functionality on any BIG-IP platform without a specific license (`see F5 KB15854 <https://support.f5.com/csp/article/K15854>`__).  APM is licensed based on the number of Access Sessions
and Concurrent Users Sessions (`see APM Operations Guide <https://support.f5.com/csp/article/K72971039>`__). You can provision APM limited and immediately start using all the functions of APM with a
limitation of 10 Access and Concurrent user session.

#. Log in to bigip1.f5lab.local with administrative credentials provided
#. On the left menu navigate to **System** --> **Resource Provisioning**
#. Click box and on the drop down next to the module and choose Nominal

.. Note:: What do the options mean?
+---------------+---------------------------------------------------------------------------------------+
|Dedicated      |Specifies that all resources are dedicated to the module you are provisioning. For all |
|               |other modules, the level option must be set to none.                                   |
+---------------+---------------------------------------------------------------------------------------+
|Minimum        |Specifies that you want to provision the minimum amount of  resources for the module   |
|               |you are provisioning.                                                                  |
+---------------+---------------------------------------------------------------------------------------+
|Nominal        |Specifies that you want to share all of the available resources equally among all of   |
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

#.  Click on **Access** --> **Guided Configuration** from the left Menu
#.  In the upper right corner you will find the version.

|image4|

#.  Click on Upgrade Guided configuration
#.  Choose File
#.  Navigate to blah and chose f5-iappslx-agc-usecase-pack-7.0-0.0.1481.tar.gz
#.  Click Upload and Install

|image5|

#.  Click Continue
#.  A set of tiles appears at top listing the areas of use cases where Guided Configuration can be used

|image6|

#.  Click on the Federation Tile.
#.  Under this tile are several Identity Federation use cases available.  Each use case has an accompanying guide to walk you through the configuration.  This is not designed for already deployed
applications but used for new deployments.  All the components needed to create the configuration will be deployed on the BIG-IP through this guide.  Editing and configuring of the solution will
be maintained within this menu.
#.  Click on **SAML Service Provider**
#.  Here you will find there are couple topologies.  SAML SP Initiated and SAML IdP Initiated.

|image7|

#. If there are any required configuration pieces missing to complete guided configuration they will appear in the right pane

|image8|

#. Below the topologies you will find all the components that will be configured using the guided configured

|image9|

#.  From here you would click next to begin configuration. (We will explore this further in the 300 Series labs)

#.  Click on the Guide Configuration bread crumb at the top of the screen to return to the main menu.

#.  Zero Trust is the next tile.
Zero trust follows the principle never trust, always verify and thus enforces authentication and verification for every user or device attempting to access resources whether from within or
outside of the network.

The easiest way to create policies to support zero trust security is to use the Zero Trust-Identity Aware Proxy template in Access Guided Configuration. The template takes you through the
steps needed to create an Identity Aware Proxy. Access Policy Manager (APM) acts as the Identity Aware Proxy helping to simplify client access to both multi-cloud and on-premise web applications,
and securely manage access from client devices.

On APM, you can develop per-request policies with subroutines that perform different levels of authentication, federated identity management, SSO (single sign on), and MFA (multi-factor
authentication) depending on the requirements. Subroutines perform continuous checking based on a specified duration or gating criteria. Policies can be as complex or as simple as you need
them to be to provide seamless yet secure access to resources. Refer to Implementing Zero Trust with Per-Request Policies for many examples of per-request policies that implement different
aspects of zero trust.

For additional security, device posture checking provides instantaneous device posture information. The system can continuously check clients to be sure, for example, that their antivirus,
firewall, and patches meet company requirements, ensuring that the device maintains trust at all times.

On the client side, F5 Access Guard allows real-time posture information to be inspected with per-request policy subroutines. F5 Access Guard generates posture information asynchronously,
and transparently transmits it to chosen APM server endpoints using special HTTP headers. Refer to BIG-IP Access Policy Manager: Configuring F5 Access Guard
for details on client requirements.
#.  Click on the Identity Aware Proxy configuration option
#.  There are two topologies available:

+---------------+---------------------------+
|Single Proxy   | |image13|   |  |image17|  |
+---------------+---------------------------+
|Multi-Proxy    | |image14|   |  |image16|  |
+---------------+---------------------------+

#.  Proceeding with this configuration will create a number of object as seen here.

|image18|

.. Note:: Webtop is available as of version 16.0

#.  Return to the may screen by clicking the Guided Configuration bread crumb
#.  Click on the Microsoft Integration tile
#.  There are three options available:
    - ADFS Proxy:  This is the Web Application Proxy (WAP) replacement use case where BIG-IP can replace the ADFS Windows Servers in the DMZ and serve as the secure WAP platform between your
    external users and the internal ADFS infrastructure.
    - Azure AD Application: This allows integration of Azure AD in to various web applications without need of application changes.
    - Exchange Proxy: This guided configuration replaces the need to run the iApps for Exchange

|image19|

#.  Click on the API Protection tile
#.  Click on the API Protection Proxy configuration
#.  The topology for API protection describes the configuration for this option. This configuration provides authentication pieces for your API.

|image19|

.. Note:: For more complete API protection combine APM with F5 Web Application Firewall for the most robust solution.

#.  The objects created with this configuration:

|image20|

Task 3: Overview
-----------------
The Overview menu is where an administrator can view active sessions, previous sessions, and view various reports.

#.  Click on **Access** --> **Overview** from the left menu
#.  Here are Active Sessions.  When users login to applications using APM policies the sessions will appear in this pane.
#.  Open another tab and login to the application
#.  Return to the BIG-IP tab and view the session
#.  A new session will appear in the Total Active Sessions.  From this pane you can see the session ID, variables collected, Client IP, Virtual Server in use, session type and any profiles in use
#.  Click on the View under Variables
#.  This gives us all the information collected on the current session
    - Can you find the user logged in?
    - What is the client platform
    - Client Type?
    - Access Profile?
#.  Click the back button on the browser to return to the Active Sessions.
#.  Click on the Session ID

.. Note:: The Session ID will also be displayed to the user should they have an issue with logging in.  An error message will display and their session ID will be given

#.  The Session ID will take you to the first set of reporting **Access Report**
#.  This section will give you details on the session.  Each log item is a message on the policy flow as a user walks through an Access policy.  (We will cover Per Session and Per Request policies in
in more deail later).
    - Can you find the first **Following Rule** log message?
    - Where did it flow?
    - Was the user successful?
#.  Return to the first screen by using the back button in the browser
#.  There are two other reporting functions in this screen, **OAuth Report** and **SWG Reports** which will be covered in more detail in later labs
#.  The last section is Event Logs.

.. Note:: URL Request Logs is part of SWG functionality and will be covered later

#.  Click on **Event Logs** and choose **Settings**
#.  This is where you can create logging profiles for access policies.  From here you can specify what information to collect and to what detail.
#.  Check the box next to the default-log setting and choose **Edit** from Below
#.  This opens the settings for the APM log


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

.. |image1| image:: /class1/media/image01.png
.. |image2| image:: /class1/media/image02.png
.. |image3| image:: /class1/media/image03.png
.. |image4| image:: /class1/media/image4.png
.. |image5| image:: /class1/media/image5.png
.. |image6| image:: /class1/media/image6.png
.. |image7| image:: /class1/media/image7.png
.. |image8| image:: /class1/media/image8.png
.. |image9| image:: /class1/media/image9.png
.. |image10| image:: /class1/media/image10.png
.. |image11| image:: /class1/media/iamge11.png
.. |image12| image:: /class1/media/image12.png
.. |image13| image:: /class1/media/image13.png
.. |image14| image:: /class1/media/image14.png
.. |image15| image:: /class1/media/image15.png
.. |image16| image:: /class1/media/image16.png
.. |image17| image:: /class1/media/image17.png
.. |image18| image:: /class1/media/imag18.png
.. |image19| image:: /class1/media/image19.png
.. |image20| image:: /class1/media/image20.png
.. |image21| image:: /class1/media/image21.png
