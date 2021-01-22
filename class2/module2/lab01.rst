Lab1: Configure Identity Aware Proxy(16.0)
===========================================

The 15.1 Zero Trust Architecture shifts many of the objects that would exist in a per-session policy to the per-request policy thereby creating a more secure authentication and authorization scheme. The authenticity of each request is further enhanced through the use of F5’s Access Guard agent installed on a client.  This agent provides a PKI signed report of the posture assessment performed on the client real-time rather than the historical way plug-ins reported status. Previously, after a user connected to an application they would experience a delay in access as the agent performed the posture assessment to provide an unsigned report to the BIG-IP. 

Topics Covered
----------------
- Real-time Posture Assessments
- Per-Request Frameworks
- Contextual Access
- HTTP Connector

Expected time to complete: **1 hour**

UDF blueprint version: **44**

Setup Lab Environment
----------------------------------------

#. Click the **Command Prompt** shortcut to open the command prompt on the jumphost 

   |image42|

#. Type the command **cd C:\\labs\\class3\\postman** to navigate the Postman collection folder.


#. Type the command **setup.bat**


#. All Steps in the collection should succeed before moving on to the lab.  If an API call fails run the collection again by repeating the previous step.  

   |image43|



Lab 1.1 - Access Guided Configuration
----------------------------------------

The first step in deploying the IAP is accessing Guided Configuration

Task - Access the Zero Trust IAP guided configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the webbrowser, click on the **Access** tab located on the left side.

   |image0|

#. Click **Guided Configuration**

   |image1|

#. Click **Zero Trust**

   |image2|

#. Click **Identity Aware Proxy**

   |image3|

#. Click **Next**


   .. NOTE::  Review the design considerations for deploying IAP in a **Single Proxy** versus a **Multi-proxy** solution.

   |image4|
   
   
   Lab 1.2 - Device Posture 
------------------------------------------------

In this section, you will configure the IAP to perform posture assessment from client devices.  

Task - Configure name of IAP Policy and enable Posture Checks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Define the configuration name **IAP_DEMO**

#. Check **Enable F5 Client Posture Check**

#. select **ca.f5lab.local.crt** from the CA Trust Certificate dropdown list

#. Select **add** to create a posture assessment group

   |image5|

Task - Define a firewall Posture Assessment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Define the Posture Group Name **FW_CHECK**
#. Check the enable a **Firewall** box
#. Check the enable a **Domain Managed Devices** box
#. Enter the Domain Name **f5lab.local** 
#. Click **Done**

   |image6|


Task - Verify the posture assessment 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. The Posture Settings box should contain **FW_CHECK**
#. Click **Save & Next**

   |image7|
   
   
   Lab 1.3 - Virtual Server
------------------------------------------------

In this section, you will define the virtual server IP address and its SSL profile settings 

Task - Create a virtual server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Click **Show Advanced Setting** located in the top right corner to expose the Server-Side SSL profile settings
#. Enter the IP address **10.1.10.100**

   |image8|


#. Click the **Create New** radio button under Client SSL Profile
#. Select **acme.com-wildcard** from the Client SSL certificate dropdown box
#. Select **acme.com-wildcard** from the Associated Private Key dropdown box
#. Select **ca.f5lab.local.crt** from the Trusted Certificate Authorities for Client Authentication drop down box

   |image9|

#. In the **Server SSL Profile** section, move the **serverssl** SSL Profile to the **Selected** side (select item and then click the right-arrow)
#. Click **Save & Next**

   |image10|


Lab 1.4 - User Identity
------------------------------------------------

In this section you will configure a single User Identity using Active Directory.  

Task - Configure Active Directory AAA
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Enter **"ad"** for the name
#. Ensure the Authentication Type is **AAA**
#. Ensure the Choose Authentication Server Type is set to **Active Directory**
#. Select **ad-servers** from the Choose Authentication Server dropdown box
#. Check **Active Directory Query Properties**
#. Select the **memberOf** in the Required Attributes box 
#. Click **Save**
#. Click **Save & Next**

|image11|





Lab 1.5 - MFA
------------------------------------------------

In this section you will configure a RADIUS server to enable simulated MFA capabilities.


Task - Configure a RADIUS AAA Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#. Check **Enable MultiFactor Authentication**

   |image13|

#. Select **Custom Radius Based**

   |image14|

#. Select **Create New** from the Choose RADIUS Server dropdown

   |image15|

#. Enter the Server Pool Name **radius_pool**
#. Enter the Server Address **10.1.20.8**
#. Enter the Secret **secret**
#. Click **Save**

   |image16|

#. Verify Custom RADIUS based Authentication appears
#. Click **Save & Next**

   |image17|

	
	Lab 1.6 - SSO & HTTP Header
------------------------------------------------

In this section you will configure HTTP Basic SSO.

Task - Create a HTTP basic SSO object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#. Check **Enable Single Sign-On(Optional)**

   |image18|

#. Enter the name **basic_sso**
#. Verify **HTTP Basic** is selected
#. Select **Create New** from the SSO Configuration Object dropdown box

   |image19|

#. Verify the Username Source is **session.sso.token.last.username**
#. Verify the Password Source is **session.sso.token.last.password**
#. Click **Save**

   |image20|


#. Verify the **basic_sso** object was created
#. click **Save & Next**

   |image21|



	

Lab 1.7 - Applications
------------------------------------------------

In this section you will define a single application

Task - Create basic.acme.com application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Enter the **basic.acme.com** for the application name
#. Enter the **basic.acme.com** for the FQDN
#. Enter the IP address **10.1.20.6** for the pool member
#. Click **Save** 

|image22|



Lab 1.8 - Application Groups
------------------------------------------------

Application Groups will be covered in a later section of the lab.

Task - Skip Application Group Section
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Click **Save & Next**

|image28|

Lab 1.9 - Contextual Access
------------------------------------------------

In this section you will define contextual access for the previously created application.  Context access is where all of the previously created objects are put together to provide fine-grain access control.

Task - Create Contextual Access for basic.acme.com
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


#. Enter **basic.acme.com** for the contextual access name
#. Select **basic.acme.com** from the Resource dropdown box
#. Select **fw_check** from the Device Posture dropdown box
#. Select **ad** from the Primary Authentication dropdown box
#. Select **basic_sso** from the Single Sign-On dropdown box
#. Check **Enable Additional Checks**

   |image23|

#. For the **Default Fallback** rule, select **Step Up** from the dropdown box under **Match Action**

#. Select **Custom Radius based Authentication (MFA)** from the Step Up Authentication box

   |image24|

#. Click **Save & Next**

   |image25|



Lab 1.10 - Customization
------------------------------------------------

The Customization section allows an administrator to define the images, colors, and messages that are presented to a user.

Task - Customize the Remediation Page URL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The default **remediation Page** URL uses the hostname site **request.com**.  This should be changed to reference a real host where users can download and install the EPI updates.

#. Scroll down to the Remediation Page Section

   |image29|

#. Enter the URL **https://iap1.acme.com/epi/downloads**

   |image30|

#. Click **Save & Next**

#. On the Logon Protection menu, Click **Save & Next**




Lab 1.11 - Summary
------------------------------------------------

The **Summary** page allows you to review the configuration that is about to be deployed.  In the event a change is required anywhere in the configuration the **pencil icon** on the right side can be selected to quickly edit the appropriate section.



Task - Deploy the configuration 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Click **Deploy**

   |image31|

#. Once the deployment is complete, click **Finish**


Lab 1.12 - Testing 
------------------------------------------------

In this section you will access the application basic.acme.com and watch how the BIG-IP restricts access when a device fails it's posture assessment.

Task - Access basic.acme.com
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. NOTE:: Posture Assessments in a Per-Request Policy use F5 Access Guard(running on clients) to perform posture assessments prior to accessing an application.  This improves the user experience since posture checks do not introduce any delay when accessing the application. This also improves security by allowing posture assessments to occur continuously throughout the life of the session.

#. From the jumpbox, browse to https://basic.acme.com
#. At the logon page enter the Username:**user1** and Password:**user1**
#. Click **Logon**

   |image33|


#. The RADIUS logon page, prepopulates the username:**user1**.  Enter the PIN: **123456**

   |image34|

#. The SSO profile passes the username and password to the website for logon.

   |image35|

#. Close the browser Window to ensure there is not cached data



Task - Disable Windows Firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Right click the computer icon in the taskbar and open **Network and Sharing Center**

   |image36|

#. Click **Windows Firewall**

   |image37|

#. Click **Turn Windows Firewall on or off**

   |image38|

#. Click the radio button **Turn off Windows Firewall** under Public Network Settings
#. Click **Ok**

   |image39|


Task - See Deny Page basic.acme.com 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the jumpbox, browse to https://basic.acme.com

#. Refresh the screen using the F5 key until the deny page appears.

#. After approximately 15 seconds you will receive a deny page from the IAP stating that you have failed the network firewall check

   |image40|

#. Close the browser Window to ensure there is no cached data


Task - Enable Windows Firewall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Right click the computer icon in the taskbar and open **Network and Sharing Center**

   |image36|

#. Click **Windows Firewall**

   |image37|

#. Click **Turn Windows Firewall on or off**

   |image38|

#. Click the radio button **Turn on Windows Firewall** under Public Network Settings
#. Click **Ok**

   |image41|
   
#. From the jumpbox, browse to https://basic.acme.com to sure you can connect. 
















.. |image0| image:: media/lab01/image000.png
.. |image1| image:: media/lab01/image001.png
.. |image2| image:: media/lab01/image002.png
.. |image3| image:: media/lab01/image003.png
.. |image4| image:: media/lab01/image004.png
.. |image5| image:: media/lab01/image005.png
.. |image6| image:: media/lab01/image006.png
.. |image7| image:: media/lab01/image007.png
.. |image8| image:: media/lab01/image008.png
.. |image9| image:: media/lab01/image009.png
.. |image10| image:: media/lab01/image010.png
.. |image11| image:: media/lab01/image011.png
.. |image13| image:: media/lab01/image013.png
.. |image14| image:: media/lab01/image014.png
.. |image15| image:: media/lab01/image015.png
.. |image16| image:: media/lab01/image016.png
.. |image17| image:: media/lab01/image017.png
.. |image18| image:: media/lab01/image018.png
.. |image19| image:: media/lab01/image019.png
.. |image20| image:: media/lab01/image020.png
.. |image21| image:: media/lab01/image021.png
.. |image22| image:: media/lab01/image022.png
.. |image23| image:: media/lab01/image023.png
.. |image24| image:: media/lab01/image024.png
.. |image25| image:: media/lab01/image025.png
.. |image28| image:: media/lab01/image028.png
.. |image29| image:: media/lab01/image029.png
.. |image30| image:: media/lab01/image030.png
.. |image31| image:: media/lab01/image031.png
.. |image32| image:: media/lab01/image032.png
.. |image33| image:: media/lab01/image033.png
.. |image34| image:: media/lab01/image034.png
.. |image35| image:: media/lab01/image035.png
.. |image36| image:: media/lab01/image036.png
.. |image37| image:: media/lab01/image037.png
.. |image38| image:: media/lab01/image038.png
.. |image39| image:: media/lab01/image039.png
.. |image40| image:: media/lab01/image040.png
.. |image41| image:: media/lab01/image041.png
.. |image42| image:: media/lab01/image042.png
.. |image43| image:: media/lab01/image043.png


