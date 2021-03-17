SessionDump 
==========================

SessionDump is a command line utility that shows sessions and their
associated session variables (like GUI Reports)

The sessiondump command has sever switches that can be used and you can
further enhance your troubleshooting by additionally using other CLI
utilities like grep to help filter the results to certain information.
As you can see from the examples below, the first command simple
provides all keys to be dumped for any/all user sessions while the
second using grep allows you to filter the output to those associated
with a given username. Refer to the screen shots below if you need
additional detail.

|image152|

This first example uses just the –allkeys switch.

**sessiondump –allkeys**

|image153|

This second example also uses the –allkeys switch. However, it also adds
the \|grep command to search for the “username”

**sessiondump -allkeys \| grep ‘student’**

**STEP 1**

|image154|

1. On the command line, if you still had the tail command showing
   logging then stop that now by typing **CTRL-C**

|image155|

Remember back in previous labs we learned that Session Variables cannot
be displayed in the Reports screens if the User Session is not in an
***Active*** state. Well that is the same with the CLI sessiondump
utility. There must be active sessions through APM in order to dump
details.

2. Once you are at the command prompt again try using the **sessiondump
   –allkeys** command first. Did you receive any data after running the
   command? If not, then why?

|image156|

3. If all your previous sessions have expired then startup and new
   session as a user and logon to APM and click through the message
   boxes.

|image157|

4. Now on the console type: **sessiondump –allkeys.** You should see a
   long list of information.

|image158|

Compare that with running: sessiondump –allkeys \| grep student You
should then only see the lines that had the username you specified in
the command to be returned

Now let us have some fun with using this utility to help with SSO
troubleshooting/validation.

**STEP 2**

|image159|

1. Edit the VPE for the **Agility-Lab-Access-Profile** policy we have
   been working with.

|image160|

2. Add two new actions to the policy after the AD Auth on the successful
   branch.

|image161|

3. First after AD Auth add the SSO Credential Mapping action from the
   Assignment Tab. Click **Add Item**

|image162|

4. Keep the default settings and click **Save**.

|image163|

5. Next add after the SSO Credential Mapping action add a Pool Assign
   action from the Assignment tab.

|image164|

6. In the next window click the **Add\\Delete** link.

|image165|

7. Then select the radio button for **/Common/Agility-Lab-Pool**. Now
   click the **Save** button.

|image166|

8. Then click Apply Access Policy link on top left of page.

**TEST 2**

|image167|

1. Restart a new APM user session. Logon and follow through all the
   policy actions

|image168|

2. This time instead of seeing a browser error you should be getting
   prompted for authentication for a website which is the site being
   hosted on the pool member that we assigned to the policy. Why are we
   getting prompted for authentication though? Did we not add the SSO
   Credential Mapping to the policy as well?

|image169|

3. Let’s use the following command at the console to check if we are
   getting credentials mapped to token variables properly: **sessiondump
   –allkeys \| grep ‘sso**\ ’ You should see two lines that show
   something like this following picture.

If you see the two lines with session.sso.token.last, then we know the
credential mapping is happening and the username should be displayed
accordingly. So what’s missing?

**STEP 3**

|image170|

1. Next go to the Access Policy menu, click on Access ->
   Profiles/Policies -> Access Profiles (Per-Session Policies) .

|image171|

2. In the list of access profiles, click the NAME of your access
   profile, **Agility-LAB-Access-Profile**

|image172|

3. When this page opens, look at the top, there are four tabs, click the
   **SSO / Auth Domains** tab

|image173|

4. On this page, use the drop down menu on the SSO Configuration row to
   select **Agility\_Lab\_SSO\_NTLM**. Then click Update

|image174|

5. Then click **Apply Access Policy** on the top left of the page and
   apply the policy on the next page.

**TEST 3**

|image175|

1. Restart your user session again to the VIP and logon and click
   through the actions.

If necessary, you can kill your existing session by navigating to Access
Policy  Manage Sessions, then select the user/session and Click Kill
Selected Sessions

|image176|

2. Now what do you see when the policy has completed? Are you seeing the
   web application without being prompted for an additional logon prompt
   from the application? If so, then you were successful.