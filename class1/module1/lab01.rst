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

      +----------------------+---------------------------+----------------------------------+
      |General Properties    | Name                      |  Basic_policy                    |
      +----------------------+---------------------------+----------------------------------+
      |                      | Profile Type              |  All                             |
      +----------------------+---------------------------+----------------------------------+
      |                      | Profile Scope             |  Profile                         |
      +----------------------+---------------------------+----------------------------------+
      |                      | Customization Type        |  Modern                          |
      +----------------------+---------------------------+----------------------------------+
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

      If you return to the radio buttons and select Multiple Domains new options will appear.  When this configuration is complete a user will be able to connect to any of the virtual servers associated and authentication will only be requested once.  Subsequent connections in the domain group should not prompt for additional login. The caveat is that all Virtual Servers must share this same policy.

      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Primary Authentication URI             |Specifies the address of your primary authentication URI. An example would be https://login.acme.com. This is where |
      |                                        |the user session is created. As long as you provide the URI, your users are able to access multiple backend         |
      |                                        |applications from multiple domains and hosts without requiring them to re-enter their credentials because the user  |
      |                                        |session is stored on the primary domain. This is a required field if you selected Multiple Domains domain mode.     |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Primary Cookie Options                 |Secure (see above for cookie explanation)                                                                           |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Cookie                                 |Example:  **Domain**  acme.com                                                                                      |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | Cookie Options                         |Seucre (see above for cookie explanation)                                                                           |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+
      | SSO Configuration                      |You can set the SSO method for the domain or you can set individual SSO methods per host                            |
      +----------------------------------------+--------------------------------------------------------------------------------------------------------------------+

      |multidomain|

      .. Important:: We will not be configuring this function in this lab.  These are all examples.  For more information on `SSO/Auth Domains <https://techdocs.f5.com/en-us/bigip-16-0-0/big-ip-access-policy-manager-single-sign-on-concepts-configuration/single-sign-on-and-multi-domain-support.html>`_

#.  From the top menu bar click on **Logs**
#.  The log profile we created earlier is now listed here.  The Default log profile is attached but we can remove that and add the **Basic_log_profile**
#.  Click Update.

    That concludes the review of the Per Session policy.

    .. Note:: A per session profile is required (even if it is blank) to be deployed with a per request policy

**Per Request policies**

#.  From the left menu navigate to **Access** --> **Profiles/Policies** --> **Per Request Policies**

      APM executes per-session policies when a client attempts to connect to the enterprise. After a session starts, a per-request policy runs each time the client makes an HTTP or HTTPS request. Because of this behavior, a per-request policy is particularly useful in the context of a Secure Web Gateway or Zero Trust scenario, where the client requires re-verification on every request, or changes based on gating criteria.

      A per-request policy can include a subroutine, which starts a subsession. Multiple subsessions can exist at one time. You can use nearly all of the same agents in per-request policies that you can use in per-session policies. However, most of the agents (including authentication agents) have to be used in a subroutine in per-request policies.

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

      A per request policy creation will work the same way as a per session policy allowing you to add various items to the main policy and create macros. In addition a per request policy can also contain subroutines.

      .. Note:: A per-request policy subroutine is a collection of actions. What distinguishes a subroutine from other collections of actions (such as macros), is that a subroutine starts a subsession that, for its duration, controls user access to specified resources. If a subroutine has an established subsession, subroutine execution is skipped. A subroutine is therefore useful for cases that require user interaction (such as a confirmation dialog or a step-up authentication), since it allows skipping that interaction in a subsequent access.
      You cannot use subroutines in macros within per-request policies.
      Subroutine properties specify subsession timeout values, maximum macro loop count, and gating criteria. You can reauthenticate, check for changes on the client, or take other actions based on timeouts or gating criteria.

      .. Note:: A subsession starts when a subroutine runs and continues until reaching the maximum lifetime specified in the subroutine properties, or until the session terminates. A subsession populates subsession variables that are available for the duration of the subsession. Subsession variables and events that occur during a subsession are logged. Multiple subsessions can exist at the same time. The maximum number of subsessions allowed varies across platforms. The total number of subsessions is limited by the session limits in APM (128 * max sessions). Creating a subsession does not count against the license limit.

#. If you click on the plus between Start and Allow a new box will appear and you can explore the various components that can be added.  At this time we will leave the policy blank and return to populate it in later tasks.

**Policy Sync**

#. Click on **Access** --> **Profiles/Policies** --> **Policy sync**

      BIG-IP APM Policy Sync maintains access policies on multiple BIG-IP APM devices while adjusting appropriate settings for objects that are specific to device locations, such as network addresses. You can synchronize policies from one BIG-IP APM device to another BIG-IP APM device, or to multiple devices in a device group.

      A sync-only device group configured for automatic and full sync is required to synchronize access policies between multiple devices.

      .. Important:: USE WITH CAUTION.  This is an advanced feature and you should consult with your F5 Account team or Professional Services before implementing this configuration.

      .. Note:: In BIG-IP 13.1.0, a maximum of either BIG-IP APM systems are supported in a sync-only group type.

**Customization**

#. Click on **Access** --> **Profiles/Policies** --> **Customization**

      What are customization and localization?

      Customization and localization are ways to change the text and the language that users see, and to change the appearance of the user interface that Access Policy Manager presents to client users. Customization provides numerous settings that let you adapt the interface to your particular operation. Localization allows you to use different languages in different countries.

      About the Customization tool

      The Customization tool is part of Access Policy Manager (APM). With the Customization tool, you can personalize screen messages and prompts, change screen layouts, colors, and images, and customize error messages and other messages using specific languages and text for policies and profiles developed in APM. You can customize settings in the Basic Customization view (fewer settings) or change the view to General Customization (many settings). In the General Customization view, you can use the Customization tool in the BIG-IP admin console, or click Popout to open it in a separate browser window. In either view, you can click Preview to see what an object (such as Logon page or Deny Ending Page) will look like.

      After you personalize settings, remember to click the **Save** icon to apply your changes.

#. About basic, general, and advanced customization

      The Customization tool provides three views that you can use to customize the interface. The General Customization view provides the greatest number of options
      and is where most of the customization takes place.

      +----------------------+--------------------------------------------------------------------------------------------------------------------+
      | View                 | Description                                                                                                        |
      +======================+====================================================================================================================+
      | Quick Start/Basic    |Basic customization provides a limited set of options intended for quick modification of the objects that are       |
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

BIG-IP APM serves as an authentication gateway or proxy. As an authentication proxy, BIG-IP APM provides separate client-side and server-side authentication. Client-side authentication occurs between the client and BIG-IP APM. Server-side authentication occurs between BIG-IP APM and servers.

Loose coupling between the client-side and server-side layers allows for a rich set of identity transformation services. Combined with a Visual Policy Editor and an expansive set of access iRules functionality, BIG-IP APM provides flexible and dynamic identity and access, based on a variety of contexts and conditions.

For example, a client accessing Microsoft SharePoint through BIG-IP APM in a corporate environment may silently authenticate to BIG-IP APM with NT LAN Manager (NTLM) or Kerberos credentials. On leaving that environment, or on using a different non-sanctioned device, the client may be required to go through another potentially stronger authentication, such as a smart card or other client certificate, RSA SecurID, or one-time passcode. You can require additional device vetting such as file, folder, and registry checks and antivirus and firewall software validation.

A BIG-IP APM authentication and SSO features access and identity security posture can automatically change depending on environmental factors, such as who or where the user is, what resource the user is accessing, or when or with what method the user is attempting to gain access.

Data centers and Cloud deployments often face the challenge of offering multiple applications with different authentication requirements. You can deploy BIG-IP APM to consolidate and enforce all client-side authentication into a single process. BIG-IP APM can also perform identity transformation on the server side to authenticate to server services using the best-supported methods. This can reduce operational costs since applications remain in the most-supported and documented configurations. Common examples of identity transformation are client-side public key infrastructure (PKI) certificate to server-side Kerberos and client-side HTTP form to server-side HTTP Basic.

The following figure shows BIG-IP APM acting as an authentication gateway. Information received during pre-authentication is transformed to authenticate to multiple enterprise applications with different requirements.

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
#. Click on server1-ad-servers and review the settings.  You can choose to use go direct or use a pool of AD servers.

      +----------------------+-----------------------------+----------------------------------+
      |General Properties    | Name                        |  server1-ad-servers              |
      +----------------------+-----------------------------+----------------------------------+
      |Configuration         | Domain Name                 |  f5lab.local                     |
      +----------------------+-----------------------------+----------------------------------+
      |                      | Server Connection           |  Use Pool                        |
      +----------------------+-----------------------------+----------------------------------+
      |                      | Domain Controller Pool Name |  /Common/server1-ad-pool         |
      +----------------------+-----------------------------+----------------------------------+
      |                      | IP Address                  |  10.1.20.7                       |
      +----------------------+-----------------------------+----------------------------------+
      |                      | Hostname                    |  dc1.f5lab.local                 |
      +----------------------+-----------------------------+----------------------------------+
      |                      | Admin Name                  |  admin                           |
      +----------------------+-----------------------------+----------------------------------+
      |                      | Admin Password              |  admin                           |
      +----------------------+-----------------------------+----------------------------------+

      .. Note:: If you choose to use a pool you can create the pool as you create the AD object.  Go back and click create to see what this looks like.

      |adpool|

      You have now created an object that can be used to facilitate Active Directory authentication in front of any application.  The application itself does not need to require authentication. If you were to deploy a policy with AD Auth on a Virtual Server for a web application the policy would preset a login page, prompt for credentials, verify the credentials against this AD object before allowing a user to access the web application.

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

      |basicpolicy|

      Now you have a basic policy with AD Authentication that you can leverage for Web Pre-Authorization in front of any application.

#. Go to **Local Traffic** --> **Virtual Servers**
#. Locate server1-https and click on it
#. Scroll down to the Access Policy section.  Next to **Access Profile** click the drop and replace server1-psp with your Basic_policy
#. Scroll down to the bottom and click **Update**
#. In a new browser tab go to http://server1.acme.com and Login

Task 6: Single Sign-On
----------------------------
Client side and server side are loosely coupled in the authentication proxy. Because of this, BIG-IP APM can transform client-side identity values of one type can into server-side identity values of another type. You configure SSO within an SSO profile, which is applied to an access profile. The system triggers SSO at the end of successful access policy evaluation and on subsequent client-side requests.

BIG-IP APM supports industry standard authentication methods, including:

    - NTLM
    - Kerberos
    - HTTP Basic
    - HTTP Form
    - Security Assertion Markup Language (SAML)

    .. Note:: Client-side authentication methods outnumber server-side methods. This is because BIG-IP APM does not transmit client certificate, RSA SecurID, or one-time passcodes to the server on the client’s behalf.

#.  Go to **Access** --> **Single Sign-On** --> **HTTP Basic**
#.  Click **Create**

        +----------------------+-----------------------------+----------------------------------+
        |General Properties    | Name                        |  Basic_http_sso                  |
        +----------------------+-----------------------------+----------------------------------+
        |Credential Source     | Username Source             |  session.sso.token.last.username |
        +----------------------+-----------------------------+----------------------------------+
        |                      | Password Source             |  session.sso.token.last.password |                        |
        +----------------------+-----------------------------+----------------------------------+
        |SSO Method Conversion | Username Conversion         |  unchecked                       |
        +----------------------+-----------------------------+----------------------------------+

        .. Note::  Username conversion can be enabled if you want domain\username or username@domain to convert to just username.

#. Click **Finished**
#. Click on **Access** --> *Profiles/Policies** --> **Access Profiles (Per-Session Policies)**
#. Locate your server1-psp profile and click on the name
#. Click on **SSO/Auth Domains**
#. Under SSO Configuration click the drop down and select **Basic_http_sso** click update
#. From the top menu bar click **Access Policy** and click **Edit Access Policy for Profile "server1-psp"** link
#. Click the **+** between **AD Auth** and **Allow**
#. Click on **Assignment** and choose **SSO Credential Mapping** -->  **Add Item** -->  **Save**
#. Click **Apply Policy**
#. Open an incognito window and try go to https://server2.acme.com
#. You should have been prompted to login.  Close the Window
#. Go to **Local Traffic** --> **Virtual Servers** and open server2-https
#. Scroll to *Access Policy** and click the drop down next to **Access Profile**.  Choose server1-psp
#. Scroll down click **Update**
#. Open a new incognito tab.  Go to https://server2.acme.com
#. Login **user1** and **user1**
#. Now you should have been signed in to the backend server with Single Sign On.


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
.. |image25| image:: /class1/module1/media/lab01/image25.png
.. |adpool| image:: /class1/module1/media/lab01/adpool.png
.. |basicpolicy| image:: /class1/module1/media/lab01/basicpolicy.png
