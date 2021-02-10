Lab 2: Client-Side Authentication
=====================================

Objectives
----------
In this lab we will explore adding authentication to your access policies. This authentication can come in many forms

Lab Requirements
----------------

-

Task 1: Active Directory Authentication
-----------------------------------------
The lab has a pre-configured test Virtual Server which will be used throughout the lab.  You will the Visual Policy Editor (VPE)
to create and attach a simple Access Profile which performs user authentication.

You can authenticate using Active Directory authentication with Access Policy Manager. We support using Kerberos-based authentication through Active Directory.


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

Task 4: MTLS
---------------



Task 5: SAML
----------------------------


Lab 2 is now complete.
