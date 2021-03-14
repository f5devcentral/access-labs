Client-side(AAA) Kerberos
============================


APM client side (AAA) Kerberos involves a domain-joined client and an APM VIP. The client must be able to communicate with its KDC and obtain a Kerberos ticket for a resource (the APM VIP), and then pass that Kerberos ticket to the resource. In the following example screenshots, the client is joined to the domain ECHO, which is a child domain of CHARLIE.COM. Please follow the steps below to create this environment:

#.	Ensure that time is correct between the domain controller, client, and BIG-IP.

#.	Create an Active Directory user account. The name in this user account does not matter. For the purposes of this example, let’s call this user “krbtsvc”. 

#.	Ensure that Active Directory DNS contains a reverse zone for the IP subnet you’ll be using.

#.	Create an entry in local Active Directory DNS to map the APM VIP’s IP to a given host name. This will be the name that the client types in the address bar of the web browser. The name does not have to match the local domain name, but you’ll need to create a new DNS zone if it does not. Check the “Create associated pointer (PTR) record” checkbox to automatically create a PTR record for this DNS entry. For the purposes of this example, let’s create a new DNS zone called “kerberosiscool.com”, and then add a new A record for “www”. Ensure that the client can then resolve “www.kerberosiscool.com”.

#.	From the domain controller, open a command prompt and issue a ktpass command to export a keytab for this user account.

    ktpass –princ HTTP/www.kerberosiscool.com@ECHO.CHARLIE.COM –mapuser echo\krbtsvc –ptype KRB5_NT_PRINCIPAL –pass ‘password!1’ –out c:\out.keytab

    ..note::

    - princ is the arbitrary principal name that will match the fully qualified name that the client browser will request a Kerberos ticket for. Be sure to include the uppercase domain (realm) name at the end of this string.
    - mapuser is the user account that the above service principal name will be applied to.
    -ptype is the principal type. There are a few to choose from, but KRB5_NT_PRINCIPAL is the most semantically correct.
    -pass is the password for the above user account. Put it in single quotes to avoid any issues with special characters.
    -out is the location to create the new keytab file.

     If successful it will export a keytab file to the specified location.


#.	In the BIG-IP management GUI, navigate to Access Policy – AAA – Kerberos. You’re now going to create a new Kerberos AAA profile. In this profile, specify the fully qualified domain name of the Active Directory (all uppercase), and the specify “HTTP” as the service name. Select the previously-created keytab file and then click Finish. 
 
#.	For the purposes of this lab, the AAA access policy can be very simple. Create a typical access profile and then open the visual policy editor. Create a 401 Response agent. By default this agent creates branches for Basic, Negotiate, and fallback conditions. You can simplify this by removing the Basic branch and setting the HTTP Auth Level to “Negotiate”. After the Negotiate branch of the 401 agent, add a Kerberos Auth agent.
 
#.	Inside the Kerberos Auth agent, select the previously-created Kerberos AAA profile. Finish the policy with an Allow block.
 
#.	Assign this access policy to a virtual server. This is client side APM Kerberos, so the service behind the BIG-IP need not require any authentication. Test access from the domain-joined client. Your first attempt will likely result in a popup authentication dialog in the browser. This will likely be because the client is not allowed to perform domain authentication with this server. For Internet Explorer, go to Tools – Internet Options. Go to the Security tab and select Local intranet and click the Sites button.
 
#.	Click the Advanced button.
 
#.	Add the website URL to the Local intranet sites list. Close these dialogs, close and re-open the browser, and test again.

#. If you’re able to access the website, then client side (AAA) APM Kerberos has been successfully configured and the lab is complete. If you take a look at the domain-joined client’s key list, you should notice (at the very least) a ticket for the KDC (krbtgt/REALM), and a ticket for the AAA VIP’s service principal name.
 



