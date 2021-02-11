Lab 1: Implement C3D with APM Enhancements
===============================================

As organizations move towards MFA to secure their enterprise applications, they often struggle when implementing Single Sign-On (SSO). Implementation of MFA at the proxy layer, while allowing for Single-Sign On, often requires usage of a less secure authentication method to the backend resource due to the introduction of service accounts requiring passwords. However, if an organization choses to implement MFA directly at the application, SSO is lost.

The F5 Client Certificate Constrained Delegation (C3D) feature allows the best of both worlds by allowing MFA at the proxy layer while maintaining strong security when performing SSO between the proxy and backend resource.

The Ephemeral Authentication lab is a combination of multiple features included in Access Policy Manager to enhance security for Authentication schemes. The first module will cover the implementation of **Client Certificate Constrained Delegation (C3D)** features enhanced in APM. This use case is often referred to as CertSSO.  The second module covers the **Privileged User Access** solution with a specific focus on ephemeral authentication for SSH access to network devices, as well integration with code respositories.

This class covers the following topics related to Ephemeral Authentication:

- LDAP Ephemeral Authentication
- RADIUS Ephemeral Authentication
- HTML5 SSH
- C3D APM Enhancements

Expected time to complete: **1 hour**


Setup Lab Environment
----------------------------------------

**NEED TO REWRITE**





Section 1.1 - Create Authentication objects
---------------------------------------

The first step in deploying CertSSO is creating the objects required for the user to authenticate to APM.  In this lab, the user will authenticate via Active Directory and simulated MFA via RADIUS.  The user's authentication method to APM is independent of how the BIG-IP authenticates the user to the backend server for Single-Sign-On.  This allows an organization to choose an authentication scheme that matches their needs such as SAML, OAuth, or other method.

Task 1 - Create an Active Directory AAA Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the web browser, click on the **Access** tab located on the left side.

   |image0|

#. Navigate to **Authentication >> Active Directory**, then click the **+** (plus symbol) to create a new AAA object

   |image1|

#. Enter the following information for the AD Authentication Object

   - Name: **ad_servers**
   - Domain Name: **f5lab.local**
   - Domain Controller Pool Name: **ad_pool**
   - Domain Controller IP address: **10.1.20.7**
   - Domain Controller Hostname: **dc.f5lab.local**
   - Admin name: **admin**
   - Admin Password: **admin**

   |image2|

#. Click **Finished**

Task 2 - Create a RADIUS AAA Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the web browser, click on the **Access** tab located on the lefthand side.

#. Navigate to **Authentication >> RADIUS**, then click the **+** (plus symbol) to create a new AAA object

   |image3|

#. Enter the following information for the Radius Authentication Object

   - Name: **radius_servers**
   - Server Pool Name: **radius_pool**
   - Server Addresses: **10.1.20.8**
   - Secret password: **secret**

   |image4|

#. Click **Finished**

Section 1.2 - Create an Access profile
-----------------------------------

In this section, you will create and define the settings of the APM Access Profile.

Task 1 - Create the cert_sso Access Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#. From the web browser, click on the **Access** tab located on the left side.

#. Navigate to **Profile/ Policies >> Access Profile(Per-Session Policies)**, then click the **+** (plus symbol) to create a new Access Profile

   |image5|

#. Enter the Name **cert_sso** 
#. Select the profile Type **All** from the dropdown

   |image6|

#. Scroll to the bottom of the profile settings to set the default language to **English**

#. Click **Finished**

   |image7|
   
   
Section 1.3 - Create the Access Policy
------------------------------------

In this section, edit the policy using the Visual Policy Editor to enable users to login via AD+MFA, then transition to CertSSO.

Task 1 - Open Visual Policy Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. On the cert_sso profile line click **edit** under Per-Session Policy

   |image8|

#. Click the **+** (plus symbol) located on the fallback branch located between the **Start** and **Deny** boxes

   |image9|

#. Click the **Logon** Tab
#. Select **Logon Page**  
#. Click **Add Item**

   |image11|

#. Add an additional field to the logon page by selecting **password** from the **Type** dropdown (line 3)
#. Enter **OTP** for **Post Variable Name**
#. Enter **OTP** for **Session Variable Name**
#. Enter **OTP** for **Logon Page Input Field #3**
#. Click **Save**

   |image12|

#. Click the **+** (plus symbol) located on the fallback branch located between the **Logon Page** and **Deny** boxes

   |image13|

#. Click the **Authentication** tab
#. Select **RADIUS Auth**  
#. Click **Add Item**

   |image14|

#. Select **radius_servers** from the **AAA Server** dropdown box
#. Change the password source to **%{session.logon.last.OTP}**
#. Click **Save**

   |image15|

#. Click the **+** (plus symbol) located on the **Successful** branch located between **RADIUS Auth** and **Deny** boxes


   |image16|

#. In the **Authentication** tab, select **AD Auth** 
#. Click **Add Item**

   |image17|


#. Select **ad_servers** from the Server dropdown box
#. Click **Save**

   |image18|

#. Click the **+** (plus symbol) located on the **Successful** branch located between **AD Auth** and **Deny** box
#. Click **Add Item**

   |image10|

#. In the **Assignment** tab, select **Variable Assign** 
#. Click **Add Item**

   |image19|

#. Click **Add new entry**

   |image36|

#. Click **change**

   |image37|

#. Enter **session.ssl.cert.whole** in the custom variable field

   |image38|

#. Locate the **F5CertSSO.f5lab.local.txt** file in the **C:\\labs\\class2\\student_files** directory. 

   |image39|

#. Open the file with **notepad++** and copy the contents of the file

   |image40|

#. Return to the **Visual Policy Editor** and paste the certificate into the **custom expression** field
#. Click **Finished**

   |image41|

#. Click **Save**

   |image42|

#. Click the **Deny** ending icon located on the fallback branch of the **Variable Assign** agent

   |image20|

#. Click **Allow**
#. Click **Save**

   |image21|

#. Click **Apply Access Policy** located in the top left corner to commit the policy changes


Section 1.4. - Create the SSL Profiles
----------------------------------------

In this section, you will define the virtual server IP address and its SSL profile settings.

Task 1 - Create a Client SSL Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Local Traffic >> Profiles >> SSL >> Client**, then click the **+** (plus symbol) to create a new **SSL Profile**

   |image23|

#. Enter the name **client_certsso**
#. **Check** the **custom** box to the right of **Certificate Key Chain**
#. Click **add**

   |image24|

#. Select **acme.com-wildcard.crt** from the **certificate** dropdown box
#. Select **acme.com-wildcard.key** from the **key** dropdown box
#. Click **Add**

   |image25|

#. **Check** the **custom** box to the right of **Client Certificate Constrained Delegation**
#. Select **Enabled** from the **Client Certificate Constrained Delegation** dropdown box
#. Click **Finished**

   |image26|


#. Click **Finished**

Task 2 - Create a Server SSL Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Local Traffic >> Profiles >> SSL >> Server**, then click the **+** (plus symbol) to create a new SSL Profile

   |image27|

#. Enter **server_certsso** for profile name
#. **Check** the two custom boxes next to **Certificate** and **Key**
#. Select **F5CertSSO.f5lab.local.crt** from the **certificate** dropbox box
#. Select **F5CertSSO.f5lab.local.key** from the **key** dropdown box

   |image28|

#. Check the **custom** box about the **Client Certificate Constrained Delegation** box
#. Select **Enabled** from the **Client Certificate Constrained Delegation** dropdown box
#. Select **F5SubCA.f5lab.local.crt** from the **CA Certificate** dropdown box
#. Select **F5SubCA.f5lab.local.key** from the **CA Key dropdown** box
#. **Click** Finished

   |image29|
   
   
Section 1.5 - Create a Pool
-------------------------------

In this section you create a pool that contains the IP address of the CentOS server hosting the website requiring mTLS.

Task 1 - Create the Pool
~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Local Traffic >> Pools >> Pool List**, then click the **+** (plus symbol) to create a new **Pool**

   |image30|


#. Enter **mtls_pool** for the **Pool Name**
#. Select **https** from the list of available monitors
#. Enter **10.1.20.9** for the member address
#. Enter **443** for the member port
#. Click **add**
#. Click **Finished**

   |image31|
   
   
Section 1.6 - Create the Virtual Server
------------------------------------------------

In this section you will configure a RADIUS server to enable simulated MFA capabilities.


Task 1 - Configure Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#. Navigate to **Local Traffic >> Virtual Servers >> Virtual Server List**, then click the **+** (plus symbol) to create a new virtual Server

   |image32|

#. Enter **mtls_vs** for the **Name**
#. Enter **10.1.10.105** for the **DestinationAddress/Mask**
#. Enter **443** for the **Service Port**
#. Select **http** for **HTTP Profile (Client)**
#. Select **client_certsso** from the **SSL Profile (Client)** List

   |image33|


#. Select **server_certsso** from the **SSL Profile (Server)** List
#. Select **Auto Map** from the **Source Address Translation** dropdown Box
#. Select **cert_sso** from the **Access Profile** dropdown Box

   |image34|

#. Select the irule **Cert_SSO**
#. Select **mtls_pool** for the **Default Pool**
#. Click **Finished**


.. note::

   The following iRule must be used when inserting custom extensions using C3D.

.. code-block:: none
   :linenos:

   when SERVERSSL_CLIENTHELLO_SEND {
      set username [ACCESS::session data get "session.logon.last.username"]
      set domain [ACCESS::session data get "session.ad.last.actualdomain"]
      SSL::c3d extension 1.1.1.1 "Minted Extension=$username@$domain"
   }

|image35|


Section 1.7 - Test CertSSO
------------------------------------------------

In this section, you will test access to an NGINX website requiring mTLS.


Task 1 - Access mtls.acme.com with static certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the jumpbox's web browser, access https://mtls.acme.com

#. Use the following credentials:
    - Username **user1** 
    - Password: **user1**
    - OTP: **123456**

   |image44|

#. You will be logged into the site as **User1**.

   .. note::

      The contents of the certificate used for logging into the website was the CertSSO certificate copied into Per-Session Policy. The iRule that was attached inserted the custom extension 1.1.1.1 with the value of the user's logon name.  Notice that the Subject Name is CertSSO, the Subject Alternative Name is empty, and the custom extension is user1@f5lab.local.
   
       - Cert Subject: **f5certsso**
       - Subject Alt: **<empty>**
       - Custom Ext: **user1@f5lab.local**

   |image45|

#. Open a new incognito browser window so you can test access to https://mtls.acme.com with different user credentials.

   |image48|

#. Use the following credentials:
    - Username **user2** 
    - Password: **user2**
    - OTP: **123456** 

   |image50|

#. You will be logged into the site as **user2@f5lab.local**

   .. note::

      Notice that user2's Cert Subject is the same as in User1, but the custom extension name is different (now user2@f5lab.local).
   
        - Cert Subject: **f5certsso**
        - Subject Alt: **<empty>**
        - Custom Ext: **user2@f5lab.local**

   |image51|
   
   
Section 1.8 - Implement Dynamic Certificate Injection
--------------------------------------------------------

In this section, we will use the HTTP Connector to retrieve a user's certificate from Active Directory and use it in the BIG-IP Certificate minting process.


Task 1 - Create an HTTP Connector Transport
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Access >> Authentication >> HTTP Connector >> HTTP Connector Transport** and click the  **+** (plus symbol)

   |image54|

#. Enter Name **demo-http-connector**

#. Select **internal-dns-resolver** from the **DNS Resolver** dropdown

#. Select **apiadmin-serverssl** from the **Server SSL Profile**

#. Click **Save**

   |image55|

Task 2 - Create a HTTP Connector Request
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Access >> Authentication >> HTTP Connector >> HTTP Connector Request** and click the  **+** (plus symbol)

   |image56|

#. Enter name **get-cert**
#. Select **demo-http-connector** from the dropdown
#. Enter URL **https://adapi.f5lab.local:8443/aduser/cert?useridentity=%{perflow.username}**
#. Enter **GET** for the **Method**
#. Select **Parse** for the **Response Action**
#. Click **Save**

   |image57|


Task 3 - Create a Per-Request Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to **Access >> Profiles/Policies >> Per-Request Policies** and click the  **+** (plus symbol)

   |image58|

#. Enter the name **certsso_prp**
#. Select the Language **English**
#. Click **Finished**

   |image59|

#. Click **edit** under **Per-Request Policy**

   |image60|

#. Click **Add New Subroutine**

   |image61|

#. Enter the name **Request Cert**
#. Click **Save**

   |image62|

#. Expand the subroutine by click the **+** (plus symbol)

   |image63|

#. Click the **+** (plus symbol) on the fallback branch.

   |image64|

#. Click the **General Purpose** tab
#. Select **HTTP Connector**
#. Click **Add Item**

   |image65|

#. Select **get-cert** drop the dropdown

   |image66|

#. Click **Edit Terminals**

   |image67|

#. Click **Add Terminal**

   |image68|

#. Change the name for the default branch to **Fail**
#. Change the default branch text to **Red**
#. Enter the name **Success** for the new branch
#. Change the color of the new branch to **Green**

   |image69|

#. Click the **Fail** terminal at the end of the **Successful** branch

   |image70|

#. Select the **Success** terminal
#. Click **Save**

   |image71|

#. Click the **+** (plus symbol) on the **successful** branch

   |image72|

#. Click the **Assignment** tab
#. Select **Variable Assign**
#. Click **Add Item**

   |image73|

#. Click **Add new entry**
#. Click **change**

   |image74|

#. Enter **session.ssl.cert.whole** for the **Custom Variable**
#. Select **Session Variable** from the dropdown
#. Enter **subsession.http_connector.body.certificate** for the **Session Variable**
#. Click **Finished**

   |image75|

#. Click **Save**

   |image76|

#. Click the **+** (plus symbol) located between **Start** and **Allow** in the policy

   |image77|

#. Click the **Subroutines** tab
#. Select the **Request Cert** subroutine
#. Click **Add Item**

   |image78|

#. Click the **+** (plus symbol) on the success branch of **Request Cert**

   |image79|

#. Click the **General Purpose** tab
#. Select **irule Event**
#. Click **Add Item**


.. note::

   This iRule event triggers the code from the previously attached iRule. This iRule must be used when inserting a certificate using C3D in a per-request policy.

.. code-block:: none
   :linenos:

   when ACCESS_PER_REQUEST_AGENT_EVENT {
      set cert [ACCESS::session data get {session.ssl.cert.whole}]
      log local0. "My cert: $cert"
      SSL::c3d cert [X509::pem2der $cert]
   }


|image80|

43. Enter **lab** for the **ID**
44. Click **Save**

|image81|

Task 4 - Attach the PRP to the mTLS Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Navigate to **Local Traffic >> Virtual Servers**.  Click **Virtual Server List**

|image82|

2. Click **mtls_vs**

|image83|

3. Navigate to the **Access Policy** section and select **certsso_prp** from the **Per-Request Policy** dropdown
4. Click **Update**


|image84|


Section 1.9 - Test Dynamic Certificate Injection
------------------------------------------------

In this section, you will learn how the HTTP Connector can used to retrieve dynamic content for use in C3D.


Task 1 - Access mtls.acme.com with Dynamic Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the web browser on the jumphost, access https://mtls.acme.com



#. Use the following credentials:
   - Username: **user1**
   - password: **user1**
   - OTP: **123456**

   |image44|

3. You will be logged into the site as **user1@f5lab.local**


   .. note::
   	The contents of the certificate used for logging into the website were from certificate retrieved via HTTP connector in Active Directory. The irule continues to insert the 	custom extension 1.1.1.1 with the value containing the user's logon name. Notice the Subject Name is user1, the Subject Alternative Name is user1@f5lab.local and the custom 	extension is user1@f5lab.local
   
      - Cert Subject: **user1**
      - Subject Alt: **user1@f5lab.local**
      - Custom Ext: **user1@f5lab.local**


   |image85|

4. Open a new incognito browser window so you can test access to mtls.acme.com with different user credentials.

   |image48|

5. Use the following credentials: 

   - Username: **user1**
   - password: **user1**
   - OTP: **123456**

   |image50|

6. You will be logged into the site as **user2@f5lab.local**

   .. note::
     Notice that user2's Cert Subject is now user2 and the subject alt is user2@f5lab.local.  The irule continues to insert the custom extension.
   
      - Subject: **user2**
      - Subject Alt: **user2@f5lab.local**
      - Custom Ext: **user2@f5lab.local**

   |image86|



.. |image0| image:: media/lab01/image000.png
	:width: 800px
.. |image1| image:: media/lab01/image001.png
.. |image2| image:: media/lab01/image002.png
	:width: 800px
.. |image3| image:: media/lab01/image003.png
.. |image4| image:: media/lab01/image004.png
	:width: 700px
.. |image5| image:: media/lab01/image005.png
.. |image6| image:: media/lab01/image006.png
	:width: 800px
.. |image7| image:: media/lab01/image007.png
.. |image8| image:: media/lab01/image008.png
.. |image9| image:: media/lab01/image009.png
.. |image10| image:: media/lab01/image010.png
.. |image11| image:: media/lab01/image011.png
.. |image12| image:: media/lab01/image012.png
.. |image13| image:: media/lab01/image013.png
.. |image14| image:: media/lab01/image014.png
.. |image15| image:: media/lab01/image015.png
	:width: 800px
.. |image16| image:: media/lab01/image016.png
.. |image17| image:: media/lab01/image017.png
.. |image18| image:: media/lab01/image018.png
	:width: 800px
.. |image19| image:: media/lab01/image019.png
.. |image20| image:: media/lab01/image020.png
.. |image21| image:: media/lab01/image021.png
.. |image22| image:: media/lab01/image022.png
.. |image23| image:: media/lab01/image023.png
.. |image24| image:: media/lab01/image024.png
	:width: 800px
.. |image25| image:: media/lab01/image025.png
.. |image26| image:: media/lab01/image026.png
	:width: 800px
.. |image27| image:: media/lab01/image027.png
.. |image28| image:: media/lab01/image028.png
	:width: 1000px
.. |image29| image:: media/lab01/image029.png
	:width: 1000px
	.. |image30| image:: media/lab01/image030.png
.. |image31| image:: media/lab01/image031.png
	:width: 800px
.. |image32| image:: media/lab01/image032.png
.. |image33| image:: media/lab01/image033.png
	:width: 800px
.. |image34| image:: media/lab01/image034.png
	:width: 800px
.. |image35| image:: media/lab01/image035.png
	:width: 800px
.. |image36| image:: media/lab01/image036.png
.. |image37| image:: media/lab01/image037.png
.. |image38| image:: media/lab01/image038.png
.. |image39| image:: media/lab01/image039.png
.. |image40| image:: media/lab01/image040.png
.. |image41| image:: media/lab01/image041.png
.. |image42| image:: media/lab01/image042.png
.. |image43| image:: media/lab01/image043.png
.. |image44| image:: media/lab01/image044.png
	:width: 800px
.. |image45| image:: media/lab01/image045.png
.. |image48| image:: media/lab01/image048.png
.. |image49| image:: media/lab01/image049.png
.. |image50| image:: media/lab01/image050.png
	:width: 800px
.. |image51| image:: media/lab01/image051.png
.. |image54| image:: media/lab01/image054.png
	:width: 800px
.. |image55| image:: media/lab01/image055.png
.. |image56| image:: media/lab01/image056.png
.. |image57| image:: media/lab01/image057.png
.. |image58| image:: media/lab01/image058.png
.. |image59| image:: media/lab01/image059.png
	:width: 800px
.. |image60| image:: media/lab01/image060.png
	:width: 1000px
.. |image61| image:: media/lab01/image061.png
.. |image62| image:: media/lab01/image062.png
.. |image63| image:: media/lab01/image063.png
.. |image64| image:: media/lab01/image064.png
.. |image65| image:: media/lab01/image065.png
.. |image66| image:: media/lab01/image066.png
.. |image67| image:: media/lab01/image067.png
.. |image68| image:: media/lab01/image068.png
.. |image69| image:: media/lab01/image069.png
.. |image70| image:: media/lab01/image070.png
.. |image71| image:: media/lab01/image071.png
.. |image72| image:: media/lab01/image072.png
.. |image73| image:: media/lab01/image073.png
.. |image74| image:: media/lab01/image074.png
.. |image75| image:: media/lab01/image075.png
.. |image76| image:: media/lab01/image076.png
.. |image77| image:: media/lab01/image077.png
.. |image78| image:: media/lab01/image078.png
.. |image79| image:: media/lab01/image079.png
.. |image80| image:: media/lab01/image080.png
.. |image81| image:: media/lab01/image081.png
.. |image82| image:: media/lab01/image082.png
.. |image83| image:: media/lab01/image083.png
.. |image84| image:: media/lab01/image084.png
.. |image85| image:: media/lab01/image085.png
.. |image86| image:: media/lab01/image086.png





