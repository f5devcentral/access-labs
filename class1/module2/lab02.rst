Lab 2: Step up Authentication with Per-Request Policies
=====================================

Objectives
----------
In this lab we will explore adding authentication to your access policies. This authentication can come in many forms

Lab Requirements
----------------

-

Lab 2: APM Per Request Policies
==========================================

The purpose of this lab is to familiarize the Student with Per Request Policies.
The F5 Access Policy Manager (APM) provides two types of policies.

Access Policy - The access policy runs when a client initiates a session.   Depending
on the actions you include in the access policy, it can authenticate the user
and perform group or class queries to populate session variables with data for
use throughout the session.

Per-Request Policy - After a session starts, a per-request policy runs each time
the client makes an HTTP or HTTPS request.  A per-request policy can include a
subroutine, which starts a sub-session.  Multiple sub-sessions can exist at one
time. One access policy and one per-request are specified within a virtual server.

**It's important to note that APM first executes a per-session policy when a client
attempts to connect to a resource.   After the session starts then a per-request
policy runs on each HTTP/HTTPS request.  Per-Request policies can be utilized in a
number of different scenarios; however, in the interest of time this lab will only
demonstrate one method of leveraging Per-Request policies**

This lab will only focus on configuring Per-Request policies for controlling access
to external URL categories.


Objective:
----------

-  Gain an understanding of Per Request policies

-  Gain an understanding of use for Per Request Policy


Lab Requirements:
-----------------

-  All lab requirements will be noted in the tasks that follow

Estimated completion time: 15 minutes

Lab 3 Tasks:
-----------------

TASK 1: Create Per Session Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Refer to the instructions and screen shots below:

+----------------------------------------------------------------------------------------------+
| 1. Login to your lab provided **Virtual Edition BIG-IP**                                     |
|     - On your jumphost launch Chrome and click the bigip1 link from the app shortcut menu    |
|     - Login with credentials admin/admin                                                     |
|                                                                                              |
| 2. Begin by selecting: **Access -> Profiles/Policies -> Per Session Policies** ->            |
|                                                                                              |
| 3. Click the **Create** button (far right)                                                   |
+----------------------------------------------------------------------------------------------+
| |Lab2-Image1|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. Enter the name of the policy, profile type, and profile scope                             |
|                                                                                              |
|    -  **Name**: **app.acme.com-PSP**                                                         |
|                                                                                              |
|    -  **Profile Type**: **All**                                                              |
|                                                                                              |
|    -  **Profile Scope**: **Profile**                                                         |
|                                                                                              |
|    -  **Accept Languages**: **English (en)**                                                 |
|                                                                                              |
| *Note: You will need a per session policy and a per request policy but we will be*           |
|        *leaving the per session policy blank and performing our auth in per Request*         |
+----------------------------------------------------------------------------------------------+
| |Lab2-Image2|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 5. On the app.acme.com-PSP policy click **Edit**                                             |
|                                                                                              |
| 6. Click on the **Deny** and change the Select Ending to **Allow**                           |
|                                                                                              |
| 7. Click **Save**                                                                            |
|                                                                                              |
| 8. Click Apply policy                                                                        |
|                                                                                              |
|   *Note:  Nothing will be set in this policy we will simply establish a session and manage*  |
|           *all the authentication in the Per-Request Policy*                                 |
+----------------------------------------------------------------------------------------------+
| |Lab2-Image3|                                                                                   |
|                                                                                              |
| |Lab2-Image4|                                                                                   |
+----------------------------------------------------------------------------------------------+

Task 2: Radius Authentication
--------------------------------------
Access Policy Manager supports authenticating and authorizing the client against external RADIUS servers. When a client connects with the user name and password, Access Policy Manager authenticates against the external server on behalf of the client, and authorizes the client to access resources if the credentials are valid.

How RADIUS works How RADIUS works
The client requests access to network resources through Access Policy Manager.
Access Policy Manager then issues a RADIUS Access Request message to the RADIUS server, requesting authorization to grant access.
The RADIUS server then processes the request, and issues one of three responses to Access Policy Manager: Access Accept, Access Challenge, or Access Reject.

Task 3: Kerberos Authentication
--------------------------------------------------
Access Policy Manager (APM) provides an alternative to a form-based login authentication method. This alternative method uses a browser login box that is triggered by an HTTP 401 response to collect credentials. A SPNEGO/Kerberos or basic authentication challenge can generate a HTTP 401 response.
This option is useful when a user is already logged in to the local domain and you want to avoid submitting an APM HTTP form for collecting user credentials. The browser automatically submits credentials to the server and bypasses the login box to collect the credentials again.
Because SPNEGO/Kerberos is a request-based authentication feature, the authentication process is different from other authentication methods, which run at session creation time. SPNEGO/Kerberos authentication can occur at any time during the session.

The benefits of this feature include:
Provides flexible login mechanism instead of restricting you to use only the form-based login method.
Eliminates the need for domain users to explicitly type login information again to log in to Access Policy Manager.
Eliminates the need for user password transmission with Kerberos method.

Task 3: Intro to Posture Assessments
-------------------------------------
A device posture check can be used to continuously check the state of a macOS or Windows client. This feature provides asynchronous desktop client posture checking.
Using F5 Access Guard for Mac and Windows, administrators can now include the ability to transmit up-to-date device posture information to Access Policy Manager in a cryptographically signed HTTP header.
With a device posture check, you can check several categories of items on a client machine.

-Antivirus
-Endpoint State
-Firewall
-Hard Disk Encryption
-Patch Management
-Public File Sharing
-System Health Agent

You can add these items in a per-request policy using subroutines only. You can configure any subroutine to be checked against the client either periodically, or on every request.
Continuous client checks in a subroutine are supported only on macOS and Windows. Continuous client checks require that the F5 Access Guard service and browser extension be installed, and that the administrator configures the F5 Access Guard configuration file to specify the items to be checked. Refer to the F5 Access Guard Configuration documentation for more information.


Task 4: Example Use Cases
----------------------------



Task 4: MTLS
---------------



Task 5: SAML
----------------------------


Lab 2 is now complete.

.. |Lab1-Image1| image:: /class1/module2/media/Lab2-Image1.png
.. |Lab1-Image2| image:: /class1/module2/media/Lab2-Image2.png
.. |Lab1-Image3| image:: /class1/module2/media/Lab2-Image3.png
.. |Lab1-Image4| image:: /class1/module2/media/Lab2-Image4.png
.. |Lab1-Image5| image:: /class1/module2/media/Lab2-Image5.png
.. |Lab1-Image6| image:: /class1/module2/media/Lab2-Image6.png
