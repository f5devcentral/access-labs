Lab 1.1: Create a SAML Identity Provider 
----------------------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="steelblue1"]
         spconnector [label="SP Connector"]
         bind [label="Bind Connectors"]
         resource [label="SAML Resource"]
         webtop [label="Webtop"]
         profile [label="Access Profile"]
         vs [label="VS"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

Task 1 - Create a Local IdP Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this lab we will create the local Identity Provider service. This
service is responsbile for handling the authentication for the SaaS
application.

.. NOTE:: This guide may require you to Copy/Paste information from the
   guide to your jumphost.  To make this easier you can open a copy of the
   guide by using the **Lab Guide** bookmark in Chrome.

a. Navigate to :menuselection:`Access --> Federation --> SAML Identity Provider --> Local IdP Services`
b. Click the :menuselection:`+` sign

    |image1|

c. Configure the :guilabel:`General Settings`:

    +------------------+------------------------+
    | Property         | Value                  |
    +==================+========================+
    | IdP Service Name | idp.f5demo.com         |
    +------------------+------------------------+
    | IdP Entity Id    | https://idp.f5demo.com |
    +------------------+------------------------+

    |image2|

d. Configure the :guilabel:`Assertiion Settings`:

    +-------------------------+--------------------------------+
    | Property                | Value                          |
    +=========================+================================+
    | Assertion Subject Value | %{session.logon.last.username} |
    +-------------------------+--------------------------------+

    |image3|

e. Configure the :guilabel:`Security Settings`:

    +---------------------+------------------------+
    | Property            | Value                  |
    +=====================+========================+
    | Signing Key         | idp.f5demo.com.key     |
    +---------------------+------------------------+
    | Signing Certificate | idp.f5demo.com.crt     |
    +---------------------+------------------------+

    |image4|

f. Click the :guilabel:`OK` button.

Lab 1.2: Create an External SP Connector
----------------------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="steelblue1"]
         bind [label="Bind Connectors"]
         resource [label="SAML Resource"]
         webtop [label="Webtop"]
         profile [label="Access Profile"]
         vs [label="VS"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

Now that we have the Identity Provider configured, we need to configure
the BIG-IP so it is aware of the Service Provider (the SaaS
application). We do this by defining an External SP Connector using the
metadata provided by the SaaS application, importing it into the
BIG-IP, and setting the appropriate cryptographic controls.

Task 1 - Obtain the SAML Service Provider Metadata
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In a common deployment the metadata is provided by the application.
This lab is no different, but the access method will vary. Follow the
listed steps below to obtain the necessary XML file.

a. Open a browser and nagivate to https://app.f5demo.com/metadata.xml
b. Save the file as ``app.f5demo.com.xml``

Task 2 - Create an External SP Connector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In this task we will create the External SP Connector object.

a. Navigate to :menuselection:`Access --> Federation --> SAML Identity Provider --> External SP Connector`
b. Click on the triangle on the right side of the :guilabel:`Create` button and select :guilabel:`From Metadata`
    
    |image5|

c. Enter the following information:

    +-----------------------+------------------------------+
    | Property              | Value                        |
    +=======================+==============================+
    | Select File           | app.f5demo.com.xml           |
    +-----------------------+------------------------------+
    | Service Provider Name | app.f5demo.com               |
    +-----------------------+------------------------------+

    |image6|

d. Click the :guilabel:`OK` button

Task 3 - Modify the SP Connector Settings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Finally, for security purposes, we'll configure the External SP
Connector object to require that resposes are cryptographically signed.
This prevents an attacker from manipulating the response and
potentially gaining unauthorized access.


a. Click the checkbox next to :guilabel:`app.f5demo.com` and click the :guilabel:`Edit` button

b. Modify the following :guilabel:`Security Settings`:

    +---------------------------------------+-----------+
    | Property                              | Value     |
    +=======================================+===========+
    | Response must be signed               | checked   |
    +---------------------------------------+-----------+

    |image7|

c. Click the :guilabel:`OK` button.


Lab 1.3: Bind SP Connectors
-----------------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="palegreen"]
         bind [label="Bind Connectors",color="steelblue1"]
         resource [label="SAML Resource"]
         webtop [label="Webtop"]
         profile [label="Access Profile"]
         vs [label="VS"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

Once we have the Identity Provider and Service Provider objects
configured, we need to link them together.

Task 1 - Bind the IdP and SP Connector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

a. Navigate to :menuselection:`Access --> Federation --> SAML Identity Provider --> Local IdP Services`

    |image1|

b. Check the radio button next to :guilabel:`idp.f5.demo.com`

c. Click on the :guilabel:`Bind/Unbind SP Connectors` button

d. Check the box next to :guilabel:`/Common/app.f5demo.com`

    |image9|

e. Click the :guilabel:`OK` button.


Lab 1.4: Create SAML Resource
-----------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="palegreen"]
         bind [label="Bind Connectors",color="palegreen"]
         resource [label="SAML Resource",color="steelblue1"]
         webtop [label="Webtop"]
         profile [label="Access Profile"]
         vs [label="VS"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

Task 1 - Create SAML Resource
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

a. Navigate to :menuselection:`Access --> Federation --> SAML Resource` and click the :guilabel:`+` sign

   |image10|

b. Configure the following settings:

   ================= ================
   Property          Value     
   ================= ================
   Name              app.f5demo.com 
   SSO Configuration idp.f5demo.com 
   Caption           app       
   ================= ================

   |image11|

c. Click the :guilabel:`Finished` button.



Lab 1.5: Create a Webtop
------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="palegreen"]
         bind [label="Bind Connectors",color="palegreen"]
         resource [label="SAML Resource",color="palegreen"]
         webtop [label="Webtop",color="steelblue1"]
         profile [label="Access Profile"]
         vs [label="VS"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

Task 1 - Create the SAML Webtop
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

a. Navigate to :menuselection:`Access --> Webtops --> Webtop Lists`
b. Click the :guilabel:`+` sign

    |image12|

c. Configure the following settings:

    +-------------------+-------------+
    | Property          | Value       |
    +===================+=============+
    | Name              | saml_webtop |
    +-------------------+-------------+
    | Type              | full        |
    +-------------------+-------------+

    |image13|

3. Click the :guilabel:`Finished` button.



Lab 1.6: Configure the Access Profile
------------------------------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="palegreen"]
         bind [label="Bind Connectors",color="palegreen"]
         resource [label="SAML Resource",color="palegreen"]
         webtop [label="Webtop",color="palegreen"]
         profile [label="Access Profile",color="steelblue1"]
         vs [label="VS"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

The Access Profile defines the characteristics of how we authenticate
and authorize a user using the BIG-IP platform. It controls things like
what type logon page is presented to the user (if any at all), what
language any dialog messages should be presented in, and -- most
importantly -- the flow through which we limit access and assign
resources.

F5 BIG-IP Access Policy Manager supports two types of Access Policies:

1. Per-Session access policies
2. Per-Request access policies

The difference centers around how frequently a policy is evaluated,
either once at time of initial logon or after every single HTTP
request.

Task 1 - Create the Access Profile Object
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

a. Navigate to :menuselection:`Access --> Profiles/Policies --> Access Profiles (Per-Session Policies)`
b. Click the :guilabel:`+` sign

    |image14|

c. Configure the following settings:

    +-------------------+-----------------------+
    | Property          | Value                 |
    +===================+=======================+
    | Name              | idp.f5demo.com-policy |
    +-------------------+-----------------------+
    | Profile Type      | All                   |
    +-------------------+-----------------------+
    | Languages         | English (en)          |
    +-------------------+-----------------------+

    |image15|

    |image16|

d. Click the :guilabel:`Finished` button.

Task 2 - Configure the Access Policy Using the Visual Policy Editor
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Visual Policy Editor (VPE) is where the administrator configures
the heart of the Access Policy. Using a flow chart methodology, it is
easy to create robust policies without adding burdensome management
overhead. Even significant policies can be easily read and understood.

1. Open the Visual Policy Editor
    a. Navigate to :menuselection:`Access --> Profiles/Policies --> Access Profiles (Per-Session Policies)`
    b. Click the :guilabel:`Edit...` link and the VPE will open in a new window

        |image20|

    We'll build a policy like the one below:

        |image17|

2. Add a Logon Page
    a. Click on the :guilabel:`+` link after the :guilabel:`Start` node
    b. Select the :guilabel:`Logon Page` tab and click the :guilabel:`Add Item` button
    c. Use the default settings and click the :guilabel:`Save` button

3. Add an Authentication Mechanism
    a. Click on the :guilabel:`+` link after the :guilabel:`Logon Page` node
    b. Select the :guilabel:`Authentication` tab and select :guilabel:`LocalDB Auth` then click the :guilabel:`Add Item` button
    c. Configure the following settings:

    +-------------------+-----------------------+
    | Property          | Value                 |
    +===================+=======================+
    | LocalDB Instance  | /Common/agility       |
    +-------------------+-----------------------+

    |image18|

      .. NOTE:: The administrator can select from a variety of
         Authentication Mechanisms, including Active Directory and LDAP,
         among others. In this lab, the :guilabel:`LocalDB Auth` has been
         pre-configured.

    d. Click the :guilabel:`Save` button.

4. Add Advanced Resource Assign
    a. Click on the :guilabel:`+` link on the successful branch after the :guilabel:`LocalDB Auth` node
    b. Select the :guilabel:`Assignment` tab and select :guilabel:`Advanced Resource Assign` then click the :guilabel:`Add Item` button
    c. Click the :guilabel:`Add New Entry` button
    d. Click the :guilabel:`Add/Delete` link
    e. Select the :guilabel:`Webtop` tab and select the :guilabel:`/Common/saml_webtop`
    f. Select the :guilabel:`SAML` tab and select the :guilabel:`/Common/app.f5demo.com`
    g. Click the :guilabel:`Update` button, then click the :guilabel:`Save` button


    |image19|

5. Change the ending to Allow
    a. Click on the :guilabel:`Deny` ending after the :guilabel:`Advanced Resource Assign`
    b. Select :guilabel:`Allow`
    c. Click :guilabel:`Save`

6. Apply Policy Changes
    a. Click the :guilabel:`Apply Access Policy` in top left next to the F5 red ball
    b. Close browser tab


    Lab 1.7: Create the Virtual Server
----------------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="palegreen"]
         bind [label="Bind Connectors",color="palegreen"]
         resource [label="SAML Resource",color="palegreen"]
         webtop [label="Webtop",color="palegreen"]
         profile [label="Access Profile",color="palegreen"]
         vs [label="VS",color="steelblue1"]
         test [label="Test"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

In order to access almost anything through an F5 BIG-IP, you must
define a Virtual Server. The Virtual Server listens on the specified
address and handles the requests either by making a load balancing
decision or prompting for a logon (or both!). 

Task 1 - Create the Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

a. Navigate to :menuselection:`Local Traffic --> Virtual Server List`
b. Click the :guilabel:`+` sign

    |image21|

b. Configure the :guilabel:`General Properties` settings:

    =========================== ========================
    General Properties
    ----------------------------------------------------
    Property                    Value
    =========================== ========================
    Name                        idp.f5demo.com
    Destination Address/Mask    10.1.10.101
    Service Port                443
    =========================== ========================

    |image22|

c. Configure the :guilabel:`Configuration` settings:

    =========================== ========================
    Configuration
    ----------------------------------------------------
    Property                    Value
    =========================== ========================
    HTTP Profile                http
    SSL Profile (Client)        idp.f5demo.com-clientssl
    SSL Profile (Server)        serverssl
    =========================== ========================

    |image23|

d. Configure the :guilabel:`Access Policy` settings:

    =========================== ========================
    Access Policy
    ----------------------------------------------------
    Property                    Value
    =========================== ========================
    Access Profile              idp.f5demo.com
    =========================== ========================

    |image24|

e. Click the :guilabel:`Finished` button.



Lab 1.8: Test the SAML Configuration
------------------------------------

.. graphviz::

   digraph breadcrumb {
      rankdir="LR"
      ranksep=.4
      node [fontsize=10,style="rounded,filled",shape=box,color=gray72,margin="0.05,0.05",height=0.1]
      fontsize = 10
      labeljust="l"
      subgraph cluster_provider {
         style = "rounded,filled"
         color = lightgrey
         height = .75
         label = "BIG-IP APM"
         idp [label="IDP",color="palegreen"]
         spconnector [label="SP Connector",color="palegreen"]
         bind [label="Bind Connectors",color="palegreen"]
         resource [label="SAML Resource",color="palegreen"]
         webtop [label="Webtop",color="palegreen"]
         profile [label="Access Profile",color="palegreen"]
         vs [label="VS",color="palegreen"]
         test [label="Test",color="steelblue1"]
         idp -> spconnector -> bind -> resource -> webtop -> profile -> vs -> test

      }
   }

Now that we have all the pieces configured, the only thing left is to
test and validate our setup to make sure it's working as expected.

Task 1 - Test SAML IdP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Open Chromium and navigate to https://app.f5demo.com

2. Notice how we've been redirected to the authentication page at https://...

3. Login with the test credentials below:

    =========== ========
    Username    Password
    =========== ========
    alice       agility
    =========== ========
4. You should now see a demo application.  If not, please step back through the configuration and make sure you did not mistype one of the settings

    |image25|

5. Close the Chromium browser


Lab 2.1: Modify the Access Profile 
----------------------------------

Task 1 - Launching the Visual Policy Editor 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to :menuselection:`Access --> Profiles/Policies --> Access
   Profiles (Per-Session Policies)`
#. Click the :guilabel:`Edit...` link
   
   |image20|

Task 2 - Add a LocalDB Query
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Click on the :guilabel:`+` sign after :guilabel:`LocalDB Auth` on the `Successful` branch
#. In the search field type `local`
#. Select :guilabel:`Local Database` and click the :guilabel:`Add Item` button
#. Configure the following settings:

   ======================= ===================
   Property                Value
   ======================= ===================
   LocalDB Instance        /Common/Agility
   ======================= ===================

#. Click the :guilabel:`Add new entry button`
#. Configure the following settings:

   ======================= ======================
   Property                Value
   ======================= ======================
   Action                  read
   Destination             session.localdb.groups
   Source                  groups
   ======================= ======================

#. Click the :guilabel:`Save` button

Task 3 - Modify the Advance Resource Assignment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Click on :guilabel:`Advance Resource Assign`
#. Click on the :guilabel:`change` link

   |image26|

#. Click the :guilabel:`Add Expression` button
#. Configure the following settings:

   ======================= ===================
   Property                Value
   ======================= ===================
   Agent Sel               LocalDB Group Check
   Condition               LocalDB Query
   User is a member of     Sales
   ======================= ===================

#. Click the :guilabel:`Add Expression` button

   |image27|

#. Click the :guilabel:`Finished` button
#. Click the :guilabel:`Save` button
#. Click the :guilabel:`Apply Access Policy` link in top left next to
   the F5 red ball



   Lab 2.2: Test Access Control
----------------------------

Now that you have your IdP configured we need to test it to make sure
it is working as expected.

Task 1 - Test with an Authorized User
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Open Chromium and navigate to https://app.f5demo.com

#. Login with the test credentials

    =========== ========
    Username    Password
    =========== ========
    alice       agility
    =========== ========

#. You should now see a demo application.  

    |image25|

#. Click the user icon in the top right of the app and logout

Task 2 - Test with an Unauthorized User
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Navigate to https://app.f5demo.com (you can click the bookmark)

#. Login with the test credentials 

    =========== ========
    Username    Password
    =========== ========
    john        agility
    =========== ========

#. You should now see an error page since John is not a member of the sales group

    |image28|

8. Close the Chromium browser

.. |image25| image:: /_static/class4/image25.png
.. |image28| image:: /_static/class4/image28.png



.. |image20| image:: /_static/class4/image20.png
.. |image26| image:: /_static/class4/image26.png
.. |image27| image:: /_static/class4/image27.png

.. |image25| image:: /_static/class4/image25.png


.. |image21| image:: /_static/class4/image21.png
.. |image22| image:: /_static/class4/image22.png
.. |image23| image:: /_static/class4/image23.png
.. |image24| image:: /_static/class4/image24.png



.. |image14| image:: /_static/class4/image14.png
.. |image15| image:: /_static/class4/image15.png
.. |image16| image:: /_static/class4/image16.png
.. |image17| image:: /_static/class4/image17.png
.. |image18| image:: /_static/class4/image18.png
.. |image19| image:: /_static/class4/image19.png
.. |image20| image:: /_static/class4/image20.png


.. |image12| image:: /_static/class4/image12.png
.. |image13| image:: /_static/class4/image13.png


.. |image10| image:: /_static/class4/image10.png
.. |image11| image:: /_static/class4/image11.png




.. |image1| image:: /_static/class4/image1.png
.. |image9| image:: /_static/class4/image9.png





.. |image5| image:: /_static/class4/image5.png
.. |image6| image:: /_static/class4/image6.png
.. |image7| image:: /_static/class4/image7.png



.. |image1| image:: /_static/class4/image1.png
.. |image2| image:: /_static/class4/image2.png
.. |image3| image:: /_static/class4/image3.png
.. |image4| image:: /_static/class4/image4.png
