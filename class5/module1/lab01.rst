Lab1: The Message Box
=======================

Task 1 - Setup Lab Environment
-----------------------------------

To access your dedicated student lab environment, you will require a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Lab Training Portal. The RDP client will be used to connect to the Jump Host, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumpohost.f5lab.local

   |image001|

#. Select your RDP solution.  

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#. Login with the following credentials:

         - User: **f5lab\\user1**
         - Password: **user1**

#. After successful logon the Chrome browser will auto launch opening the site https://portal.f5lab.local.  This process usually takes 30 seconds after logon.

#. Click the **Classes** tab at the top of the page.

	|image002|


#. Scroll down the page until you see **101 Intro to Access Foundational Concepts** on the left

   |image003|

#. Hover over tile **Visual Policy Editor(VPE) Overview**. A start and stop icon should appear within the tile.  Click the **Play** Button to start the automation to build the environment

   |image004|

#. The screen should refresh displaying the progress of the automation within 30 seconds.  Scroll to the bottom of the automation workflow to ensure all requests succeeded.  If you you experience errors try running the automation a second time or open an issue on the `Access Labs Repo <https://github.com/f5devcentral/access-labs>`__.

   |image005|



Task 2 - 
--------------
Now that we have reviewed/refreshed our memory on VPE conventions lets
edit our policy we were previously working on to add some more actions.
This section we show a great tool for troubleshooting a policy that may
have been reaching an ENDING DENY and closing the APM session too
rapidly for proper inspection during the troubleshooting phase.

**STEP 1**

|image71|

1. Navigate to Access  Access Profiles  Profiles/Policies -> Access
   Profiles (Per-Sessions Policies). Click Edit next to
   **Agility-Lab-Access-Profile** to open the Visual Policy Editor
   (VPE).

|image72|

2. After the Logon Page object, on the fallback branch, click the **+**
   symbol to open the Actions window.

|image73|

3. Click on the **General** **Purpose** tab and then click the radio
   button next to **Message Box** and click the **ADD ITEM** button at
   the bottom of the page.

|image74|

4. Click the **SAVE** button on the next window

|image75|

5. Now client the ending Deny.

|image76|

6. In the pop-up window change it to Allow and click the **SAVE**
   button.

|image77|

7. Then click the Apply Access Policy link at the top left.

**TEST 1**

|image78|

1. Return to the browser or tab you are using for access to
   **https://10.128.10.100**. Restart a new session if necessary.

  -  Username: **student**

  -  Password: **password**

|image79|

2. Did we receive an error this time after the logon page?

3. Did the Message Box display?

|image80|

4. Keep the message box display there and move to the other browser to
   review the Manage Sessions menu.

5. Does the Manage Sessions menu show the Username this time?

6. Is the Status showing a Blue Square or Green Circle? Why?

|image81|

7. Click the session ID to review the details for any new messages.

8. If things worked correctly you should see a message in the details
   stating, “Session deleted due to user inactivity or errors”

|image82|

9. If you look back at the other browser window you should notice a
   Session Expired/Timeout message is being displayed.

**STEP 2**

|image83|

1. Navigate back to Access  Profiles/Policies  Access Profiles
   (Per-Session Policies). Click on **Agility-Lab-Access-Profile**

|image84|

2. Access Policy Timeout from 30 seconds back to **300** seconds by
   removing the check from the custom column.

3. Click the **UPDATE** button at the bottom of the page.

|image85|

4. Click Apply Access Policy link at the top left of the page.

|image86|

5. Finalize the update by confirming the box is checked next to the
   profile and clicking **APPLY ACESS POLICY**

**TEST 2**

|image87|

1. Now go back and restart the user session and logon.

|image88|

2. **Do NOT** click the message box link “Click here to continue”

3. Leave the message box message displayed for the time.

|image89|

4. Go to the other browser/tab and open the Manage Sessions menu.

5. Your session should be there but the Status icon should still be a Blue Square.

6. Click on your Session ID

|image90|

7. Click Built-in Reports

|image91|

8. Click on All Sessions report, then choose Run Report on the pop-up menu.

|image92|

9. Click the Session Variables for your current session.

|image93|

10. Do you now have Session Variables being displayed for this session? If so why?

|image94|

11. Click the All Sessions tab and look at the column labeled Active. Does it show a Y or N in the column?

Note that session variables will only be displayed for Active sessions.
Since you placed a message box in the VPE to pause policy execution the
session is seen as active. This provides you the ability to now review
Session Variables that APM has collected up to this point in the
policies execution.

|image95|

12. Now in the user browser click the link in the Message Box.

If it timed out then restart and this time click through the message box
link.

|image96|

13. Now review the Active Sessions menu and note what icon is shown in the status column. Green Circle finally? Success!!

|image97|

14. If you now click the Session ID you will see that the Policy has reached an ending Allow thus the Access Policy Result is now showing we have been granted LTM+APM\_Mode access.

|image98|

15. Now open the All Sessions report once more to review the Session Variables collected.

|image99|

16. Click the logon folder in the Session Variables page that opens for your session.

|image100|

17. Click the folder icon named *last* to expand its contents.

Notice on the left column labeled Variable Name above and to the right
the next column is Variable Value and the third column is Variable ID.
If you look at the Variable Name of username you will see to the right
its value is recorded as student as you entered it in the logon page.
The next column displays APM’s matching session Variable ID for this
information. You will see that the naming convention follows the session
hierarchy starting with session. then the first folder logon. then the
next folder last. then finally the Variable Name of Username.

We will use some session variables in the next lab to GET and SET
information for the users session.
