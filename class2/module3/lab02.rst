Lab 2: SAML SP Access Guided Configuration (AGC) Lab
=======================================================

The purpose of this lab is to configure and test SAML Federation Services.
This lab will be configured in two parts.  

Students will leverage Access Guided Configuration (AGC) to 
configure the various aspects of a SAML Service Provider (SP), import and bind to
a SAML Identity Provider (IdP) and test SP-Initiated SAML Federation.

Objective:
----------

-  Gain an understanding of SAML Federation configurations and
   their component parts through Access Guided Configuration (AGC)

-  Gain an understanding of the access flow for IDP & SP Initiated SAML

Lab Requirements:
-----------------

-  All Lab requirements will be noted in the tasks that follow

-  Estimated completion time: 25-30 minutes

                                                                         |

TASK 1: Configure a SAML Service Provider (SP) via AGC 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Navigate to **Access -> Guided Configuration** in the left-hand menu.                     |
|                                                                                              |
| 2. Once **Guided Configuration** loads, click on **Federation**.                             |
+----------------------------------------------------------------------------------------------+
| |image026|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. In the resulting **Federation** sub-menu click, **SAML Service Provider**.                |
+----------------------------------------------------------------------------------------------+
| |image027|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. In the resulting **SAML Service Provider** window, review the **{SP-Initiated)** flow     |
|                                                                                              |
|    and then click the **right arrow**.                                                       |
+----------------------------------------------------------------------------------------------+
| |image028|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 5. Review the **IdP-Initiated** flow and then scroll down to the bottom of the window.       |
+----------------------------------------------------------------------------------------------+
| |image029|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. Review the configuration objects to be created and the click **Next**.                    |
+----------------------------------------------------------------------------------------------+
| |image030|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 2: Configure the Service Provider
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Service Provider Properties** section, enter the following values in the fields  |
|                                                                                              |
|    provided:                                                                                 |
|                                                                                              |
|    * In the **Configuration Name** field input **agc-sp.acme.com**.                          |
|                                                                                              |
|    * In the **Entity ID** field input **https://agc-sp.acme.com**.                           |
|                                                                                              |
| 2. In the **Security Settings** section, check the checkbox next to **Sign Authentication**  |
|                                                                                              |
|    **Requests**.                                                                             |
|                                                                                              |
| 3. In the updated **Security Settings** section, use the dropdowns to select the following:  |
|                                                                                              |
|    * For the **Message Signing Key** select **saml-agc-sp.acme.com**.                        |
|                                                                                              |
|    * For the **Message Signing Certificate** select **saml-agc-sp.acme.com**.                |
|                                                                                              |
| 4. Click **Save & Next**.                                                                    |
+----------------------------------------------------------------------------------------------+
| |image031|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 3: Configure the Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Virtual Server Properties** section, enter the following values in the fields    |
|                                                                                              |
|    provided:                                                                                 |
|                                                                                              |
|    * In the **Destination Address** field input **10.1.10.103**.                             |
|                                                                                              |
|    * In the **Service Port** field input **443** **HTTPS**                                   |
|                                                                                              |
|    * In the **Redirect Port** field input **80** **HTTP**                                    |
|                                                                                              |
| 2. In the **Client SSL Profile** section, use the arrows to move only the                    |
|                                                                                              |
|    **wildcard.acme.com** profile to the right-hand column as shown.                          |
|                                                                                              |
| 3. Click **Save & Next**.                                                                    |
+----------------------------------------------------------------------------------------------+
| |image032|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 4: Configure External IdP Connector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **External Identity Provider Connector Settings** section, use the first dropdown  |
|                                                                                              |
|    **Select Method to configure your IdP Connector** to select **Metadata**.                 |
|                                                                                              |
| 2. In the updated window, click the **Choose File** button and then browse the **Jumphost**  |
|                                                                                              |
|    desktop and select the file **idp_partner_com_metadata.xml**.                             |
|                                                                                              |
| 3. In the **Name** field, input **idp.partner.com**                                          |
|                                                                                              |
| 4. Click **Save & Next**.                                                                    |
+----------------------------------------------------------------------------------------------+
| |image033|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 5: Configure Pool
~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Click **Show Advanced Setting** in the upper right of the **Guided Configuration**.       |
|                                                                                              |
| 2. In the **Pool Properties** section, use the dropdown to select **Create New** for         |
|                                                                                              |
|    **Select a Pool**.                                                                        |
|                                                                                              |
| 3. In the **Health Monitors** section, use the arrows to move only the **/Common/http**      |
|                                                                                              |
|    health monitor to the right-hand column as shown.                                         |
|                                                                                              |
| 4. In the **Resource Properties** section, use the dropdown to select **Least Connections**  |
|                                                                                              |
|    **(member)** for **Load Balancing Method**.                                               |
|                                                                                              |
| 5. For the **Pool Servers** section, use the first dropdown for **IP Address/Node Name** to  |
|                                                                                              |
|    select **/Common/10.1.20.6**. Ensure port **80** and **HTTP** are set for the **Port**.   |
|                                                                                              |
| 6. Click **Save & Next**.                                                                    |
+----------------------------------------------------------------------------------------------+
| |image034|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 6: Configure SSO
~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Single Sign-On Settings** section, check the **Enable Signle Sign-On** checkbox. |
|                                                                                              |
| 2. Use the **Selected Single Sign-On Type** dropdown to select **HTTP header-based**.        |
|                                                                                              |
| 3. In the **Username Source** field, ensure **session.saml.last.identity** is present.       |
|                                                                                              |
| 4. In the **SSO Headers** section, makes sure the following values are correct:              |
|                                                                                              |
|    * **Header Operation: replace**                                                           |
|                                                                                              |
|    * **Header Name: Authorization**                                                          |
|                                                                                              |
|    * **Header Value: %{session.saml.last.identity}**                                         |
|                                                                                              |
| 5. Scroll to the bottom of the window and Click **Save & Next**.                             |
+----------------------------------------------------------------------------------------------+
| |image035|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 7: Configure Endpoint Checks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Endpoints Checks Properties** window, click **Save & Next**.                     |
|                                                                                              |
| **Note:** *Endpoints checks can also be configured to protect application access.  The*      |
|                                                                                              |
| *Access 302 Lab, hosted at this year's Agility will have additional details.*                |
+----------------------------------------------------------------------------------------------+
| |image036|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 8: Configure Session Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Review the Session Managment settings, in the **Timeout Settings** section then scroll to |
|                                                                                              |
|    the bottom of the window and click **Save & Next**.                                       |
+----------------------------------------------------------------------------------------------+
| |image037|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 9: Review the Summary and Deploy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Review the Summary, then scroll to the bottom of the window and click **Deploy**.         |
+----------------------------------------------------------------------------------------------+
| |image038|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. The application is now deployed click **Finish**.                                         |
+----------------------------------------------------------------------------------------------+
| |image039|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. Review the Access Guided Confguration window, **Status** for **agc-sp.acme.com** is       |
|                                                                                              |
|    **DEPLOYED**.                                                                             |
+----------------------------------------------------------------------------------------------+
| |image040|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK: 10: Testing the SAML Service Provider (SP)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Open Firefox from the Jumphost desktop and click on the **AGC-SP (Partner)** link in the  |
|                                                                                              |
|    bookmark toolbar.                                                                         |
|                                                                                              |
| **Note:** *If you have issues, open Firefox in a New Private Window (Incognito/Safe Mode)*   |
+----------------------------------------------------------------------------------------------+
| |image041|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. Once the page loads, enter **user1** for username and **user1** for password  in the      |
|                                                                                              |
|    **Partner Secure Logon** form and click the **Logon** button.                             |
+----------------------------------------------------------------------------------------------+
| |image042|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. The **Partner Application** will now open if successfully configured.                     |
+----------------------------------------------------------------------------------------------+
| |image043|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 11: End of Lab1
~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. This concludes Part 2 of Lab1. This concludes Lab1, feel free to review and test the      |
|                                                                                              |
|    configuration.                                                                            |
+----------------------------------------------------------------------------------------------+
| |image000|                                                                                   |
+----------------------------------------------------------------------------------------------+

.. |image000| image:: ./media/image001.png
   :width: 800px
.. |image001| image:: ./media/lab1-001.png
   :width: 800px
.. |image002| image:: ./media/lab1-002.png
   :width: 800px
.. |image003| image:: ./media/lab1-003.png
   :width: 800px
.. |image004| image:: ./media/lab1-004.png
   :width: 800px
.. |image005| image:: ./media/lab1-005.png
   :width: 800px
.. |image006| image:: ./media/lab1-006.png
   :width: 800px
.. |image007| image:: ./media/lab1-007.png
   :width: 800px
.. |image008| image:: ./media/lab1-008.png
   :width: 800px
.. |image009| image:: ./media/lab1-009.png
   :width: 800px
.. |image010| image:: ./media/lab1-010.png
   :width: 800px
.. |image011| image:: ./media/lab1-011.png
   :width: 800px
.. |image012| image:: ./media/lab1-012.png
   :width: 800px
.. |image013| image:: ./media/lab1-013.png
   :width: 800px
.. |image014| image:: ./media/lab1-014.png
   :width: 800px
.. |image015| image:: ./media/lab1-015.png
   :width: 800px
.. |image016| image:: ./media/lab1-016.png
   :width: 800px
.. |image017| image:: ./media/lab1-017.png
   :width: 800px
.. |image018| image:: ./media/lab1-018.png
   :width: 800px
.. |image019| image:: ./media/lab1-019.png
   :width: 800px
.. |image020| image:: ./media/lab1-020.png
   :width: 800px
.. |image021| image:: ./media/lab1-021.png
   :width: 800px
.. |image022| image:: ./media/lab1-022.png
   :width: 800px
.. |image023| image:: ./media/lab1-023.png
   :width: 800px
.. |image024| image:: ./media/lab1-024.png
   :width: 800px
.. |image025| image:: ./media/lab1-025.png
   :width: 800px
.. |image026| image:: ./media/lab1-026.png
   :width: 800px
.. |image027| image:: ./media/lab1-027.png
   :width: 800px
.. |image028| image:: ./media/lab1-028.png
   :width: 800px
.. |image029| image:: ./media/lab1-029.png
   :width: 800px
.. |image030| image:: ./media/lab1-030.png
   :width: 800px
.. |image031| image:: ./media/lab1-031.png
   :width: 800px
.. |image032| image:: ./media/lab1-032.png
   :width: 800px
.. |image033| image:: ./media/lab1-033.png
   :width: 800px
.. |image034| image:: ./media/lab1-034.png
   :width: 800px
.. |image035| image:: ./media/lab1-035.png
   :width: 800px
.. |image036| image:: ./media/lab1-036.png
   :width: 800px
.. |image037| image:: ./media/lab1-037.png
   :width: 800px
.. |image038| image:: ./media/lab1-038.png
   :width: 800px
.. |image039| image:: ./media/lab1-039.png
   :width: 800px
.. |image040| image:: ./media/lab1-040.png
   :width: 800px
.. |image041| image:: ./media/lab1-041.png
   :width: 800px
.. |image042| image:: ./media/lab1-042.png
   :width: 800px
.. |image043| image:: ./media/lab1-043.png
   :width: 800px

