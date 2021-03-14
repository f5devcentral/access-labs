Lab 2: Step up Authentication with Per-Request Policies
=====================================

Objectives
----------

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
| |Lab2-Image1|                                                                                |
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
| |Lab2-Image2|                                                                                |
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
| |Lab2-Image3|                                                                                |
|                                                                                              |
| |Lab2-Image4|                                                                                |
+----------------------------------------------------------------------------------------------+

Task 2: Step Up Authentication with Per Request Policies
--------------------------------------
Step-up authentication can be used to protect layers or parts of a web application that manage more sensitive data. It can be used to increase protection by requiring stronger authentication within an already authenticated access to the web application.
Step-up authentication can be a part of using the portal access or web application management (reverse proxy) features of Access Policy Manager.

In this example we're going to use a Per-Request Policy with a subroutine to authenticate user when they access a specific URI, extract information from Active Directory and submit that information as a header

+----------------------------------------------------------------------------------------------+
| 5. Begin by selecting: **Access -> Profiles/Policies -> Per Request Policies** ->            |
|                                                                                              |
| 6. Click the **Create** button (far right)                                                   |
|                                                                                              |
+----------------------------------------------------------------------------------------------+
| |Lab2-Image7|                                                                                |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. Give the policy a name and select the Language Settings                                   |
|                                                                                              |
|    -  **Name**: **app.acme.com-PRP**                                                         |
|                                                                                              |
|    -  **Accept Languages**: **English (en)**                                                 |
+----------------------------------------------------------------------------------------------+
| |Lab2-Image8|                                                                                |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. On the app.acme.com-PRP policy click **Edit**                                             |
|                                                                                              |
| 5. Click on **Add New Subroutine**                                                           |
|                                                                                              |
| |Lab2-Image10|                                                                               |
|                                                                                              |
| 6. Give it a name and Click Save                                                             |
|                                                                                              |
|    -  **Name**: **AD_Subroutine**                                                            |
|                                                                                              |                                                                                           |
| |Lab2-Image11|                                                                               |
|                                                                                              |
| 7. Click the + between In and Out                                                            |
|                                                                                              |
| 8. Click the **Logon** Tab                                                                   |
|                                                                                              |
| 9. At the middle of the list choose **Logon Page** and click **Add Item**                    |
|                                                                                              |
| 10. Select **Save** at the bottom of the Logon Page dialog box                               |
|                                                                                              |
|                                                                                              |
| |Lab2-Image12|                                                                               |
|                                                                                              |
| |Lab2-Image13|                                                                               |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. In the subroutine, between the Logon page and the green out branch click the + sign and   |
|   select the **Logon Tab** and click the **Logon Page** radio button                         |
|   |Lab2-Image14|                                                                             |
|   |Lab2-Image15|                                                                             |
|                                                                                              |
|   |Lab2-Image16|                                                                             |                                                                                           |
| 5. Click on **Authentication**                                                               |
|                                                                                              |
|   |Lab2-Image17|                                                                             |
|                                                                                              |
| 6. Select AD Auth and click **Add Item** at the bottom                                       |
|   |Lab2-Image18|                                                                             |
|                                                                                              |
| 7. Give the item a name                                                                      |
|    -  **Name**: **AD_Auth**                                                                  |
|                                                                                              |
| 8. Select **/Common/Lab_SSO_AD_Server** for the Server option                                |
|                                                                                              |
| 8. Click the **Save**                                                                        |
|    |Lab2-Image19|                                                                            |
| 9. Between **AD Auth** and the Out endpoint click the + Sign                                 |
|                                                                                              |
| 10. Select Authentication and Select the **AD Query radio button and click **Add Item**      |
|                                                                                              |
| 11. Change the **Server** option to **/Common/Lab_SSO_AD_Server** and click **Save**         |
|                                                                                              |
| 12. Between **AD Query** and the Out endpoint click the + Sign                               |
|                                                                                              |
| 13. Navigate to the **Assignment** tab and select **Variable Assign** and click **Add Item** |
|                                                                                              |
| 14. Under Variable Assign click **Add New Entry**                                            |
|                                                                                              |
| 15. Next to "Empty" click the **change** links                                               |
|                                                                                              |
| 16. Change the drop down on the right hand side to **Session Varaible** and imput the        |
| following value                                                                              |
|    - **subsession.ad.last.attr.memberOf**                                                    |
|                                                                                              |
| 17. In the left hand box type the following then click finished and Save                     |
|   - **session.adgroups.custom**                                                              |
|                                                                                              |
|                                                                                              |
|                                                                                              |
+----------------------------------------------------------------------------------------------+
| |Lab2-Image20|                                                                               |
|                                                                                              |
| |Lab2-Image21|                                                                               |
|                                                                                              |
| |Lab2-Image22|                                                                               |
|                                                                                              |
| |Lab2-Image23|                                                                               |
|                                                                                              |
| |Lab2-Image24|                                                                               |
|                                                                                              |
| |Lab2-Image25|                                                                               |
|                                                                                              |
| |Lab2-Image26|                                                                               |
|                                                                                              |
| |Lab2-Image27|                                                                               |
|                                                                                              |
| |Lab2-Image28|                                                                               |
|                                                                                              |
| |Lab2-Image29|                                                                               |
|                                                                                              |
| |Lab2-Image30|                                                                               |
|                                                                                              |
| |Lab2-Image31|                                                                               |
|                                                                                              |
| |Lab2-Image32|                                                                               |
|                                                                                              |
| |Lab2-Image33|                                                                               |
|                                                                                              |
| |Lab2-Image34|                                                                               |
|                                                                                              |
| |Lab2-Image35|                                                                               |
|                                                                                              |
| |Lab2-Image36|                                                                               |
|                                                                                              |
| |Lab2-Image37|                                                                               |
+----------------------------------------------------------------------------------------------+


Lab 2 is now complete.

.. |Lab2-Image1| image:: /class1/module2/media/Lab2-Image1.png
.. |Lab2-Image2| image:: /class1/module2/media/Lab2-Image2.png
.. |Lab2-Image3| image:: /class1/module2/media/Lab2-Image3.png
.. |Lab2-Image4| image:: /class1/module2/media/Lab2-Image4.png
.. |Lab2-Image5| image:: /class1/module2/media/Lab2-Image5.png
.. |Lab2-Image6| image:: /class1/module2/media/Lab2-Image6.png
.. |Lab2-Image7| image:: /class1/module2/media/Lab2-Image7.png
.. |Lab2-Image8| image:: /class1/module2/media/Lab2-Image8.png
.. |Lab2-Image9| image:: /class1/module2/media/Lab2-Image9.png
.. |Lab2-Image10| image:: /class1/module2/media/Lab2-Image10.PNG
.. |Lab2-Image11| image:: /class1/module2/media/Lab2-Image11.png
.. |Lab2-Image12| image:: /class1/module2/media/Lab2-Image12.png
.. |Lab2-Image13| image:: /class1/module2/media/Lab2-Image13.png
.. |Lab2-Image14| image:: /class1/module2/media/Lab2-Image14.png
.. |Lab2-Image15| image:: /class1/module2/media/Lab2-Image15.png
.. |Lab2-Image16| image:: /class1/module2/media/Lab2-Image16.png
.. |Lab2-Image17| image:: /class1/module2/media/Lab2-Image17.png
.. |Lab2-Image18| image:: /class1/module2/media/Lab2-Image18.png
.. |Lab2-Image19| image:: /class1/module2/media/Lab2-Image19.png
.. |Lab2-Image20| image:: /class1/module2/media/Lab2-Image20.png
.. |Lab2-Image21| image:: /class1/module2/media/Lab2-Image21.png
.. |Lab2-Image22| image:: /class1/module2/media/Lab2-Image22.png
.. |Lab2-Image23| image:: /class1/module2/media/Lab2-Image23.png
.. |Lab2-Image24| image:: /class1/module2/media/Lab2-Image24.png
.. |Lab2-Image25| image:: /class1/module2/media/Lab2-Image25.png
.. |Lab2-Image26| image:: /class1/module2/media/Lab2-Image26.png
.. |Lab2-Image27| image:: /class1/module2/media/Lab2-Image27.png
.. |Lab2-Image28| image:: /class1/module2/media/Lab2-Image28.png
.. |Lab2-Image29| image:: /class1/module2/media/Lab2-Image29.png
.. |Lab2-Image30| image:: /class1/module2/media/Lab2-Image30.png
.. |Lab2-Image31| image:: /class1/module2/media/Lab2-Image31.png
.. |Lab2-Image32| image:: /class1/module2/media/Lab2-Image32.png
.. |Lab2-Image33| image:: /class1/module2/media/Lab2-Image33.png
.. |Lab2-Image34| image:: /class1/module2/media/Lab2-Image34.png
.. |Lab2-Image35| image:: /class1/module2/media/Lab2-Image35.png
.. |Lab2-Image36| image:: /class1/module2/media/Lab2-Image36.png
.. |Lab2-Image37| image:: /class1/module2/media/Lab2-Image37.png
