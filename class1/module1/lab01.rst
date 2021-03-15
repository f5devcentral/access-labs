Lab 1: APM GUI Overview
===========================================

Objectives
----------

The intention of this lab will be to show how to enable Access Policy Manager (APM) through resource provisioning.  Next we will explore all the components within the **Access** left menu.
This is not a deep dive on the components but an overview of the components, features and concepts of APM.

Lab Requirements
----------------

-  A pre existing virtual server at IP and DNS Name

Setup Lab Environment
-----------------------------------

To access your dedicated student lab environment, you will require a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Lab Training Portal. The RDP client will be used to connect to the Jump Host, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumpohost.f5lab.local

   |accessjh|

#. Select your RDP solution.

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#. Login with the following credentials:

         - User: **f5lab\\user1**
         - Password: **user1**

#. After successful logon the Chrome browser will auto launch opening the site https://portal.f5lab.local.  This process usually takes 30 seconds after logon.

#. Click the **Classes** tab at the top of the page.

	|accessportal|


#. Scroll down the page until you see **101 Intro to Access Foundational Concepts** on the left

   |101intro|

#. Hover over tile **APM GUI Overview**. A start and stop icon should appear within the tile.  Click the **Play** Button to start the automation to build the environment

   |guioverview|

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |issues|

Task 1: Resource Provisioning
---------------------------------------
Access Policy Manager (APM) is a module available for use on the BIG-IP platform (Hardware and Virtual).  Unlike other modules, APM can be provisioned with limited functionality on any BIG-IP platform without a specific license (`see F5 KB15854 <https://support.f5.com/csp/article/K15854>`__).  APM is licensed based on the number of Access Sessions and Concurrent Users Sessions (`see APM Operations Guide <https://support.f5.com/csp/article/K72971039>`__). You can provision APM limited and immediately start using all the functions of APM with a limitation of 10 Access and Concurrent user session.

#. Log in to bigip1.f5lab.local with administrative credentials provided
#. On the left menu navigate to **System** --> **Resource Provisioning**
#. Click box and on the drop down next to the module and choose **Nominal**

      .. Note:: In most use cases you will want to use **Nominal** for provisioning modules.  What does each setting mean?
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

      |image01|

      .. Important::  APM has already been provisioned for this lab.  The next step would be completed if you are provisioning on your own BIG-IP.

#. Before you click on Submit note that this operation will halt operations while the module provisions.  Do not do this on an active unit processing traffic unless you are in an outage window. This will not require a reboot but will take approximately 1 to 5 minutes to complete.

      |image02|
      |image03|

      .. Note::  Resource Provisioning is not a synced item between HA pairs.  You will need to provision the module on all devices in the cluster.

Task 2: Guided Configuration
-----------------------------
Access Guided Configuration (AGC) provides an easy way to create BIG-IP configurations for categories of Access use cases. This feature is written in has an independent release from TMOS and requires updates for new configurations from time to time. To find updates and expanded use cases it will be necessary to download and install updates from https://downloads.f5.com. In this task we are going to explore the menu and take a look at a few options. We will not be deploying any of these solutions in this lab.

.. Important::  This lab has already been updated with the latest **Access Guided Configuration** updates.  The following steps can be used on your own appliances.

#. https://downloads.f5.com/esd/product.jsp?sw=BIG-IP&pro=Guided_Configuration
#. Click on **Access** --> **Guided Configuration** from the left Menu
#. In the upper right corner you will find the version.

      |image4|

#. Click on Upgrade Guided configuration
#. Choose File
#. Navigate to the location you have saved the latest download and chose the tar.gz package
#. Click Upload and Install

      |image5|

#.  Click Continue

#.  Go to **Access** --> **Guided Configuration**
#.  A set of tiles appears at top listing the areas of use cases where Guided Configuration can be used

      |image06|

#.  Click on the Federation Tile.
#.  Under this tile are several Identity Federation use cases available.  Each use case has an accompanying guide to walk you through the configuration.  This is not designed for already deployed applications but used for new deployments.  All the components needed to create the configuration will be deployed on the BIG-IP through this guide.  Editing and configuring of the solution will be maintained within this menu.
#.  Click on **SAML Service Provider**
#.  Here you will find there are couple topologies.  SAML SP Initiated and SAML IdP Initiated.

      |image07|

#. If there are any required configuration pieces missing to complete guided configuration they will appear in the right pane

      |image08|

#. Below the topologies you will find all the components that will be configured using the guided configured

      |image09|

#.  From here you would click next to begin configuration. (We will explore this further in the 300 Series labs)
#.  Click on the Guide Configuration bread crumb at the top of the screen to return to the main menu.
#.  Zero Trust is the next tile. Zero trust follows the principle never trust, always verify and thus enforces authentication and verification for every user or device attempting to access resources whether from within or outside of the network.

      **About Identity Aware proxy**

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

      +---------------+-------------+-------------+
      |Single Proxy   | |image13|   |  |image17|  |
      +---------------+-------------+-------------+
      |Multi-Proxy    | |image14|   |  |image16|  |
      +---------------+-------------+-------------+

#.  Proceeding with this configuration will create a number of object as seen here.

      .. Note::  If you are interested in learning more on this specific solution please consider taking the Zero Trust Identity Aware Proxy class.

      |image18|

      .. Note:: Webtop is available as of version 16.0

#.  Return to the main screen by clicking the Guided Configuration bread crumb
#.  Click on the Microsoft Integration tile
#.  There are three options available:

      +-----------------------+-------------------------------------------------------------------------------------------------------+
      |ADFS Proxy             |This is the Web Application Proxy (WAP) replacement use case where BIG-IP can replace the ADFS Windows |
      |                       |Servers in the DMZ and serve as the secure WAP platform between your external users and the internal   |
      |                       |ADFS infrastructure.                                                                                   |
      +-----------------------+-------------------------------------------------------------------------------------------------------+
      |Azure AD Application   |This allows integration of Azure AD in to various web applications connecting through without need of  |
      |                       |application changes.                                                                                   |
      +-----------------------+-------------------------------------------------------------------------------------------------------+
      |Exchange Proxy         |This guided configuration replaces the need to run the iApps for Exchange.                             |
      |                       |                                                                                                       |
      +-----------------------+-------------------------------------------------------------------------------------------------------+

      |image19|

#.  Click on the API Protection tile
#.  Click on the API Protection Proxy configuration
#.  The topology for API protection describes the configuration for this option. This configuration provides authentication pieces for your API.

      |image20|

      .. Note:: For more complete API protection combine APM with F5 Web Application Firewall for the most robust solution.

#.  The objects created with this configuration:

      |image21|

Task 3: Overview
-----------------
The Overview menu is where an administrator can view active sessions, previous sessions, and view various reports.

#.  Click on **Access** --> **Overview** from the left menu
#.  Here are Active Sessions.  When users login to applications using APM policies the sessions will appear in this pane.
#.  Open another tab and login to the application:  https://server1.acme.com

      +---------------+-------------+
      |username       | user1       |
      +---------------+-------------+
      |password       | user1       |
      +---------------+-------------+

#.  Return to the BIG-IP tab and view the active session
#.  A new session will appear in the Total Active Sessions.  From this pane you can see the session ID, variables collected, Client IP, Virtual Server in use, session type and any profiles in use
#.  Click on the View under Variables
#.  This gives us all the information collected on the current session

      - Can you find the user logged in?
      - What is the client platform
      - Client Type?
      - Access Profile?

#.  Click the back button on the browser to return to the Active Sessions.
#.  Click on the Session ID

      .. Note:: The Session ID will also be displayed to the user should they have an issue with logging in.  An error message will display and their session ID will be given.  You can simulate this by editing the access policy **server1-psp** later on in the lab.

        |sessionid|

#.  The Session ID will take you to the first set of reporting **Access Report**
#.  This section will give you details on the session.  Each log item is a message on the policy flow as a user walks through an Access policy.  (We will cover Per Session and Per Request policies in in more detail later).

      - Can you find the first **Following Rule** log message?
      - Where did it flow?
      - Was the user successful?

#.  Return to the first screen by clicking on **Active Sessions** from the menu bar above

      |activesessions|

#.  In **Active Sessions** click on the check box next to the session and select the **Kill Selected Sessions** button.  This will terminate the users session and make them login again.

      |killsession|

#.  Click **Delete**
#.  Click on **Access Reports** from the menu bar above
#.  You will be prompted to enter a time period to run the report

      |image22|

      .. Note:: This is how you can view past sessions.  Pick a time frame and run a report.

#.  There are two other reporting functions in this screen, **OAuth Report** and **SWG Reports**.  We will not cover these reports in this lab.
#.  The last section is Event Logs.

    .. Note:: URL Request Logs is part of SWG functionality and will not be covered in this lab

#.  From the top menu bar Click on the drop down next to **Event Logs** and choose **Log Settings**. This is where you can create logging profiles for access policies.  From here you can specify what information to collect and to what detail.
#.  Click the **Create** button
#.  We will create a new APM Log profile

      +----------------------+---------------------------+----------------------------------+
      |General Information   | Name                      |  Basic_Log_profile               |
      +----------------------+---------------------------+----------------------------------+
      |                      | Enable Access System Logs |  Check box                       |
      +----------------------+---------------------------+----------------------------------+
      |Access System Logs    | Publisher                 |  /Common/sys-db-access-publisher |
      +----------------------+---------------------------+----------------------------------+
      |                      | Access Policy             |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | ACL                       |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | Secure Web Gateway        |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | OAuth                     |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | VDI                       |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | ADFS Proxy                |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | Per-Request Policy        |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | SSO                       |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | ECA                       |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | PingAccess Profile        |  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |                      | Endpoint Management System|  Notice                          |
      +----------------------+---------------------------+----------------------------------+
      |Access Profile        | Selected                  |  server1-psp                     |
      +----------------------+---------------------------+----------------------------------+

      .. Note:: Within the Access System Logs section of the log profile is where you can change the logging for various portions of the APM Policies.  The one you will use most will be to move Access Policy from Notice to Debug and/or Pre-Request Policy from Notice to Debug.  As you can see you can pick and choose what level of notifications you want in your logs.  This will impact what you see in Access Reports for a session and what appears in /var/log/apm.

#.  From the left menu go to **Access** --> **Overview** --> **Dashboard**

      |image23|

#.  The Dashboard can give you a quick synopsis on Access Session, Network Access Session, Portal Access and Access control Lists.

      .. Note:: For more reporting on APM stats look to BIG-IQ or exporting logs to 3rd party SIEMs and create your own dashboard.

Task 4: Profile/Policies
------------------------
Profiles and Policies are where we begin to learn about what makes APM function.  In order for APM functions to be added to a Virtual server we need to create Access Profiles and Policies.  These entities take all the components we will look at below and put them in a logical flow through the Visual Policy Editor (VPE). These entities are things like login pages, authentication, single sign on methods and endpoint checks.  To being we have to create an Access Profile.  Within that profile we create a per session policy.  When that is completed we attach that profile to a Virtual Server.

.. Note::  You can associate one Access Profile (which includes a per-session policy) and one per-request policy per virtual server.

#.  From the left menu go to **Access** --> **Profiles/Policies** --> **Access Profiles (Per-Session Policies)**

      The per-session policy runs when a client initiates a session. (A per-session policy is also known as an access policy.) Depending on the actions you include in the access policy, it can authenticate the user and perform other actions that populate session variables with data for use throughout the session.

#.  Click on the Create button on the far right








Lab 2 is now complete.

.. |accessjh| image:: /class1/module1/media/lab01/setup/accessjh.png
.. |accessportal| image:: /class1/module1/media/lab01/setup/accessportal.png
.. |101intro| image:: /class1/module1/media/lab01/setup/101intro.png
.. |guioverview| image:: /class1/module1/media/lab01/setup/guioverview.png
.. |issues| image:: /class1/module1/media/lab01/setup/issues.png
.. |image01| image:: /class1/module1/media/lab01/image01.png
.. |image02| image:: /class1/module1/media/lab01/image02.png
.. |image03| image:: /class1/module1/media/lab01/image03.png
.. |image4| image:: /class1/module1/media/lab01/image4.png
.. |image5| image:: /class1/module1/media/lab01/image5.png
.. |image06| image:: /class1/module1/media/lab01/image6.png
.. |image07| image:: /class1/module1/media/lab01/image7.png
.. |image08| image:: /class1/module1/media/lab01/image8.png
.. |image09| image:: /class1/module1/media/lab01/image9.png
.. |image13| image:: /class1/module1/media/lab01/image13.png
.. |image14| image:: /class1/module1/media/lab01/image14.png
.. |image16| image:: /class1/module1/media/lab01/image16.png
.. |image17| image:: /class1/module1/media/lab01/image17.png
.. |image18| image:: /class1/module1/media/lab01/image18.png
.. |image19| image:: /class1/module1/media/lab01/image19.png
.. |image20| image:: /class1/module1/media/lab01/image20.png
.. |image21| image:: /class1/module1/media/lab01/image21.png
.. |sessionid| image:: /class1/module1/media/lab01/sessionid.png
.. |activesessions| image:: /class1/module1/media/lab01/activesessions.png
.. |killsession| image:: /class1/module1/media/lab01/killsession.png
.. |image22| image:: /class1/module1/media/lab01/image22.png
.. |image23| image:: /class1/module1/media/lab01/image23.png
.. |multidomain| image:: /class1/module1/media/lab01/multidomain.png
