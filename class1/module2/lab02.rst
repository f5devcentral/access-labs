Lab 2: Client-Side Authentication
=====================================

Objectives
----------
In this lab we will explore adding authentication to your access policies. This authentication can come in many forms

Lab Requirements
----------------

-

Task 2: Intro to Per-Request Policy
--------------------------------------
The purpose of this lab is to familiarize the Student with Per Request Policies. The F5 Access Policy Manager (APM) provides two types of policies.

Access Policy - The access policy runs when a client initiates a session. Depending on the actions you include in the access policy, it can authenticate the user and perform group or class queries to populate session variables with data for use throughout the session.

Per-Request Policy - After a session starts, a per-request policy runs each time the client makes an HTTP or HTTPS request. A per-request policy can include a subroutine, which starts a subsession. Multiple subsessions can exist at one time. One access policy and one per-request are specified within a virtual server.

It’s important to note that APM first executes a per-session policy when a client attempts to connect to a resource. After the session starts then a per-request policy runs on each HTTP/HTTPS request. Per-Request policies can be utilized in a number of different scenarios; however, in the interest of time this lab will only demonstrate one method of leveraging Per-Request policies



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
