Checking APM Logs
=====================

APM Logs by default show the same information you can get from the
Manage Sessions menu, as well as APM module-specific information.

Access Policy Manager uses syslog-ng to log events. The syslog-ng
utility is an enhanced version of the standard logging utility syslog.

The type of event messages available on the APM are:

+------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Event Messages         | File Location    | Description                                                                                                                                                                                                 |
+========================+==================+=============================================================================================================================================================================================================+
| Access Policy Events   | /var/log/apm     | Access Policy event messages include logs pertinent to access policy, SSO, network access, and web applications. To view access policy events, on the navigation pane, expand System menu and click Logs.   |
+------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Audit Logging          | /var/log/audit   | Audit event messages are those that the APM system logs as a result of changes made to its configuration.                                                                                                   |
+------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

When setting up logging you can customize the logs by designating the
minimum severity level or log level, that you want the system to report
when a type of event occurs. The minimum log level indicates the minimum
severity level at which the system logs that type of event.

.. NOTE::
  Files are rotated daily if their file size exceeds 10MB. Additionally, weekly rotations are enforced if the rotated log file is a week old, regardless whether or not the file exceeds the 10MB threshold.

The **default** log level for the BIG-IP APM access policy log is
**Notice**, which does ***not*** log Session Variables. Setting the
access policy log level to **Informational** or **Debug** will cause the
BIG-IP APM system to log Session Variables, but it will also add
additional system overhead. If you need to log Session Variables on a
production system, F5 recommends setting the access policy log level to
Informational temporarily while performing troubleshooting or debugging.

We need to add some more actions to the APM Profile in the VPE we have
been working with to go along with the next few lab tests.

**STEP 1**

|image130|

1. Open the VPE and add a new AD Query action after the first Message
   Box action by selecting the **+** sign that follows.

|image131|

2. Navigate to the Authentication tab and select the AD Query radial and
   click **Add Item**.

|image132|

3. In the AD Query, use the drop-down dialog box on Server to select the
   **/Common/LAB\_AD\_AAA** server. Click the **Save** button.

|image133|

4. On the top branch following the AD Query action, add another Message
   Box.

Hint: A Message Box can be added by clicking the **+** sign, navigating
to the General Purpose tab and selecting Message Box

|image134|

5. After the second Message Box add the AD Auth action from the
   Authentication tab

Hint: An AD Auth action can be added by clicking the **+** sign,
navigating to the Authentication tab and selecting AD Auth

|image135|

6. In the AD Auth properties window use the server drop-down menu to
   select **/Common/LAB\_AD\_AAA** server.

7. Click the **Save** button.

|image136|

8. Your policy should now look like this

Notice that one the top branch to the AD Query object the line reads
User Primary Group ID is 100 (See graphic in Step 8 above, just after AD
Query). Maybe you do not want to query for that information and would
prefer to delete that branch. You must be ***careful*** in what you
select or do when deleting that branch when you have other actions
following it in the policy or they could be deleted when you do not want
them to be deleted. Here is a trick you can use to preserve the actions
that follow the ad query when you need to delete a branch.

|image137|

9. Just before the second Message Box after the “User Primary Group ID
   is 100” and after the **+** symbol there is a double arrow symbol.
   This will allow us to swap portions of the policy that come after
   that **->>-** double arrow to another location in the VPE policy.

|image138|

10. Click the **->>-** double arrow.

|image139|

11. You will now notice a **vertical arrow** pointing to other locations
    in the VPE where this section highlighted in green can be swapped.

12. Click on the **Vertical Arrow**

|image140|

13. Now click the **AD Query** action in your policy and go to **Branch
    Rules** tab

14. Click the **X** to the right in the gray box for the Branch Rule

15. Click **Save** to save your settings

|image141|

16. Your policy should now look like this. Now you can see how the Swap function can help with moving action objects throughout the VPE

|image142|

17. Click **Apply Access Policy** to save and implement or work

Now let’s see what can be seen in the logs when set at the default
logging level of Notice.

**TEST 1**

|image143|

|image144|

|image145|

1. Review the current Access Policy Logging (Access  Overview  Event
   Logs -> Settings)

2. Select **default-log-setting**, then Click Edit to view settings.

3. Select **Access System Logs**

|image146|

4. Logon to the BIGIP APM console using an SSH client (PuTTY from your
   desktop). Select **agilitylab** > **Load** > **Open**

|image147|

5. Maximize your SSH window to reduce line wrapping when reviewing the
   logs from the CLI.

6. From the CLI prompt, type **tail –f /var/log/apm** and hit **Enter**
   so you can start see the logs being displayed

|image148|

With the SSH console logging, open a browser and access the APM as the
user **student**.

|image149|

7. Notice the logs being produced at the different stages of the users
   session as it first reaches the VIP, then when the user
   authenticates, receives message boxes or other policy actions, and
   then when the user reaches the policy result.

With the ***default logging*** level, there are no session variables
being logged.

In the Next test we will turn up logging to Informational and restart
the user session and then in the last test change logging level to Debug
and notice the differences from Informational and Notice logging levels.

Turning up the heat on Logging
------------------------------

Now let’s test more verbose logging. You can step up from Notice to
Informational and then to Debug if you want to see the differences
yourself. For the purpose of this test though I will jump straight to
Debug. You can use the GUI to make the log level changes to Debug or you
could use the Traffic Management Shell (TMSH) command from the CLI to
adjust the logging.

**STEP 1**

|image150|

1. Change Access Policy log setting to Debug (Access -> Overview  Event
   Logs  Settings, select default-log-setting, then click Edit)

TIP: Make sure you change setting back to Notice when not
troubleshooting. High levels of logging not only consume more disk
space, but also consume other resources, such as CPU, when enabled.

**TEST 2**

|image151|

1. Once you have the logging level increased restart you user session
   with the browser to the APM VIP and walk through the policy message
   boxes and other actions taking note of the additional verbosity in
   the logs you see in the SSH terminal window.

For sake of saving space in this document we will not include the screen
shots showing the Informational and Debug logging messages and allow you
to experience that yourself during your tests.