
ADTest Tool
================

In this section we will get familiar with anther CLI utility to assist
in verifying proper authentication and query capabilities to an Active
Directory domain. We need to prepare for this lab by making a quick
change to the BIGIP’s configuration.

**STEP 1**

|image177|

1. Navigate to System > Configuration > Device  DNS

2. Highlight **10.128.10.100** in the DNS Lookup Server List and click
   **Delete**.

3. Also highlight and **Delete** the DNS Search Domain List of
   **agilitylab.com**

4. Click the **Update** button.

The **/usr/local/bin/adtest** utility is a test tool for APM's Active
Directory Module

+---------------------------------------------------------------------+--------------+
| tYPICAL USAGE                                                       |              |
+=====================================================================+==============+
| Auth Test with Administrative username & password (not necessary)   | |image178|   |
+---------------------------------------------------------------------+--------------+
| Auth Test without just username and password                        | |image179|   |
+---------------------------------------------------------------------+--------------+
| Query Test With Administrative username and password                | |image180|   |
+---------------------------------------------------------------------+--------------+

The ADTest tool can help point out potential issues with a BIG-IP’s
configuration or interoperability issues on the server’s side.

+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| COMMON ERRORS                                                                                                                                                                                                                                                  |                                                                                          |
+================================================================================================================================================================================================================================================================+==========================================================================================+
| ERROR: query with '(sAMAccountName=student)' failed in krb5\_get\_init\_creds\_password(): Preauthentication failed, principal name: administrator@agilitylab.com (-1765328360)                                                                                | The cause of this is simply failed administrative credentials while attempting a query   |
|                                                                                                                                                                                                                                                                |                                                                                          |
| **Test done: total tests: 1, success=0, failure=1**                                                                                                                                                                                                            |                                                                                          |
+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+
| ERROR: query with '(sAMAccountName=student)' failed in ldap\_sasl\_interactive\_bind\_s(): Local error, SASL(-1): generic failure: GSSAPI Error: Unspecified GSS failure. Minor code may provide more information (Cannot find KDC for requested realm) (-2)   | The cause of this is typically failed DNS resolution                                     |
|                                                                                                                                                                                                                                                                |                                                                                          |
| **Test done: total tests: 1, success=0, failure=1**                                                                                                                                                                                                            |                                                                                          |
+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------+

Refer to the screen shots below if you need additional information
regarding the options of ADTest.

|image181|

**TEST 1**

|image182|

1. Try logging on to the VIP as a user again after removing the DNS
   entries. You will notice that your logon will likely fail and you
   will receive the following screen.

|image183|

2. Review the session details for this logon session in reports or
   manage sessions. As we can see from the session details the AD Query
   is failing as well as AD Auth

|image184|

3. Now we can test from the console. Open a console/ssh session. Using
   the following command let us first test authentication using the
   ADtest utility. **adtest -t auth -r "agilitylab.com" -u student -w
   password**. What result did you get with that test?

|image185|

4. Now let’s try a query test. **adtest -t query -r "agilitylab.com" -A
   Administrator -W adminpass -u student -w password**. What result was
   returned?

|image186|

5. Go back to the DNS Settings section and re-add the DNS server IP and
   domain. Then re-test the Auth and Query using the ADtest utility.
