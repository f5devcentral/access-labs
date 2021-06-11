Lab 6: SAML IdP Chaining to AzureAD (BIG-IP Primary IdP)
========================================================



Task 1 - Setup Lab Environment
-----------------------------------

To access your dedicated student lab environment, you will need a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Unified Demo Framework (UDF) Training Portal. The RDP client will be used to connect to the jumphost, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumphost.f5lab.local

   |image001|

#. Select your RDP resolution.

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#. Login with the following credentials:

         - User: **f5lab\\user1**
         - Password: **user1**

#. After successful logon the Chrome browser will auto launch opening the site https://portal.f5lab.local.  This process usually takes 30 seconds after logon.

#. Click the **Classes** tab at the top of the page.

	|image002|

#. Scroll down the page until you see **301 SAML Federation** on the left

   |image003|

#. Hover over tile **SAML IdP Chaining to AzureAD (BIG-IP Primary IdP)**. A start and stop icon should appear within the tile.  Click the **Play** Button to start the automation to build the environment

   +---------------+-------------+
   | |image004|    | |image005|  |
   +---------------+-------------+ 

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image006|


Task 3 - Create portal.acme.com SAML Service Provider(SP) Service
--------------------------------------------------------------------

#. Begin by selecting: Access ‑> Federation ‑> SAML Service Provider ‑> Local SP Services. Click the **Plus (+) Sign** 

   |image009|

#. In the **Create New SAML SP Service** dialog box, click **General Settngs** in the left navigation pane and key in the following:

   +-------------------+--------------------------------+
   | Service Name:     | ``portal.acme.com-sp-s``       |
   +-------------------+--------------------------------+
   | Entity ID:        | ``https://portal.acme.com``    |
   +-------------------+--------------------------------+

#. Click **OK**

   |image010|

#. Select the **Checkbox** next to the previously created ``portal.acme.com``
   and click the **Bind/Unbind IdP Connectors** button at the bottom of the GUI

   |image011|

#. Click **Add New Row**

   |image012|

#. Select **/Common/azure-idp** from the SAML IdP Connectors dropdown menu
#. Click **Update**

.. NOTE:: The Azure IdP connector was previously configured through the automation.

   |image013|

#. Click **OK**

   |image014|

Task 2 ‑ Configure the SAML Identity Provider (IdP) Service 
-------------------------------------------------------------


#. Begin by selecting: Access ‑> Federation ‑> SAML Identity Provider ‑> Local IdP Services. Click the **Plus (+) Sign** 

   |image015|

#. In the **Create New SAML IdP Service** dialog box, click **General Settngs**
   in the left navigation pane and key in the following:

   +-------------------+--------------------------------+
   | IdP Service Name: | ``portal.acme.com-idp-s``      |
   +-------------------+--------------------------------+
   | IdP Entity ID:    | ``https://portal.acme.com``    |
   +-------------------+--------------------------------+

   |image016|

   .. NOTE:: The yellow box on "Host" will disappear when the Entity ID is
      entered

#. In the **Create New SAML IdP Service** dialog box, click **Assertion
   Settings** in the left navigation pane and key in the following:

   +----------------------------------------+-----------------------------------------------------------------+
   | Assertion Subject Type:                | ``Persistent Identifier`` (drop down)                           |
   +----------------------------------------+-----------------------------------------------------------------+
   | Assertion Subject Value:               | ``%{session.logon.last.username}`` (drop down)                  |
   +----------------------------------------+-----------------------------------------------------------------+
   | Authentication Context Class Reference | ``urn:oasis:names:tc:SAML:2.0:ac:classes:unspecified``          |  
   +----------------------------------------+-----------------------------------------------------------------+

   |image017|

#. In the **Create New SAML IdP Service** dialog box, click
   **Security Settings** in the left navigation pane and key in
   the following:

   +----------------------+-----------------------------------------+
   | Signing Key:         | ``/Common/portal.acme.com`` (drop down) |
   +----------------------+-----------------------------------------+
   | Signing Certificate: | ``/Common/portal.acme.com`` (drop down) |
   +----------------------+-----------------------------------------+

   .. NOTE:: The certificate and key were previously imported via automation

#. Click **OK** to complete the creation of the IdP service

   |image018|


#. Select the **Checkbox** next to the previously created ``portal.acme.com``
   and click the **Bind/Unbind SP Connectors** button at the bottom of the GUI

   |image019|

#. In the **Edit SAML SP's that use this IdP** dialog, select the
   ``/Common/sp.acme.com`` SAML SP Connection Name.  


#. Click the **OK** button at the bottom of the dialog box

   |image020|


Task 6 - Create a SAML Resource
---------------------------------


#. Begin by selecting **Access ‑> Federation ‑> SAML Resources >> **Plus (+) Sign**

   |image021|

#. In the **New SAML Resource** window, enter the following values:

   +--------------------+------------------------------+
   | Name:              | ``sp.acme.com``              |
   +--------------------+------------------------------+
   | SSO Configuration: | ``portal.acmem.com-idp-s``   |
   +--------------------+------------------------------+
   | Caption:           | ``sp.acme.com``              |
   +--------------------+------------------------------+

#. Click **Finished** at the bottom of the configuration window

   |image022|



Task 4 - Create a Webtop
-------------------------------

#. Select Access ‑> Webtops ‑> Webtop Lists >> **Plus (+) Sign**


   |image023|

#. In the resulting window, enter the following values:

   +------------------+----------------------+
   | Name:            | ``full_webtop``      |
   +------------------+----------------------+
   | Type:            | ``Full`` (drop down) |
   +------------------+----------------------+
   | Minimize To Tray | ``uncheck``          |
   +------------------+----------------------+

#. Click **Finished** at the bottom of the GUI

   |image024|

  
Task 7 - Create a SAML IdP Access Policy
---------------------------------------------

#. Select Access ‑> Profiles/Policies ‑> Access Profiles (Per-Session Policies) -> **Plus (+) Sign**

   |image025|

#. In the **New Profile** window, enter the following information:

   +----------------------+---------------------------+
   | Name:                | ``portal.acme.com‑psp``   |
   +----------------------+---------------------------+
   | Profile Type:        | ``All`` (drop down)       |
   +----------------------+---------------------------+
   | Profile Scope:       | ``Profile`` (default)     |
   +----------------------+---------------------------+
   | Customization Type:  | ``modern`` (default)      |
   +----------------------+---------------------------+

   |image026|


#. Scroll to the bottom of the **New Profile** window to the
   **Language Settings** section

#. Select *English* from the **Factory Built‑in Languages** menu on the
   right and click the **Double Arrow (<<)**, then click the **Finished**
   button.

#. The **Default Language** should be automatically set

   |image027|

#. From the **Access ‑> Profiles/Policies ‑> Access Profiles
   (Per-Session Policies) screen**, click the **Edit** link on the previously
   created ``portal.acme.com-psp`` line

   |image028|

#. Click the **Plus (+) Sign** between **Start** and **Deny**

   |image031|

#. In the pop-up dialog box, select the **Authentication** tab and then select the
   **Radio** next to **On-Demand Cert Auth**, and click the **Add Item** button

   |image032|

#. Click **Save** in the resulting Logon Page dialog box

   |image033|

#.  On the successful branch of the On-Demand Cert Auth Policy-Item click the **Plus (+) Sign**

    |image034|

#. In the pop-up dialog box, select the **Authentication** tab and then select the **Radio** next to **OCSP Auth**, and click the **Add Item** button

   |image035|

#. Select ``/Common/ocsp_servers`` from the **OCSP Responder** drop down menu.

#. Click **Save** at the bottom of the window

   |image036|

#. Click the **Plus (+) Sign** on the successful branch between **OCSP Auth** and **Deny**

   |image037|

#. In the pop-up dialog box, select the **Assignment** tab and then select
   the **Radio** next to **Variable Assign**, and click the
   **Add Item** button

   |image038|

#. Enter the Name **upn_extract**
#. Click **Add new entry**
#. Click **Change**

    |image039|

#. Enter the Custom Variable **session.custom.upn**
#. Select **Custom Expresssion** from the right drop down menu
#. Enter the text below for the custom expression.

    .. code-block:: text

        set x509e_fields [split [mcget {session.ssl.cert.x509extension}] "\n"];
        # For each element in the list:
        foreach field $x509e_fields {
        # If the element contains UPN:
        if { $field contains "othername:UPN" } {
        ## set start of UPN variable
        set start [expr {[string first "othername:UPN<" $field] +14}]
        # UPN format is <user@domain>
        # Return the UPN, by finding the index of opening and closing brackets, then use string range to get everything between.
        return [string range $field $start [expr { [string first ">" $field $start] - 1 } ] ];  } }
        #Otherwise return UPN Not Found:
        return "UPN-NOT-FOUND";

#. Click **Finished**

    |image040|

#. Click **Save**  

    |image041|

#. Click the **Plus (+) Sign** between **upn_extract** and **Deny**  

    |image042|

#. In the pop-up dialog box, select the **Authentication** tab and then select
   the **Radio** next to **LDAP Query**, and click the
   **Add Item** button

   |image043|

#. In the **LDAP Query Properties** window, enter the following information:

   +----------------------+------------------------------------------------+
   | Server:              | ``/Common/ldap_servers`` (drop down)           |
   +----------------------+------------------------------------------------+
   | Search DN:           | ``dc=f5lab,dc=local`` (drop down)              |
   +----------------------+------------------------------------------------+
   | SearchFilter:        | ``(userPrincipalName=%{session.custom.upn})``  |
   +----------------------+------------------------------------------------+
   
#. Click **Add new entry**
#. Add **sAMAAccountName** to the list of Required Attributes
   
    |image044|


#. Click the **Branch Rules** tab
#. Click the **X** on the User Group Membership line

    |image045|

#. Click **Add Branch Rule**

    |image046|

#. Enter the name **LDAP Query Passed**
#. Click **change**

    |image047|

#. Click **Add Expression**

    |image048|

#. Select **LDAP Query** from the Context dropdown menu
#. Select **LDAP Query Passed** from the Condition dropdown menu
#. Click **Add Expression**

    |image049|

#. Click **Finsished**

    |image050|

#. Click **Save**

    |image051|

#. Click the **Plus (+) Sign** on the LDAP Query Passed branch between **LDAP Query** and **Deny**  

    |image052|

#. In the pop-up dialog box, select the **Assignment** tab and then select
   the **Radio** next to **Variable Assign**, and click the
   **Add Item** button

   |image053|

#. Enter the Name **set_username**
#. Click **Add new entry**
#. Click **Change**

    |image054|

#. Enter the Custom Variable **session.logon.last.username**
#. Select **Session Variable** from the right drop down menu
#. Enter the session variable name **session.ldap.last.attr.sAMAccountName**
#. Click **Finished**

    |image055|

#. Click **Save**

    |image056|

#. Click the **Plus (+) Sign** between **set_username** and **Deny**  

    |image057|

#. In the pop-up dialog box, select the **Assignment** tab and then select
   the **Radio** next to **Advanced Resource Assign**, and click the
   **Add Item** button

   |image058|


#. In the new Resource Assignment entry, click the **Add/Delete** link

   |image059|

#. In the resulting pop-up window, click the **SAML** tab, and select the
   **Checkbox** next to ``/Common/sp.acme.com``

   |image060|

#. Click the **Webtop** tab, and select the **Checkbox** next to
   ``/Common/full_webtop``

#. Click the **Update** button at the bottom of the window to complete
   the Resource Assignment entry

   |image061|


#. Click the **Save** button at the bottom of the **Advanced Resource Assign** window

   |image062|


#. In the **Visual Policy Editor**, select the **Deny** ending on the
   fallback branch following **Advanced Resource Assign**

   |image063|

#. In the **Select Ending** dialog box, selet the **Allow** radio button
   and then click **Save**

   |image064|

#. In the **Visual Policy Editor**, click **Apply Access Policy**
   (top left), and close the **Visual Policy Editor**

   |image065|


Task 8 - Create a Client-side SSL Profile
---------------------------------------------

#. Navigate to Local Traffic ‑> Profile -> SSL -> Client. Click the **Plus (+) Sign**

    |image066|

#. Enter the Name **idp.acme.com-clientssl**
#. Check the **custom box** on the Certificate Key Chain Line 
#. Click **Add**

    |image067|

#. Select **acme.com-wildcard** from the Certificate dropdown menu
#. Select **acme.com-wildcard** from the Key dropdown menu
#. Click **Add**

    |image068|

#. Check the **custom box** on the Trusted Certificate Authorities Line
#. Select **ca.f5lab.local** from the Trusted Certificate Authorities dropdown menu     
#. Check the **custom box** on the Advertised Certificate Authorities Line
#. Select **ca.f5lab.local** from the Advertised Certificate Authorities dropdown menu

    |image069|

#. Click **Finished**



Task 9 - Create an IdP Virtual Server
----------------------------------------

#. Begin by selecting Local Traffic ‑> Virtual Servers -> Virtual Server List. Click the **Plus (+) Sign** 


   |image070|

#. In the **New Virtual Server** window, enter the following information:

   +---------------------------+------------------------------+
   | General Properties                                       |
   +===========================+==============================+
   | Name:                     | ``idp.acme.com``             |
   +---------------------------+------------------------------+
   | Destination Address/Mask: | ``10.1.10.102``              |
   +---------------------------+------------------------------+
   | Service Port:             | ``443``                      |
   +---------------------------+------------------------------+

   |image071|

   +---------------------------+------------------------------+
   | Configuration                                            |
   +===========================+==============================+
   | HTTP Profile:             | ``http`` (drop down)         |
   +---------------------------+------------------------------+
   | SSL Profile (Client)      | ``idp.acme.com-clientssl``   |
   +---------------------------+------------------------------+

   |image072|

   +-----------------+---------------------------+
   | Access Policy                               |
   +=================+===========================+
   | Access Profile: | ``idp.acme.com-psp``      |
   +-----------------+---------------------------+

   |image073|


#. Scroll to the bottom of the configuration window and click **Finished**


Task 10 - Test the Configuration
------------------------------------------

#. From the jumphost, navigate to the SAML IdP you previously configured at **https://idp.acme.com**. 
#. Select the **user1** certificate
#. Click **OK**


   |image074|
  
#. Click **sp.acme.com**

   |image075|

#. You are then successfully logged into https://sp.acme.com and presented a webpage.

   |image076|

#. Review your Active Sessions **(Access ‑> Overview ‑> Active Sessions­­­)**

#. Review your Access Report Logs **(Access ‑> Overview ‑> Access Reports)**


Task 11 - Lab Cleanup
------------------------

#. From a browser on the jumphost navigate to https://portal.f5lab.local

#. Click the **Classes** tab at the top of the page.

   |image002|

#. Scroll down the page until you see **301 SAML Federation** on the left

   |image003|

#. Hover over tile **SAML IdP Chaining to AzureAD (BIG-IP Primary IdP)**. A start and stop icon should appear within the tile.  Click the **Stop** Button to trigger the automation to remove any prebuilt objects from the environment

   +---------------+-------------+
   | |image004|    | |image007|  |
   +---------------+-------------+ 

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image008|

#. This concludes the lab.

   |image000|


.. |image000| image:: ./media/lab06/000.png
.. |image001| image:: ./media/lab06/001.png
.. |image002| image:: ./media/lab06/002.png
.. |image003| image:: ./media/lab06/003.png
.. |image004| image:: ./media/lab06/004.png
.. |image005| image:: ./media/lab06/005.png
.. |image006| image:: ./media/lab06/006.png
.. |image007| image:: ./media/lab06/007.png
.. |image008| image:: ./media/lab06/008.png
.. |image009| image:: ./media/lab06/009.png
.. |image010| image:: ./media/lab06/010.png
.. |image011| image:: ./media/lab06/011.png
.. |image012| image:: ./media/lab06/012.png
.. |image013| image:: ./media/lab06/013.png
.. |image014| image:: ./media/lab06/014.png
.. |image015| image:: ./media/lab06/015.png
.. |image016| image:: ./media/lab06/016.png
.. |image017| image:: ./media/lab06/017.png
.. |image018| image:: ./media/lab06/018.png
.. |image019| image:: ./media/lab06/019.png
.. |image020| image:: ./media/lab06/020.png
.. |image021| image:: ./media/lab06/021.png
.. |image022| image:: ./media/lab06/022.png
.. |image023| image:: ./media/lab06/023.png
.. |image024| image:: ./media/lab06/024.png
.. |image025| image:: ./media/lab06/025.png
.. |image026| image:: ./media/lab06/026.png
.. |image027| image:: ./media/lab06/027.png
.. |image028| image:: ./media/lab06/028.png
.. |image029| image:: ./media/lab06/029.png
.. |image030| image:: ./media/lab06/030.png
.. |image031| image:: ./media/lab06/031.png
.. |image032| image:: ./media/lab06/032.png
.. |image033| image:: ./media/lab06/033.png
.. |image034| image:: ./media/lab06/034.png
.. |image035| image:: ./media/lab06/035.png
.. |image036| image:: ./media/lab06/036.png
.. |image037| image:: ./media/lab06/037.png
.. |image038| image:: ./media/lab06/038.png
.. |image039| image:: ./media/lab06/039.png
.. |image040| image:: ./media/lab06/040.png
.. |image041| image:: ./media/lab06/041.png
.. |image042| image:: ./media/lab06/042.png
.. |image043| image:: ./media/lab06/043.png
.. |image044| image:: ./media/lab06/044.png
.. |image045| image:: ./media/lab06/045.png
.. |image046| image:: ./media/lab06/046.png
.. |image047| image:: ./media/lab06/047.png
.. |image048| image:: ./media/lab06/048.png
.. |image049| image:: ./media/lab06/049.png
.. |image050| image:: ./media/lab06/050.png
.. |image051| image:: ./media/lab06/051.png
.. |image052| image:: ./media/lab06/052.png
.. |image053| image:: ./media/lab06/053.png
.. |image054| image:: ./media/lab06/054.png
.. |image055| image:: ./media/lab06/055.png
.. |image056| image:: ./media/lab06/056.png
.. |image057| image:: ./media/lab06/057.png
.. |image058| image:: ./media/lab06/058.png
.. |image059| image:: ./media/lab06/059.png
.. |image060| image:: ./media/lab06/060.png
.. |image061| image:: ./media/lab06/061.png
.. |image062| image:: ./media/lab06/062.png
.. |image063| image:: ./media/lab06/063.png
.. |image064| image:: ./media/lab06/064.png
.. |image065| image:: ./media/lab06/065.png
.. |image066| image:: ./media/lab06/066.png
.. |image067| image:: ./media/lab06/067.png
.. |image068| image:: ./media/lab06/068.png
.. |image069| image:: ./media/lab06/069.png
.. |image070| image:: ./media/lab06/070.png
.. |image071| image:: ./media/lab06/071.png
.. |image072| image:: ./media/lab06/072.png
.. |image073| image:: ./media/lab06/073.png
.. |image074| image:: ./media/lab06/074.png
.. |image075| image:: ./media/lab06/075.png
.. |image076| image:: ./media/lab06/076.png







