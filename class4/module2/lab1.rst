Lab 1: Create a Empty Per-Session Policy
==========================================

Objectives
----------

The lab has a pre-configured test Virtual Server which will be used throughout the lab.  You will the Visual Policy Editor (VPE)
to create and attach a simple Access Profile which performs user authentication.

Lab Requirements
----------------

-  A pre existing virtual server at 10.1.10.101 or https://server1.acme.com

Task 1: Define an Authentication Server
---------------------------------------

Before we can create an access profile, we must create the necessary AAA
server profile for our Active Directory.

#. From the main screen, browse to **Access > Authentication > Active
   Directory**

#. Click **Create** in the upper right-hand corner

#. Configure the new server profile as follows:

	- Name: **lab101-ad-servers**
	- Domain Name: **f5lab.local**
	- Server Connection: **Use Pool**
	- Domain Controller Pool Name: **lab101-ad-pool**
	- IP Address: **10.1.20.7**
	- Hostname: **dc1.f5lab.local**
    - User Name: **admin**
    - Password: **admin**

#. Click **Finished**

	|image1|


Task 2: Create a Simple Access Profile
--------------------------------------

#. Navigate to **Access > Profiles / Policies > Access Profiles (Per-Session Policies)**. Click the **+ (Plus Symbol)**.   
   |image2|


#. In the Name field enter **lab101-psp** and for the Profile Type select **All** from the dropdown.
	 
   |image3|

#. Under “Language Settings”, choose **English** and click the
   “\ **<<**\ “ button to slide over to the “Accepted Languages” column.
   
   |image4|

#. Click **Finished**, which will bring you back to the Access Profiles
   screen.

#. On the Access Profiles screen, click the **Edit** link under the
   Per-Session Policy column. 
   
   |image5|
   
   The Visual Policy Editor (VPE) will open in a new tab.

#. On the VPE page, click the ‘\**+**\’ icon on the “fallback” path,
   to the right of the **Start** object.
   
   |image6|

#. On the popup menu, choose the **Logon Page** radio button under the
   Logon tab and click **Add Item**
   
   |image7|
   
#. Accept the defaults and click **Save**

   |image8|


#. Between the “Logon Page” and “Deny” objects, click the ‘\**+**\’
   icon. 
   
   |image9|
   
#.  Select **AD Auth** found under the **Authentication** tab,
   and click the **Add Item** button.
   
   |image10|

#. Accept the default for the **Name** and in the **Server** drop-down
   menu select the AD server created above:
   **/Common/lab101-ad-servers**, then click **Save**
   
   |image11|

#. On the “Successful” branch between the **AD Auth** and **Deny**
   objects, click on the word **Deny** to change the ending
   
   |image12|

#. Change the “Successful” branch ending to **Allow**, then click **Save**

   |image13|
   
#. The completed policy should now appear like the one below.
   
   |image14|

#. In the upper left-hand corner of the screen, click on the **Apply
   Access Policy** link.
   
    |image15|

#. Close the window using the **Close** button in the upper right-hand. Click **Yes** when asked “Do you want to close this tab?”
  
   |image16|

Task 3: Associate Access Policy to Virtual Servers
--------------------------------------------------

Now that we have created an access policy, we must apply it to the
appropriate virtual server to be able to use it.

1. From the **Local Traffic** menu, navigate to the **Virtual Servers
   List** and click the name of the virtual server created previously:
   **lab101-https**.

2. Scroll down to the “Access Policy” section, then for the “Access
   Profile” dropdown, select **lab101-psp**
   
   |image17|

3. Click **Update** at the bottom of the screen

Task 4: Testing
---------------

Now you are ready to test.

1. Open a new browser window and open the URL for the virtual server
   that has the access policy applied:
   **https://server1.acme.com** 
   You will be presented with a login window
   
   |image18|

2. Enter the following credentials and click **Logon**:
   - Username: **user1**
   - Password: **user1**

   You will see a screen similar to the following:
   
   |image19|


Task 5: Troubleshooting tips
----------------------------

You can view active sessions by navigating Access/Overview/Active Sessions

You will see a screen similar to the following:

Click on the session id for the active session. If the session is active it will show up as a green in the status.

|image20|

Click on the "session ID" next to the active session. Note every session has a unique session id. Associated with it.
This can be used for troubleshooting specific authentication problem.

Once you click on the session id you wll be presented with a screen that is similar to the following.

|image21|

Note that the screen will show all of the log messages associated with the session. This becomes useful if there is a problem authenticating users.

The default log level shows limited "informational" messages but you can enable debug logging in the event that you need to increase the verbositiy of the logging 
on the APM policy. Note you should always turn off debug logging when you are finished with trouble shooting as debug level logging can
generate a lot of messages that will fill up log files and could lead to disk issues in the event that lgging is set to logto the
local Big-IP.

Please review the following support article that details how to enable debug logging.

https://support.f5.com/csp/article/K45423041

Lab 1 is now complete.

.. |image1| image:: media/001.png
.. |image2| image:: media/002.png
.. |image3| image:: media/003.png
.. |image4| image:: media/004.png
.. |image5| image:: media/005.png
.. |image6| image:: media/006.png
.. |image7| image:: media/007.png
.. |image8| image:: media/008.png
.. |image9| image:: media/009.png
.. |image10| image:: media/010.png
.. |image11| image:: media/011.png
.. |image12| image:: media/012.png
.. |image13| image:: media/013.png
.. |image14| image:: media/014.png
.. |image15| image:: media/015.png
.. |image16| image:: media/016.png
.. |image17| image:: media/017.png
.. |image18| image:: media/018.png
.. |image19| image:: media/019.png
.. |image20| image:: media/020.png
.. |image21| image:: media/021.png
