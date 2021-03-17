iRule Logging 
================

As many know one of the most useful features of F5 BIGIP TMOS is the
flexibility provided by iRules.

With APM and iRules you can accomplish many things, in fact you can now
use iRules to create APM sessions. We are not going to go over that here
however for the purpose of how iRules can be used for troubleshooting we
will provide some highlights.

Often you can run into problems wherein an application single sign-on is
not being processed and completing as it should. What happens as a
result of the initial setup not working im/_static/class4tely is that many people
start second guessing what is happening as traffic passes from the
clients browser, to the front client side of the BIGIP VIP, then what F5
VIP is actually able to SEE, next What does LTM see, APM see, what is
being passed along the way at each stage of the transaction through the
BIGIP, and of course what does the BIGIP APM then forward to the Backend
Server Application and How does that Backend Server Application respond?
Fortunately, iRules can be very beneficial in this process to collect
and subsequently log specific data at each stage which greatly enhances
the troubleshooting capabilities.

We all know that TCPDump can be your friend in capturing data to analyze
however at times the application workflows between client f5 and server
and encryption along the way can hamper what TCPDump could capture for
analysis. Another issue with TCPDump is that is captures a lot of data
that then needs to be analyzed. Granted TCPDump provides a filtering
capability to weed through that extra data however when you compare it
to using some targeted iRules to collect APM session variables and data
to be output to logs it makes it easier to review the application flow
more specific to the steps you are trying to validate.

By default, APM in the current code release automatically secures that
variables that are entered into the logon page on APM. Furthermore, the
password is hidden from the reports screen session variable view and
hidden from the database. Yet there are times when the Admin of the APM
may need to have access to the decrypted password to either verify that
the correct information is being keyed by user, received by APM and sent
from APM to servers. Fortunately, there is a way using an iRule to do
just this for our troubleshooting purpose.

**TEST 1**

1.  First open a console session to the BIGIP.

2.  From the command prompt type: **tail –f /var/log/ltm**

3.  Hit the enter key several times to move the text on the screen up to
    the top so you have a clear screen to start reviewing log data
    during this test.

4.  Now open a browser and access the APM VIP and logon as a user.

5.  When you reach the end of your APM policy take a look at the console
    session and note whether or not the logs provide any details about
    the username or password you just used to logon to APM.

6.  Now in another browser open the APM Admin GUI.

7.  Go to the reports screen and run the All Sessions Report.

8.  Open the Session Variables link for the current session you have
    just started as the user.

9.  Navigate down to the SSO folder and expand it.

10. Review the SSO Token Username and verify it displays the username
    you entered.

11. Review the SSO Token Password and verify it displays the password
    you entered. Or can you?

12. No, you cannot because it is obscured by default.

Next, we will implement an iRule to assist the Admin in verifying what
password is being entered by the user.

An iRule has been created already and supplied for you so you won’t need
to create it yourself you only need to apply it to the Virtual Server
under the Resources Tab.

**STEP 2**

1. Open the properties for the Virtual Server.

2. Click the resources Tab.

3. In the iRules section, click the Manage button.

4. In the right-side box scroll down to find the iRule named
   **Agility-201-Troubleshooting**

5. Highlight the iRule and click the arrow button to move it to the left
   box.

6. Click the finished button.

**TEST 2**

1. Navigate to Manage Sessions and Kill all existing sessions.

2. In the console screen, hit the enter key several times to move any
   existing output up to the top of the window, then enter the following
   command **tail –F /var/log/ltm**

3. In the browser for user session testing, restart the session back to
   the APM VIP and logon with your username and password.

4. Click through to the end of the policy.

5. Now go back to the console session and review the log messages.

6. Do you see the username you entered in the logon page?

7. Do you see the password you entered in the logon page? If you
   answered yes then you were successful. Congratulations!