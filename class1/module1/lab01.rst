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
Access Policy Manager (APM) is a module available for use on the BIG-IP platform (Hardware and Virtual).  Unlike other modules, APM can be provisioned with
limited functionality on any BIG-IP platform without a specific license (`see F5 KB15854 <https://support.f5.com/csp/article/K15854>`__).  APM is licensed based on the number of Access Sessions
and Concurrent Users Sessions (`see APM Operations Guide <https://support.f5.com/csp/article/K72971039>`__). You can provision APM limited and immediately start using all the functions of APM with a
limitation of 10 Access and Concurrent user session.

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
Access Guided Configuration (AGC) provides an easy way to create BIG-IP configurations for categories of Access use cases. This feature is written in has an independent release from TMOS and requires
updates for new configurations from time to time. To find updates and expanded use cases it will be necessary to download and install updates from https://downloads.f5.com. In this task we are
going to explore the menu and take a look at a few options. We will not be deploying any of these solutions in this lab.

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
Profiles and Policies are where we begin to learn about what makes APM function.  In order for APM functions to be added to a Virtual server we need to create Access Profiles and Policies.  These
entities take all the components we will look at below and put them in a logical flow through the Visual Policy Editor (VPE). These entities are things like login pages, authentication, single sign
on methods and endpoint checks.  To being we have to create an Access Profile.  Within that profile we create a per session policy.  When that is completed we attach that profile to a Virtual Server.

.. Note::  You can associate one Access Profile (which includes a per-session policy) and one per-request policy per virtual server.

#.  From the left menu go to **Access** --> **Profiles/Policies** --> **Access Profiles (Per-Session Policies)**

      The per-session policy runs when a client initiates a session. (A per-session policy is also known as an access policy.) Depending on the actions you include in the access policy, it can authenticate the user and perform other actions that populate session variables with data for use throughout the session.

#.  Click on the Create button on the far right

      +----------------------+---------------------------+----------------------------------+
      |General Properties    | Name                      |  Basic_policy                    |
      +----------------------+---------------------------+----------------------------------+
      |                      | Profile Type              |  All                             |
      +----------------------+---------------------------+----------------------------------+
      |                      | Profile Scope             |  Profile                         |
      +----------------------+---------------------------+----------------------------------+
      |                      | Customization Type        |  Modern                          |
      +----------------------|---------------------------|----------------------------------+
      |Language Settings     | Accepted Languages        |  English                         |
      +----------------------+---------------------------+----------------------------------+

      .. Note:: Customization Type is a newer setting that changes the look and feel of login pages.  For the traditional look you can **Standard**

#.  Click **Finished**
#.  Now we have a basic profile.  There were a number of other settings to modify and use in the profile.  For now we will focus just on the basics.
#.  From the **Access Profiles (Per-Session Policies)** section locate the **Basic_policy**
#.  There are two ways to edit the Policy piece of the profile.

      First way

      +----------------------------------------------------------------------------+
      | Click on the profile                                                       |
      +----------------------------------------------------------------------------+
      | Click on **Access Policy** from the top menu bar                           |
      +----------------------------------------------------------------------------+
      | Click on the link to **Edit Access Policy for Profile "Basic_policy"**     |
      +----------------------------------------------------------------------------+
      | This will take you to the Visual Policy Editor (VPE)                       |
      +----------------------------------------------------------------------------+

      Second way

      +-----------------------------------------------------------------------------------+
      | Locate the **Basic_policy** in the Profile list and follow the line to the right. |
      +-----------------------------------------------------------------------------------+
      | Middle of the line there will be an **Edit** link                                 |
      +-----------------------------------------------------------------------------------+
      | Click the **Edit** link                                                           |
      +-----------------------------------------------------------------------------------+

#.  Close the VPE (we will visit the VPE and policy in more detail later)
#.  Return to **Access** --> **Profiles/Policies** --> **Access Profiles (Per-Session Policies)**
#.  Click on the **Basic_policy** and explore the settings for the Profile.

      +----------------------+------------------------------------------------------------------------------------+
      | Settings             | Here you can manage settings for the profile. You may want to change timeouts, max |
      |                      | sessions and login attempts. These are settings specifically for this profile.     |
      +----------------------+------------------------------------------------------------------------------------+
      | Configurations       | These are more advanced options and covered in other labs                          |
      +----------------------+------------------------------------------------------------------------------------+
      | Language Settings    | You have to set this at creation.                                                  |
      +----------------------+------------------------------------------------------------------------------------+

      .. Note:: If you are unsure of the settings you need at profile creation you can see that you can return to the profile and make adjustments.

#.  Still in the profile click on **SSO/Auth Domain** at the top

      BIG-IP APM offers a number of Single Sign On (SSO) options.  The SSO/Auth Domain tab in a Per Session Profile is where you will select what SSO method to use for your application. In Task 6 we will cover the objects that need to be created in order to associate that SSO method to a policy.  At this time the drop down for the SSO Configuration will have a pre-built sso object we will use later.

#.  What is Domain Mode?

      Access Policy Manager (APM) provides a method to enable users to use a single login or session across multiple virtual servers in separate domains. Users can access back-end applications through multiple domains or through multiple hosts within a single domain, eliminating additional credential requests when they go through those multiple domains. With multi-domain support, you have the option of applying different SSO methods across different domains.

      .. Note:: When thinking Domain do not confuse this with Active Directory domain.  In this context domain refers to the DNS domain.  Example, app1.f5demo.com and app2.f5dmeo.com are in the f5demo.com DNS domain.

      .. Important:: To enable multi-domain support, all virtual servers must be on a single BIG-IP system and share the same access profile. All virtual servers must include all of the profiles that the access profile requires (for example, VDI, rewrite, server SSL, connectivity, and so on).

      APM provides the following benefits when using multi-domain support with SSO.

      - Users can sign out from all domains at once.
      - Users can move from one domain to another seamlessly. This eliminates the need re-run the access policy, and thus maintains the established session for the user.
      - Administrators can configure different cookie settings (Secure, Host/Domain and Persistent) for different domains, and for different hosts within same domain
      - Administrators can set up multiple SSO configurations to sign users in to multiple back-end applications for a single APM® session


#.  What are the options?

      +----------------------+-----------------------------------------------------------------------------------------+
      | Single Domain        | Choose this option for a single domain with a single sign on method                     |
      +----------------------+-----------------------------------------------------------------------------------------+
      | Multiple Domains     | This option allows for one policy and multiple SSO methods to multiple Virtual Servers  |
      +----------------------+-----------------------------------------------------------------------------------------+


#.  What is a Domain Cookie?

      By default, BIG-IP APM requires authentication for each access profile.  This can easily be changed by adding the domain cookie. For this section you will add the domain for your application. For example, if you have two applications app1.f5demo.com and app2.f5demo.com you would enter the domain f5demo.com for your domain cookie. Now your users can access each application and will only be prompted for authentication once.

#.  Cookie Options

      +----------------------+--------------------------------------------------------------------------------------------------------------------+
      | secure               |If the BIG-IP APM virtual server is configured with a Client SSL profile, select **Secure** (default setting) when  |
      |                      |configuring the BIG-IP APM SSO/Auth Domain cookie settings.                                                         |
      +----------------------+--------------------------------------------------------------------------------------------------------------------+
      | Persistent           |Session cookie persistence functions only on BIG-IP LTM and APM deployments. For BIG-IP APM  deployments with       |
      |                      |connectivity resources (such as Network Access, Portal Access, etc.), you cannot set BIG-IP APM cookies as          |
      |                      |**Persistent**. This is by design, as session cookie persistence can present a security risk. For some deployments  |
      |                      |of the BIG-IP APM system, as with Microsoft SharePoint, cookie persistence may be required. When you select cookie  |
      |                      |persistence, persistence is hard coded at 60 seconds.                                                               |
      +----------------------+--------------------------------------------------------------------------------------------------------------------+
      | HTTP Only            |For BIG-IP APM deployments with connectivity resources (such as Network Access, Portal Access, etc.), do not set    |
      |                      |BIG-IP APM cookies with the **HTTP Only** flag.                                                                     |
      +----------------------+--------------------------------------------------------------------------------------------------------------------+
      | Samesite             |New in version 16.x APM now has the option to enable Samesite attribute for session cookies. This attribute         |
      |                      |enforces samesite usage and prevents the cookies from being included with cross-site requests. It can have one of   |
      |                      |these values:                                                                                                       |
      |                      |                                                                                                                    |
      |                      |- Strict: Only include the cookie with requests originating from the same site as the cookie                        |
      |                      |- Lax:  Include the cookie with same-site requests and with top-level cross-site navigations that use a safe HTTP   |
      |                      |  method. The cookie is not sent with cross-site sub-requests such as calls to load images, but is sent when a user |
      |                      |  navigates to the URL from an external site, such as by following a link.                                          |
      |                      |- None: Do not enforce the same-site origin. If selected, requests must follow the HTTPS protocol, and the Secure   |
      |                      |  cookie attribute must be set.                                                                                     |
      +----------------------+--------------------------------------------------------------------------------------------------------------------+

#.  SSO Configuration

      This drop down is where you will find all the SSO objects that you have configured on this BIG-IP appliance. If you want to enable an SSO method for an application first you must configuration the SSO object and then select in this section of the policy.

      .. Note:: Task 6 will review SSO methods and configuration.

#.  Multiple domains

      If you return to the radio buttons and select Multiple Domains new options will appear.  When this configuration is complete a user will be able to connect to any of the virtual servers and authentication will only be requested once.  Subsequent connections in the domain group should not prompt for additional login. The caveat is that all Virtual Servers must share this same policy.

      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Primary Authentication URI             |Specifies the address of your primary authentication URI. An example would be https://login.acme.com. This is where |
      |                                        |the user session is created. As long as you provide the URI, your users are able to access multiple backend         |
      |                                        |applications from multiple domains and hosts without requiring them to re-enter their credentials because the user  |
      |                                        |session is stored on the primary domain. This is a required field if you selected Multiple Domains domain mode.     |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Authentication Domain Configuration    |An example domain would be acme.com                                                                                 |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Authentication Domains                 |To add the applications click on **Add** at the far right and enter the host. Example, app1.acme.com, app2.acme.com |
      |                                        |If you have and SSO method created select the SSO method from the drop down box.  This can be edited later to add an|
      |                                        |SSO method.                                                                                                         |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+


#.  Logs

#.  The log profile we created earlier is now listed here.  The Default log profile is attached but we can remove that and add the **Basic_log_profile**
#.  Click Update.

That concludes the review of the Per Session policy.

.. Note:: A per session profile is required (even if it is blank) to be deployed with a per request policy

#.  From the left menu navigate to **Access** --> **Profiles/Policies** --> **Per Request Policies**

APM executes per-session policies when a client attempts to connect to the enterprise. After a session starts, a per-request policy runs each time the client
makes an HTTP or HTTPS request. Because of this behavior, a per-request policy is particularly useful in the context of a Secure Web Gateway or Zero Trust
scenario, where the client requires re-verification on every request, or changes based on gating criteria.

A per-request policy can include a subroutine, which starts a subsession. Multiple subsessions can exist at one time. You can use nearly all of the same agents
in per-request policies that you can use in per-session policies. However, most of the agents (including authentication agents) have to be used in a subroutine
in per-request policies.

#. Click **Create**

+----------------------+---------------------------+----------------------------------+
|General Properties    | Name                      |  Basic_prp_policy                |
+----------------------+---------------------------+----------------------------------+
|                      | Profile Type              |  All                             |
+----------------------+---------------------------+----------------------------------+
|                      | Incomplete Action         |  Deny                            |
+----------------------+---------------------------+----------------------------------+
|                      | Customization Type        |  Modern                          |
+----------------------+---------------------------+----------------------------------+
|Language Settings     | Accepted Languages        |  English                         |
+----------------------+---------------------------+----------------------------------+

#. Click **Edit**

A per request policy creation will work the same way as a per session policy allowing you to create various box, subroutines and macros.  If you click on the plus between
Start and Allow a new box will appear and you can explore the various components that can be added.  At this time we will leave the policy blank and return to populate it
in later tasks.

#. Policy sync

BIG-IP APM Policy Sync maintains access policies on multiple BIG-IP APM devices while adjusting appropriate settings for objects that are specific to device locations,
such as network addresses. You can synchronize policies from one BIG-IP APM device to another BIG-IP APM device, or to multiple devices in a device group.

A sync-only device group configured for automatic and full sync is required to synchronize access policies between multiple devices.

.. Important:: USE WITH CAUTION.  This is an advanced feature and you should consult with your F5 Account team or Professional Services before implementing this configuration.

.. Note:: In BIG-IP 13.1.0, a maximum of either BIG-IP APM systems are supported in a sync-only group type.

#. What are customization and localization?

Customization and localization are ways to change the text and the language that users see, and to change the appearance of the user interface that Access Policy Manager
presents to client users. Customization provides numerous settings that let you adapt the interface to your particular operation. Localization allows you to use different
languages in different countries.

#. About the Customization tool

The Customization tool is part of Access Policy Manager (APM). With the Customization tool, you can personalize screen messages and prompts, change screen layouts,
colors, and images, and customize error messages and other messages using specific languages and text for policies and profiles developed in APM.

You can customize settings in the Basic Customization view (fewer settings) or change the view to General Customization (many settings). In the General Customization
view, you can use the Customization tool in the BIG-IP admin console, or click Popout to open it in a separate browser window. In either view, you can click Preview
to see what an object (such as Logon page or Deny Ending Page) will look like.

After you personalize settings, remember to click the **Save** icon to apply your changes.

#. About basic, general, and advanced customization

The Customization tool provides three views that you can use to customize the interface. The General Customization view provides the greatest number of options
and is where most of the customization takes place.

+----------------------+--------------------------------------------------------------------------------------------------------------------+
| View                 | Description                                                                                                        |
+======================+====================================================================================================================+
| Basic                |Basic customization provides a limited set of options intended for quick modification of the objects that are       |
| Customization        |commonly displayed to users. This is the default customization view. Use this to configure basic look and feel      |
|                      |for pages, and common text labels and captions for resources on the webtop. Different options exist depending on    |
|                      |the Customization Type selected when the policy was created.                                                        |
+----------------------+--------------------------------------------------------------------------------------------------------------------+
| General              |This view provides a tree structure containing all the configuration elements, and more detailed options to         |
| Customization        |customize objects, such as:                                                                                         |
|                      |                                                                                                                    |
|                      |- The size, color, and placement of forms and screens.                                                              |
|                      |- The look and feel of objects with more opportunities to replace images.                                           |
|                      |- Text on the screen, including headers and footers.                                                                |
|                      |- Messages, including installation and error messages.                                                              |
|                      |                                                                                                                    |
|                      |Any text or image that you can customize using the visual policy editor, can also be adjusted using the general     |
|                      |customization UI. Different options exist depending on the Customization Type selected when the policy was created, |
|                      |and which elements were added to the access or per-request policy.                                                  |
+----------------------+--------------------------------------------------------------------------------------------------------------------+
| Advanced             |Advanced customization provides direct access to PHP, Cascading Style Sheets (CSS), JavaScript, and HTML files that |
| Customization        |you can edit to control the display and function of web and client pages in Access Policy Manager.                  |
+----------------------+--------------------------------------------------------------------------------------------------------------------+

.. Note:: See the `APM Customization guide <https://techdocs.f5.com/en-us/bigip-16-0-0/big-ip-access-policy-manager-customization.html>`__ for further details on customization

#. Click on --> **Access** --> **Profiles/Policies** --> **Customization**
#. Under **Available Profiles** choose the /Common/Basic_policy
#. Select Language:  **English**
#. Let's upload a new image.  Click **Upload New Image**
#. Choose an image from the selection and click **Open**
#. Pick a Background color
#. Pick a Header Background color
#. Change the footer Text
#. Click on the **Preview** button
#. Choose **Access Profiles** --> **/Common/Basic_policy** --> **Access Policy** --> **Ending pages** -- **Deny**

Bonus Answer:  Why don't we see logon pages?

.. Hint::  What is in the policy so far?


Task 5: Authentication
----------------------------

BIG-IP APM serves as an authentication gateway or proxy. As an authentication proxy, BIG-IP APM provides separate client-side and server-side authentication. Client-side
authentication occurs between the client and BIG-IP APM. Server-side authentication occurs between BIG-IP APM and servers.

Loose coupling between the client-side and server-side layers allows for a rich set of identity transformation services. Combined with a Visual Policy Editor and an expansive
set of access iRules functionality, BIG-IP APM provides flexible and dynamic identity and access, based on a variety of contexts and conditions.

For example, a client accessing Microsoft SharePoint through BIG-IP APM in a corporate environment may silently authenticate to BIG-IP APM with NT LAN Manager (NTLM) or Kerberos
credentials. On leaving that environment, or on using a different non-sanctioned device, the client may be required to go through another potentially stronger authentication,
such as a smart card or other client certificate, RSA SecurID, or one-time passcode. You can require additional device vetting such as file, folder, and registry checks and
antivirus and firewall software validation.

A BIG-IP APM authentication and SSO features access and identity security posture can automatically change depending on environmental factors, such as who or where the user is,
what resource the user is accessing, or when or with what method the user is attempting to gain access.

Data centers and Cloud deployments often face the challenge of offering multiple applications with different authentication requirements. You can deploy BIG-IP APM to consolidate
and enforce all client-side authentication into a single process. BIG-IP APM can also perform identity transformation on the server side to authenticate to server services using
the best-supported methods. This can reduce operational costs since applications remain in the most-supported and documented configurations. Common examples of identity
transformation are client-side public key infrastructure (PKI) certificate to server-side Kerberos and client-side HTTP form to server-side HTTP Basic.

The following figure shows BIG-IP APM acting as an authentication gateway. Information received during pre-authentication is transformed to authenticate to multiple enterprise
applications with different requirements.

|image25|

#. Client-side authentication

Client-side authentication involves the client (typically a user employing a browser) accessing a BIG-APM virtual server and presenting identity. This is called authentication, authorization, and accounting (AAA).

BIG-IP APM supports industry standard authentication methods, including:

- NTLM
- Kerberos
- Security Assertion Markup Language (SAML)
- Client certificate
- RSA SecurID
- One-time passcode
- HTTP Basic
- HTTP Form
- OAuth 2.0
- OpenId Connect

After access credentials are submitted, BIG-IP APM validates the listed methods with industry-standard mechanisms, including:

- Active Directory authentication and query
- LDAP and LDAPS authentication and query
- Remote Authentication Dial-in User Service (RADIUS)
- Terminal Access Controller Access Control System (TACACS)
- Online Certificate Status Protocol (OCSP) and Certificate Revocation List Distribution Point (CRLDP) (for client certificates)
- Local User Database authentication

#. Go to **Access** --> **Authentication** --> **Active Directory**
#. Click create

+----------------------+-----------------------------+----------------------------------+
|General Properties    | Name                        |  Basic_policy_aaa                |
+----------------------+-----------------------------+----------------------------------+
|Configuration         | Domain Name                 |  f5lab.local                     |
+----------------------+-----------------------------+----------------------------------+
|                      | Server Connection           |  Use Pool                        |
+----------------------+-----------------------------+----------------------------------+
|                      | Domain Controller Pool Name |  basic_ad_pool                   |
+----------------------+-----------------------------+----------------------------------+
|                      | IP Address                  |  10.1.20.7                       |
+----------------------+-----------------------------+----------------------------------+
|                      | Hostname                    |  dc1.f5lab.local                 |
+----------------------+-----------------------------+----------------------------------+
|                      | Admin Name                  |  admin                           |
+----------------------+-----------------------------+----------------------------------+
|                      | Admin Password              |  admin                           |
+----------------------+-----------------------------+----------------------------------+

You have now created an object that can be used to facilitate Active Directory authentication in front of any application.  The application itself does not need to require authentication. If
you were to deploy a policy with AD Auth on a Virtual Server for a web application the policy would preset a login page, prompt for credentials, verify the credentials against this AD object
before allowing a user to access the web application.

#. Go to **Access** --> **Profiles/Policies** --> **Access Profiles (Per-Session Policies)**
#. Locate the Basic_policy and click **Edit**
#. Click the **+** symbol between Start and Deny.
#. From the **Logon** tab select the **Logon Page** radio button
#. Click **Add Item**
#. Notice that you can add fields and change the names of the fields.  Click **Save**
#. Click the **+** between **Logon Page** and Deny
#. Click the **Authentication** tab
#. Choose the **AD Auth** radio button and click **Add Item**
#. Under the **Type** field click on the drop down menu and choose the newly created AAA server **Basic_policy_aaa**
#. Click **Save**
#. Click on the **Deny** end point and choose **Allow** then click **Save**
#. Click **Apply Access Policy**

Now you have a basic policy with AD Authentication that you can leverage for Web Pre-Authorization in front of any application.

Task 6: Single Sign-On
----------------------------
Client side and server side are loosely coupled in the authentication proxy. Because of this, BIG-IP APM can transform client-side identity values of one type can into server-side identity values of another type. You configure SSO within an SSO profile, which is applied to an access profile. The system triggers SSO at the end of successful access policy evaluation and on subsequent client-side requests.

BIG-IP APM supports industry standard authentication methods, including:

    NTLM
    Kerberos
    HTTP Basic
    HTTP Form
    Security Assertion Markup Language (SAML)

Note: Client-side authentication methods outnumber server-side methods. This is because BIG-IP APM does not transmit client certificate, RSA SecurID, or one-time passcodes to the server on the client’s behalf.

For more information on BIG-IP APM server-side authentication, refer to BIG-IP Access Policy Manager: Authentication and Single Sign-On.

Note: For information about how to locate F5 product manuals, refer to K98133564: Tips for searching AskF5 and finding product documentation


Task 7: Federation
----------------------------

Authentication and authorization

Most organizations require users to verify their identity (authenticate). Additionally, most organizations control (authorize) the resources each user can access and the actions they can take when
using their applications (services), based on their identity.

Identity providers and service providers

Federation is an agreement between organizations to trust user authentication and/or authorization from one organization (identity provider (IdP)) to access services from the other organizations
in the group (service providers (SPs)). In this model, one organization can be both the IdP and an SP or simply an SP.

Federation provides many benefits to organizations and users, including single sign-on (SSO), which enables users to avoid logging in to each SP. For more information about BIG-IP APM and SSO, refer
to Authentication and SSO.

Standard web security protocols

To manage and map identities across geographies, SPs, and services, federation relies on common standards and protocols.

SAML 2.0

Security Assertion Markup Language (SAML) 2.0 is an open standard for exchanging authentication and authorization data between SPs. SAML 2.0 is an XML-based language that shares messages containing
user information (assertions) while protecting their identity, thereby enabling a trusted relationship between SPs to perform services. SAML 2.0 relies on Simple Object Access Protocol (SOAP) to make
web service calls.

Faster and easier

However, in recent years, representational state transfer (REST) has gained popularity as a light-weight alternative to SOAP that makes web service calls more quickly. Developers combine REST with
JSON to transmit user data, instead of XML, because it is easier to implement and contains small, compact messages. This combination is the basis for OAuth 2.0 and OpenID Connect.

OAuth 2.0

OAuth 2.0 is an open standard for exchanging authorization data—but not authentication data—between SPs. It is a set of defined process flows for accessing resources on behalf of the user (delegated
authorization).

In this model, the user (resource owner) has a resource hosted by one SP (on a resource server) that they want to make available to another SP (client), such as importing a list of contacts. The
resource server must authorize the client’s access (using an authorization server) on behalf of the user. The resource owner does not sign in to the client, which requires authentication; however,
the resource owner may be prompted to give consent to authorize the client’s access. For more information about BIG-IP APM and OAuth 2.0, refer to OAuth authorization.

OpenId Connect

OpenId Connect is an open standard for exchanging authentication data—but not authorization data—between SPs. OpenId Connect uses OAuth 2.0 and adds additional steps over its process flows to
perform authentication. In short, when an authorization server is enabled for OpenId Connect, it provides an ID token in addition to an access token.

In this model, users use their account from one SP to sign in to another, such as using a Google or Facebook account to sign in to another website. The SP owning the account is the IdP with the
authorization server and the other SP is the client.

BIG-IP APM federation with SAML

BIG-IP APM supports SAML 2.0 and can act as the IdP for popular SPs, such as Microsoft Office 365 and Salesforce. The system supports both IdP- and SP-initiated identity federation deployments.

IdP-initiated federation with BIG-IP APM

Figure 3.1 IdP-initiated SAML

    The user logs in to the BIG-IP APM IdP and the system directs them to the BIG-IP APM webtop.
    The user selects the SP they want, such as Salesforce.
    The system retrieves any required attributes from the user data store to pass on to the SP.
    The system uses the browser to direct the request to the SP, along with the SAML assertion and any required attributes.

SP-initiated federation with BIG-IP APM

Figure 3.2 SP-initiated SAML

    The user logs in to the SP, such as Salesforce.
    The SP uses the browser to redirect the user back to the BIG-IP APM IdP.
    The BIG-IP APM IdP prompts the user to log in.
    The system retrieves any required attributes from the user data store to pass on to the SP.
    The system uses the browser to send the SAML assertion and any required attributes to the SP.

Using a custom SP portal instead of the BIG-IP APM webtop for federation

Some enterprises do not want to use the built-in BIG-IP APM webtop as the portal to their SPs. Instead, they want to create their own, customized, external portal. For more information about the
webtop, refer to Webtop.

As of BIG-IP APM 14.0, you can use a custom, external portal when you can use SAML inline SSO for federation. You must meet the following conditions:

    Federation is SP-initiated. That is, when a user visits an SP, the BIG-IP APM acts as the IdP.
    You have an existing per-session policy.
    Users visit the SP using the BIG-IP in BIG-IP LTM + BIG-IP APM mode.

Using SAML inline SSO

When you use SAML inline SSO, when BIG-IP APM receives an SP authentication request, it generates a SAML assertion on-the-fly to automatically sign in the user. The BIG-IP APM IdP is chained so
that it accepts an assertion from another SAML IdP to create the session. The system constructs session data using the same method.

How it works

    You put an internal SP behind the virtual address for the IdP.
    You configure the internal SP server in a typical BIG-IP LTM pool on the virtual server. An SP that is load balanced by the BIG-IP can be either a SAML-enabled application or a third-party
    SAML SP.
    When the client transmits an authentication request to the BIG-IP APM IdP, the system generates assertions for the application.

Figure 3.3 SAML inline SSO

Figure 3.4 SAML inline SSO request flow

    The user attempts to access a resource and BIG-IP APM starts access policy evaluation.
    The system authenticates the user.
    The user resends the original request.
    The BIG-IP system load balances the request to a pool member associated with the virtual server.
    When the user doesn’t have a valid session, the internal SP or SAML-enabled application generates an authentication request and redirects the user to the IdP.
    The system forwards the application response to the user, the browser evaluates it, and it results in an authentication request.
    The user submits the authentication request back to the BIG-IP virtual server.
    The BIG-IP APM IdP validates the request and, when successful, generates an assertion.
    The system modifies the client’s HTTP request and releases it to the internal SP.
    The internal SP receives and validates the assertion for the BIG-IP system.
    The SP either provides access to the application or provides an error to the user, depending on the result of validation.

For more information about using SAML inline SSO, refer to K06743491: Overview of BIG-IP APM SAML inline SSO.

Using SAML inline SSO with multiple unique host names

Typically, you identify, load balance, and secure an SP by giving it a unique virtual address and host name, such as salesforce.f5.com. However, when you have multiple SPs with unique host names
that you want to locate behind a single BIG-IP IdP, you don’t have to configure multiple BIG-IPs to act as IdP for each SP. That approach quickly becomes overly complex.

Instead, you can share a single access profile across all virtual addresses participating in SAML inline SSO. In this model, there is a main authentication virtual server that performs authentication
and generates SAML assertions when requested. The SPs on other virtual servers use the same access profile. For more information, refer to the SP-initiated multi-domain inline SAML SSO section in
K06743491: Overview of BIG-IP APM SAML inline SSO.


Task 8: Connectivity/VPN
----------------------------
Run Automation for Solution 1.

Policy Walk-Through

|image001|

#.  A user enters their credentials into the logon page agent.
    - Those credentials are collected, stored as the default system session variables of session.logon.last.username and session.logon.last.password.

#.  The AD Auth Agent validates the username and password session variables against the configured AD Domain Controller.
#.  The user is assigned resources defined in the Advanced Resource Assign Agent
#.  The user is granted access via the Allow Terminal
#.  If unsuccessful, the user proceeds down the fallback branch and denied access via the Deny Terminal

Policy Agent Configuration

The Logon Page contains only the default setting

|image002|

The AD Auth agent defines the AAA AD Servers that a user will be authenticated against.  All Setting are the default.

|image003|


The Advanced Resource Assign agent grants a user access to the assigned resources.

|image004|


Supporting APM Objects

Network Access Resource

The Properties page contains the Caption name **VPN**.  This is the name displayed to a user.

|image005|


- The Network Settings tab assigns the **lease pool** of ip addresses that will be used for the VPN.
- Split Tunneling is configured to permit only the **10.1.20.0/24** subnet range inside the VPN.

|image006|


Lease Pool

A single address of **10.1.20.254** is assigned inside the lease pool.

|image007|


Webtop Sections

A single section is configured to display a custom name.

|image008|


Webtop

- A Full Webtop was defined with modified default settings.
- The Minimize to Tray box is **checked** to ensure the Webtop is not displayed when a user connects to the VPN.

|image009|

The Policy from a user's perspective


#. The connects to https://solution1.acme.com with the following credentials

   - Username: user1
   - Password: user1

|image010|

#. Once authenticated the user is presented a Webtop with a single VPN icon.

|image011|

#. Assuming the VPN has already been installed the user is notified that the client is attempting to start

|image012|

#. A popup opens displaying the status of the VPN connection.  The status will eventually become **Connected**

|image013|



Task 9: API Protection
----------------------------
An API protection profile is the primary tool that Access Policy Manager administrators use to safeguard API servers. Protection profiles define groups of related RESTful APIs used by applications.
The protection profile contains a list of paths that may appear in a request. The system classifies requests and sends them to specific API servers.

The simplest way to create an API protection profile and establish API protection is using an OpenAPI Spec file to import the details of the APIs. If you use an OpenAPI Spec file, Access Policy
Manager automatically creates the following (depending on what's included in the spec file):

- API Protection Profile
- Paths
- API servers
- Responses
- Per-request policy with a Request Classification agent and a subroutine containing an OAuth scope check agent


To enable API protection, the API Protection Profile must be associated with a virtual server. If using API Protection, the virtual server can have only one API Protection Profile associated with it.
You cannot select other access profiles or per-request policies in that virtual server.


Task 10: Secure Web Gateway
----------------------------

About APM Secure Web Gateway
BIG-IP Access Policy Manager (APM) implements a Secure Web Gateway (SWG) for outbound access by providing access control based on URL categorization to forward proxy. With APM, you can create
a configuration to protect your network assets and end users from threats, and enforce a use and compliance policy for Internet access. Users that access the Internet from the enterprise go through
APM, which can allow or block access to URL categories or indicate that the user should confirm the URL before access can be allowed.
Benefits of using APM for web access
BIG-IP Access Policy Manager (APM®) controls basic website access purely based on user-defined URL categories. This feature is a part of base APM functionality, without requiring an SWG subscription.
The benefits include:

    URL filtering capability for outbound web traffic.
    Monitoring and gating outbound traffic to maximize productivity and meet business needs.
    User identification or authentication (or both) tied to logging, and access control compliance and accountability.
    Visibility into SSL traffic.
    Reports on blocked requests and all requests. (Reports depend on event logging settings.)
    Ability to interactively request additional authentication for sensitive resources and provide time-limited access to them in subsessions.
    Ability to interactively request confirmation before allowing or blocking access to resources that might not, in all instances, provide benefit to the business. Confirmation and access take place
    in a subsession with its own lifetime and timeout values.

Secure Web Gateway subscription benefits
A BIG-IP Access Policy Manager (APM) with a Secure Web Gateway (SWG) subscription provides these benefits over those supplied by APM alone:

    A database with over 150 predefined URL categories and 60 million URLs.
    A service that regularly updates the URL database as new threats and URLs are identified.
    Identification of malicious content and the means to block it.
    Web application controls for application types, such as social networking and Internet communication in corporate environments.
    Support for Safe Search, a search engine feature that can prevent offensive content and images from showing up in search results.
    A dashboard with statistical information about traffic logged by the BIG-IP system for SWG. Graphs, such as Top URLs by Request Count and Top Categories by Blocked Request Count, summarize
    activities over time and provide access to underlying statistics.

SWG subscription benefits extend these APM benefits:

    URL filtering capability for outbound web traffic.
    Monitoring and gating outbound traffic to maximize productivity and meet business needs.
    User identification or authentication (or both) tied to logging, and access control compliance and accountability.
    Visibility into SSL traffic.
    Reports on blocked requests and all requests. (Reports depend on event logging settings.)
    Ability to interactively request additional authentication for sensitive resources and provide time-limited access to them in subsessions.
    Ability to interactively request confirmation before allowing or blocking access to resources that might not, in all instances, provide benefit to the business. Confirmation and access take
    place in a subsession with its own lifetime and timeout values.

What happens when the Secure Web Gateway subscription expires?
Secure Web Gateway (SWG) subscriptions expire periodically depending on the subscription length your company purchased. The system displays a warning message when the subscription is about to expire.
If you fail to renew the subscription, your organization will lose access to SWG functionality, including category lookup within the Forcepoint URL database, request analytics, and response analytics.
Depending on how the per-request policies implementing SWG are configured, requests to access the Internet through the forward proxy may fail.
If the SWG subscription expires and Reset on Failure
is enabled in the Category lookup/Analytics agents, a TCP reset occurs whenever the category lookup fails. Clients receive no response from the server in this case and requests fail. You can configure
a per-request policy to branch on failure and specify what you want to happen (such as Allow, Reject, or specify another path). For maximum protection, it is recommended that you renew the SWG
subscription before it expires.
About the URL database URL categories
The URL database is available only on a BIG-IP-APM system with an SWG subscription.
The Secure Web Gateway URL database supplies over 150 URL categories and identifies over 60 million URLs that fit within these categories. In addition, you can create custom categories if needed and
add URLs to any category, custom or otherwise. You can also use custom categories to define blacklists and whitelists.
About user-defined URL categories
Without a URL database, an administrator tasked with treating only a few URLs differently can specify criteria for matching those few URLs in a simple URL Branching
action in a per-request policy. An administrator who must categorize and filter a large number of URLs can, however, do this using Access Policy Manager (APM) user-defined URL categories.
About APM session management cookies and forward proxy
When Access Policy Manager (APM®) acts as a forward proxy, APM does not use session management cookies. If presented with an APM session management cookie while acting as a forward proxy, APM ignores
the cookie.



Task 11: Access Control Lists
-----------------------------
BIG-IP APM uses ACLs to restrict user access to specified internal hosts, ports and/or URIs. For an ACL to have an effect on traffic, it must be assigned to a user session. ACLs are applied to
all access methods by default.

An ACL consists of a list of access control entries (ACEs). These entriescan work on L4, L7, or both.

In addition to source (ip:port), destination (ip:port), and Scheme + URI (for L7), each ACL and its entries has a unique acl-order field that determines its priority.

Important: Important If no webtop is assigned during access policy execution, the session is in Web Access Management/LTM-APM mode.

During access policy execution, BIG-APM assigns a list of ACLs to a user session. BIG-IP APM tests ACLs and ACEs in order, based on their priority in the respective list. To make sure of compliance
with network use policies, the order must be correct.

If there are no ACLs assigned to a session by the access policy, the default behavior for the session traffic is Allow.

If a default deny stance is required, an ACL with a Deny All entry should be configured. This ACL should be assigned to the user session at the end of the ACL entry list (that is, its order field
value should be highest number). BIG-IP APM rejects any connection not matched by a previous entry.

ACLs can be configured to create log entries when they are matched. These log entries appear in the /var/log/pktfilter log file. You can view them in the Configuration utility by going to System >
Logs > Packet Filter.

When BIG-IP APM applies an ACL is applied to an access policy, the policy dynamically creates an internal layered virtual server that the system uses to apply the ACL. However, if the BIG-IP APM
virtual server targets a layered virtual server, such as an SSO layered virtual server, traffic bypasses the dynamically-created internal layered virtual server and the ACL is not applied.

For more information, refer to K14219: An L4 ACL is not applied to the network access tunnel when a virtual server is used.

Dynamic ACLs

A dynamic ACL is an ACL created on and stored in an LDAP, RADIUS, or ActiveDirectory server. A dynamic ACL action dynamically creates ACLs based on attributes from the AAA server. Because a dynamic
ACL is associated with a user directory, you can use it to assign ACLs specifically per the user session. BIG-IP APM supports dynamic ACLs in an F5 ACL format, and in a subset of the Cisco ACL format.

When using dynamic ACLs, make sure that the dynamic ACL appears after authentication in an access policy since its actions are determined by attributes received from an authentication server. If it’s
configured in a Cisco format, make sure the dynamic ACL contains the prefix ip:inacl#.

For more information, refer to Configuring Dynamic ACLs in BIG-IP Access Policy Manager: Implementations.

Note: For information about how to locate F5 product manuals, refer to K98133564: Tips for searching AskF5 and finding product documentation.


Task 12: Webtops
----------------------------
A webtop is a BIG-IP APM customizable landing page. At the end of successful access policy execution and final client POST to complete the access policy, the client can be redirected to a BIG-IP
APM webtop.

Webtop types

BIG-IP APM supports three types of webtop:

    Network Access—Contains JavaScript and browser plug-ins to start Network Access on supported browsers or BIG-IP Edge Client.
    Portal Access—Contains a 302 redirect to the Portal Access encoded URL.
    Full webtop—Contains a complex set of JavaScript, XML, and HTML to present a menu to users. Assigned resources are presented to the user as icons. A full webtop also allows the starting of
    Network Access from a browser and BIG-IP Edge Client.

Note: If no webtop is assigned during access policy execution, the session is in Web Access Management/LTM-APM mode.

Features

The full webtop can replace intranet or extranet portal pages, offering users a centralized place to start assigned applications.

Network Access and Portal Access webtops automatically place users into a specific application assigned during access policy execution.

BIG-IP APM provides a basic customization framework allowing administrators to alter images, color, and layout settings.

The advanced customization framework allows web developers to completely replace all BIG-IP APM-delivered web content, including webtops, logon pages, and error pages.

Implementation

In BIG-IP 12.0 and later, Webtop Sections can be assigned to user during Access Policy Execution.

Webtop sections can contain up to 300 ordered references to APM resources and are available only with a full webtop.




Lab 2 is now complete.

.. |accessjh| image:: /class1/module1/media/lab01/setup/accessjh.png
.. |accessportal| image:: /class1/module1/media/lab01/setup/accessportal.png
.. |101intro| image:: /class1/module1/media/lab01/setup/101intro.png
.. |guioverview| image:: /class1/module1/media/lab01/setup/guioverview.png
.. |issues| image:: /class1/module1/media/lab01/setup/issues.png
.. |image4| image:: /class1/module1/media/lab01/image4.png
.. |image5| image:: /class1/module1/media/lab01/image5.png
.. |image01| image:: /class1/module1/media/lab01/image01.png
.. |image02| image:: /class1/module1/media/lab01/image02.png
.. |image03| image:: /class1/module1/media/lab01/image03.png
.. |image06| image:: /class1/module1/media/lab01/image6.png
.. |image07| image:: /class1/module1/media/lab01/image7.png
.. |image08| image:: /class1/module1/media/lab01/image8.png
.. |image09| image:: /class1/module1/media/lab01/image9.png
.. |image10| image:: /class1/module1/media/lab01/image10.png
.. |image11| image:: /class1/module1/media/lab01/iamge11.png
.. |image12| image:: /class1/module1/media/lab01/image12.png
.. |image13| image:: /class1/module1/media/lab01/image13.png
.. |image14| image:: /class1/module1/media/lab01/image14.png
.. |image15| image:: /class1/module1/media/lab01/image15.png
.. |image16| image:: /class1/module1/media/lab01/image16.png
.. |image17| image:: /class1/module1/media/lab01/image17.png
.. |image18| image:: /class1/module1/media/lab01/image18.png
.. |image19| image:: /class1/module1/media/lab01/image19.png
.. |image20| image:: /class1/module1/media/lab01/image20.png
.. |image21| image:: /class1/module1/media/lab01/image21.png
.. |image22| image:: /class1/module1/media/lab01/image22.png
.. |image23| image:: /class1/module1/media/lab01/image23.png
.. |image25| image:: /class1/module1/media/lab01/image25.png
.. |sessionid| image:: /class1/module1/media/lab01/sessionid.png
.. |activesessions| image:: /class1/module1/media/lab01/activesessions.png
.. |killsession| image:: /class1/module1/media/lab01/killsession.png

.. |image001| image:: /class1/module1/media/lab01/001.png
.. |image002| image:: /class1/module1/media/lab01/002.png
.. |image003| image:: /class1/module1/media/lab01/003.png
.. |image004| image:: /class1/module1/media/lab01/004.png
.. |image005| image:: /class1/module1/media/lab01/005.png
.. |image006| image:: /class1/module1/media/lab01/006.png
.. |image007| image:: /class1/module1/media/lab01/007.png
.. |image008| image:: /class1/module1/media/lab01/008.png
.. |image009| image:: /class1/module1/media/lab01/009.png
.. |image010| image:: /class1/module1/media/lab01/010.png
.. |image011| image:: /class1/module1/media/lab01/011.png
.. |image012| image:: /class1/module1/media/lab01/012.png
.. |image013| image:: /class1/module1/media/lab01/013.png
