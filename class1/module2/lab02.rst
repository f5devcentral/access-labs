Lab 2: Portal Resources
=========================

In this lab, we will add a Webtop resource to the Access Policy
created in the previous lab. A full webtop provides an access policy ending for an access policy branch to which you can optionally assign portal access resources, app tunnels, remote desktops, and webtop links, in addition to network access tunnels.
Then, the full webtop provides your clients with a web page on which they can choose resources, including a network access connection to start.


Section 1 - Setup Lab Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Task 1 - Deploy prebuilt objects
-----------------------------------

To access your dedicated student lab environment, you will require a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Lab Training Portal. The RDP client will be used to connect to the Jump Host, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumpohost.f5lab.local

   |image001|

#. Select your RDP resolution.

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#. Login with the following credentials:

         - User: **f5lab\\user1**
         - Password: **user1**

#. After successful logon the Chrome browser will auto launch opening the site https://portal.f5lab.local.  This process usually takes 30 seconds after logon.

#. Click the **Classes** tab at the top of the page.

	|image002|

#. Scroll down the page until you see **102 Webtop Features** on the left

   |image003|

#. Hover over tile **Portal Resources**. A start and stop icon should appear within the tile.  Click the **Play** Button to start the automation to build the environment

   +---------------+-------------+
   | |image004|    | |image005|  |
   +---------------+-------------+

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image006|

Section 2 - Basic Portal Resource
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Task 1 - Create a Webtop 
--------------------------

#. From a browser navigate to https://bigip1.f5lab.local

#. Login with username **admin** and password **admin**

   |image009|


#. Navigate to **Access** >> **Webtops** >> **Webtop Lists** >> click the **Plus Sign(+)**.

   |image010|

#. Enter the Name **full-webtop**
#. From the Type dropdown menu select **Full**
#. Click **Finished**.

   |image011|


Task 2 - Create a portal resource
---------------------------------------

#. Navigate to **Access** >> **Connectivity/VPN** >> **Portal Access Lists** >> click the **Plus Sign(+)**.

   |image012|


#. Enter the Name **files**
#. From the Link Type dropdown menu select **Application URI**
#. Enter the Application URI **http://files-master.f5lab.local**
#. Enter the Caption *files**
#. Click **Create**

   |image013|

Task 3 - Create a Connectivity Profile
---------------------------------------

#. Navigate to **Access** >> **Connectivity/VPN** >> **Connectivity** >>  **Profiles** >>click the **Plus Sign(+)**.

   |image014|


#. Enter the Name **webtop-cp**
#. From the Parent Profile dropdown menu select **/Common/connectivity**
#. Click **OK**

   |image015|

Task 4 - Add new profiles to an existing Virtual Server
---------------------------------------------------------

#. Navigate to **Local Traffic** >> **Virtual Servers** >> **Virtual Server List**

   |image016|

#. Click **webtop-https**

   |image017

#. In Content Rewrite Section, select **rewrite** from the Rewrite Profile dropdown menu.
#. In Access Policy Section, select **webtop-cp** from the Connectivity Profile dropdown menu.
#. Click **Update**

   |image018|

Task 5 - Add a Webtop Resource to an existing Policy
------------------------------------------------------

#. Navigate to **Access** > **Profiles / Policies** > **Access Profiles (Per-Session Policies)**, 

    |image019|

#. Click on **Edit** for **webtop-psp**. 

   |image020|

#. Click the Plus Sign(+) in between the AD Auth policy item and the Allow Terminal .

   |image021|

#. Click on the **Assignment Tab**
#. Select the **Advanced Resource Assign** radio button
#. Click **Add Item**

   |image022|

#. Click the **Add New Entry** button.
#. Click the **Add/Delete** button

   |image023|

#. Click on the **Portal Access** tab
#. Select the radio button for **/Common/files**

   |image024|

#. Click on the **Webtop** tab
#. Select the radio button for **/Common/full-webtop**
#. Click the **Update** button at the bottom of the screen.

   |image025|

#. Click **Save**.

   |image026|

#. At the top left of the browser window, click on **Apply Access Policy**

   |image027|



Task 3 - Test the Configuration
---------------------------------

#. Open a **New Incognito** web browser and navigate to **https://webtop.acme.com**. 
#. Enter the following credentials:

    +-------------+--------------+
    |Username:    |**user1**     |
    +-------------+--------------+
    |Password:    |**user1**     |
    +-------------+--------------+

#. Click **Logon**.

   |image028|


   ..note:: This will open the APM landing page that shows the resources you are allowed to access. In this lab, we've only configured a single resource but you can add as many as you want and they will appear on this Webtop page.

#. Click the **F5** Resource on the webtop

   |image029|

#.  The Files site opens in a new tab,  but notice you are not redirected to http://files.f5lab.local.  Instead you are being reverse proxied to the site through https://webtop.acme.com   

   |image030| 

Section 3 - Lab Cleanup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Task 1 - Run Cleanup automation
---------------------------------

#. From a browser on the jumphost navigate to https://portal.f5lab.local

#. Click the **Classes** tab at the top of the page.

    |image002|

#. Scroll down the page until you see **102 Webtop Features** on the left

   |image003|

#. Hover over tile **Portal Resources**. A start and stop icon should appear within the tile.  Click the **Stop** Button to trigger the automation to remove any prebuilt objects from the environment

    +---------------+-------------+
    | |image004|    | |image007|  |
    +---------------+-------------+


#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image008|

#. This concludes the lab.

   |image000|



.. |image000| image:: ./media/lab01/000.png
.. |image001| image:: ./media/lab01/001.png
.. |image002| image:: ./media/lab01/002.png
.. |image003| image:: ./media/lab01/003.png
.. |image004| image:: ./media/lab01/004.png
.. |image005| image:: ./media/lab01/005.png
.. |image006| image:: ./media/lab01/006.png
.. |image007| image:: ./media/lab01/007.png
.. |image008| image:: ./media/lab01/008.png
.. |image009| image:: ./media/lab01/009.png
.. |image010| image:: ./media/lab01/010.png
.. |image011| image:: ./media/lab01/011.png
.. |image012| image:: ./media/lab01/012.png
.. |image013| image:: ./media/lab01/013.png
.. |image014| image:: ./media/lab01/014.png
.. |image015| image:: ./media/lab01/015.png
.. |image016| image:: ./media/lab01/016.png
.. |image017| image:: ./media/lab01/017.png
.. |image018| image:: ./media/lab01/018.png
.. |image019| image:: ./media/lab01/019.png
.. |image020| image:: ./media/lab01/020.png
.. |image021| image:: ./media/lab01/021.png
.. |image022| image:: ./media/lab01/022.png
.. |image023| image:: ./media/lab01/023.png
.. |image024| image:: ./media/lab01/024.png
.. |image025| image:: ./media/lab01/025.png
.. |image026| image:: ./media/lab01/026.png
.. |image027| image:: ./media/lab01/027.png
.. |image028| image:: ./media/lab01/028.png
.. |image029| image:: ./media/lab01/029.png
.. |image030| image:: ./media/lab01/030.png
.. |image031| image:: ./media/lab01/031.png
.. |image032| image:: ./media/lab01/032.png
.. |image033| image:: ./media/lab01/033.png
.. |image034| image:: ./media/lab01/034.png
.. |image035| image:: ./media/lab01/035.png
.. |image036| image:: ./media/lab01/036.png
.. |image037| image:: ./media/lab01/037.png
.. |image038| image:: ./media/lab01/038.png
.. |image039| image:: ./media/lab01/039.png
.. |image040| image:: ./media/lab01/040.png
.. |image041| image:: ./media/lab01/041.png
.. |image042| image:: ./media/lab01/042.png
.. |image043| image:: ./media/lab01/043.png
.. |image044| image:: ./media/lab01/044.png
.. |image045| image:: ./media/lab01/045.png
.. |image046| image:: ./media/lab01/046.png
.. |image047| image:: ./media/lab01/047.png
.. |image048| image:: ./media/lab01/048.png
.. |image049| image:: ./media/lab01/049.png
.. |image050| image:: ./media/lab01/050.png
.. |image051| image:: ./media/lab01/051.png
.. |image052| image:: ./media/lab01/052.png
.. |image053| image:: ./media/lab01/053.png
.. |image054| image:: ./media/lab01/054.png
.. |image055| image:: ./media/lab01/055.png
.. |image056| image:: ./media/lab01/056.png
.. |image057| image:: ./media/lab01/057.png
.. |image058| image:: ./media/lab01/058.png
.. |image059| image:: ./media/lab01/059.png
.. |image060| image:: ./media/lab01/060.png
.. |image061| image:: ./media/lab01/061.png
.. |image062| image:: ./media/lab01/062.png