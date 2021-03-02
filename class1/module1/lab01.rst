Lab 1: Provisioning & Main Menu Navigation
===========================================

Objectives
----------

The intention of this lab will be to show how to enable Access Policy Manager (APM) through resource provisioning.  Next we will explore all the components within the **Access** left menu.
This is not a deep dive on the components but an overview of the components/features of APM.

Lab Requirements
----------------

-  A pre existing virtual server at 10.1.10.101 or https://server1.acme.com

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

|image1|

#. Before you click on Submit note that this operation will halt operations while the module provisions.  Do not do this on an active unit processing traffic unless you are in an outage window. This
will not require a reboot but will take approximately 1 to 5 minutes to complete.

|image2|
|image3|

.. Note::  Resource Provisioning is not a synced item between HA pairs.  You will need to provision the module on all devices in the cluster.

Task 2: Guided Configuration
-----------------------------
Access Guided Configuration (AGC) provides an easy way to create BIG-IP configurations for categories of Access use cases. This feature is written in has an independent release from TMOS and requires
updates for new configurations from time to time. To find updates and expanded use cases it will be necessary to download and install updates from https://downloads.f5.com. In this task we are
going to explore the menu and take a look at a few options. We will not be deploying any of these solutions in this lab. Lab 3 will dive a little deeper in to the use cases and when to use AGC.

#.  Go to **Access** --> **Guided Configuration**
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
#.  Zero Trust is the next tile. Zero trust follows the principle never trust, always verify and thus enforces authentication and verification for every user or device attempting to access resources whether from within or
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

+---------------+-------------+-------------+
|Single Proxy   | |image13|   |  |image17|  |
+---------------+-------------+-------------+
|Multi-Proxy    | |image14|   |  |image16|  |
+---------------+-------------+-------------+

#.  Proceeding with this configuration will create a number of object as seen here.

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
in more detail later).

- Can you find the first **Following Rule** log message?
- Where did it flow?
- Was the user successful?

#.  Return to the first screen by using the back button in the browser
#.  In **Active Sessions** click on the check box next to the session and select the **Kill Selected Sessions** button.  This will terminate the users session and make them login again.
#.  Click on **Access Reports**
#.  You will be prompted to enter a time period to run the report

|image22|

.. Note:: This is how you can view past sessions.  Pick a time frame and run a report.

#.  There are two other reporting functions in this screen, **OAuth Report** and **SWG Reports** which will be covered in more detail in later labs
#.  The last section is Event Logs.

.. Note:: URL Request Logs is part of SWG functionality and will be covered later

#.  Click on **Event Logs** and choose **Settings**
#.  This is where you can create logging profiles for access policies.  From here you can specify what information to collect and to what detail.
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
|Access Profile        | Selected                  |  Blah                            |
+----------------------+---------------------------+----------------------------------+

.. Note:: Within the Access System Logs section of the log profile is where you can change the logging for various portions of the APM Policies.  The one you will use most will be to move Access Policy
from Notice to Debug and/or Pre-Request Policy from Notice to Debug.  As you can see you can pick and choose what level of notifications you want in your logs.  This will impact what you see in
Access Reports for a session and what appears in /var/log/apm.

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

The per-session policy runs when a client initiates a session. (A per-session policy is also known as an access policy.) Depending on the actions you include in the access policy, it can authenticate
the user and perform other actions that populate session variables with data for use throughout the session.

#.  Click on the Create button on the far right

+----------------------+---------------------------+----------------------------------+
|General Properties    | Name                      |  Basic_policy                    |
+----------------------+---------------------------+----------------------------------+
|                      | Profile Type              |  All                             |
+----------------------+---------------------------+----------------------------------+
|                      | Profile Scope             |  Profile                         |
+----------------------+---------------------------+----------------------------------+
|Language Settings     | Accepted Languages        |  English                         |
+----------------------+---------------------------+----------------------------------+

#.  Now we have a basic profile.  There were a number of other settings to modify and use in the profile.  For now we will focus just on the basics.
#.  From the **Access Profiles (Per-Session Policies)** section locate the **Basic_policy**
#.  There are two ways to edit the Policy piece of the profile.
    First way

    +----------------------------------------------------------------------------+
    | Click on the profile                                                       |
    +----------------------------------------------------------------------------+
    | Click on **Access Policy**                                                 |
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

#.  Close the VPE (we will visit the VPE and policy in more detail later)  Click on the **Basic_policy** and explore the settings for the Profile.

    +----------------------+------------------------------------------------------------------------------------+
    | Settings             | Here you can manage settings for the profile. You may want to change timeouts, max |
    |                      | sessions and login attempts. These are settings specifically for this profile.     |
    +----------------------+------------------------------------------------------------------------------------+
    | Configurations       | For various use cases this section may need configuration.                         |
    +----------------------+------------------------------------------------------------------------------------+
    | Language Settings    | You set these at creation.                                                         |
    +----------------------+------------------------------------------------------------------------------------+

.. Note:: If you are unsure of the settings you need at profile creation you can see that you can return to the profile and make adjustments.

#.  Still in the profile click on **SSO/Auth Domain** at the top

BIG-IP APM offers a number of Single Sign On (SSO) options.  The SSO/Auth Domain tab in a Per Session Profile is where you will select what SSO method to use for your application.
In Task 6 we will cover the objects that need to be created in order to associate that SSO method to a policy.  At this time the drop down for the SSO Configuration will be
blank.

#.  What is Domain Mode?

Access Policy Manager (APM) provides a method to enable users to use a single login or session across multiple virtual servers in separate
domains. Users can access back-end applications through multiple domains or through multiple hosts within a single domain, eliminating additional
credential requests when they go through those multiple domains. With multi-domain support, you have the option of applying different SSO methods
across different domains.

.. Note:: When thinking Domain do not confuse this with Active Directory domain.  In this context domain refers to the DNS domain.  Example, app1.f5demo.com and app2.f5dmeo.com
are in the f5demo.com DNS domain.

.. Important:: To enable multi-domain support, all virtual servers must be on a single BIG-IP system and share the same access profile. All virtual
servers must include all of the profiles that the access profile requires (for example, VDI, rewrite, server SSL, connectivity, and so on).

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

By default, BIG-IP APM requires authentication for each access profile.  This can easily be changed by adding the domain cookie. For this section you will add
the domain for your application. For example, if you have two applications app1.f5demo.com and app2.f5demo.com you would enter the domain f5demo.com for your
domain cookie. Now your users can access each application and will only be prompted for authentication once.

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

This drop down is where you will find all the SSO objects that you have configured on this BIG-IP appliance. If you want to enable an SSO method for an application
first you must configuration the SSO object and then select in this section of the policy.

.. Note:: Task 6 will review SSO methods and configuration.

#.  Multiple domains

If you return to the radio buttons and select Multiple Domains new options will appear.  When this configuration is complete a user will be able to connect to any of
the virtual servers and authentication will only be requested once.  Subsequent connections in the domain group should not prompt for additional login.

- Primary Authentication URI:  Specifies the address of your primary authentication URI. An example would be https://login.acme.com. This is where the user session
  is created. As long as you provide the URI, your users are able to access multiple backend applications from multiple domains and hosts without requiring them to
  re-enter their credentials because the user session is stored on the primary domain. This is a required field if you selected Multiple Domains domain mode.
- Authentication Domain Configuration: Set the domain acme.com
- Authentication Domains:  To add the applications click on **Add** at the far right and enter the host. Example, app1.acme.com, app1.acme.com  If you have and SSO
  method created select the SSO method from the drop down box.  This can be edited later to add an SSO method.

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

Server-side authentication involves BIG-IP APM providing authentication to a server resource. This is called SSO.

.. Note:: Single Sign On (SSO) will be covered in Task 6.

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
.. |image18| image:: /class1/media/image18.png
.. |image19| image:: /class1/media/image19.png
.. |image20| image:: /class1/media/image20.png
.. |image21| image:: /class1/media/image21.png
.. |image22| image:: /class1/media/image22.png
.. |image23| image:: /class1/media/image23.png
.. |image25| image:: /class1/media/image25.png
