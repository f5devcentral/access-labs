 Server-Side(SSO) Kerberos 
 =============================

APM server side (SSO) Kerberos involves a non-domain (external) client and an APM VIP. The APM VIP contains a Kerberos SSO profile that will request a Kerberos ticket to the target resource on the client’s behalf (S4U2Self and S4U2Proxy). In the following example screenshots, the target resource is an IIS server in the ECHO domain, which is a child domain of CHARLIE.COM. For this lab, all communications will be direct to the ECHO domain, so no cross-domain authentication is necessary. Please follow the steps below to create this environment:
#.	Ensure that time is correct between the domain controller, client, and BIG-IP.

#.	Create an Active Directory user account. In this case, the user logon name will be formatted as an arbitrary and unique service principal name. In this example, we’ll use the value “host/krbsso.echo.charlie.com” for the user logon name and simply “krbsso” for the pre-Windows 2000 (sAMAccountName).

#.	Once created, edit the account’s servicePrincipalName attribute. If the Attribute Editor tab is not available in the account properties, in the tree section of the Active Directory Users and Computers MMC, right click, select View, and then select Advanced Features. Open the account’s properties again, go to the Attribute Editor tab, scroll down to the servicePrincipalName attribute, and enter the SAME service principal name used in the user logon name field when you created the account.
 
    You can also use the “setspn” command line tool to assign the service principal name:
    setspn –a host/krbsso.echo.charlie.com ECHO\krbsso
    where:
    -a indicates to add
    host/krbsso.echo.charlie.com is the new service principal name
    ECHO\krbsso is the account to assign this service principal name to

 
#.	Close and re-open the account’s properties. By virtue of the existence of the service principal name, the account will now have a Delegation tab. Open this tab and apply the following settings:

    Select the “Trust this user for delegation to specified services only” option. This enables Kerberos constrained delegation and S4U2Proxy.

    Select the “Use any authentication protocol” option. This enables Kerberos protocol transition.

    Click the add button and find the http service principal name of the target resource.

 
 
#.	Create an APM Kerberos SSO profile. Assign the Kerberos Realm value as the uppercase fully qualified Active Directory domain name. In the Account Name field, enter the SAME service principal name used in the creation of the AD delegation account. Finally, make note of the two “Source” session variables. Kerberos SSO requires these two input values – a valid domain user name and the domain name. If you do not specify the domain name in the access policy, the defined Kerberos Realm value will be used. This session variable will become exceedingly important when configuring cross-domain authentication.
 
 
#.	Create an APM access policy and assign the Kerberos SSO profile to it. For the purposes of this lab, client side authentication is not required. In fact, Kerberos SSO only requires the two source session variables as inputs. How those variables are populated does not really matter. We’re going to create a very simple access policy.

 

    Inside the visual policy we’ll simply add a Variable Assignment agent and statically assign the username and domain session variables needed by Kerberos SSO.
    
    The purpose of this configuration is to directly test server side Kerberos SSO. The final policy will no doubt contain some form of client side authentication and some mechanism to appropriately populate the required SSO session variables. This is, however, a very good way to troubleshoot server side Kerberos.

#.	For this lab, the SSO profile will be deriving the target service’s service principal name from a reverse DNS lookup of the LTM pool IP address. Ensure that Active Directory DNS has a reverse DNS zone, that the target service has a PTR record that matches the host server’s name, and that the BIG-IP is configured to use Active Director for DNS queries. To validate this, from the BIG-IP command line shell, perform forward and reverse DNS lookups (nslookup or dig) of the fully qualified domain name, and of the target service’s host name and IP address.
 
#.	Ensure that the target service will indeed accept a Kerberos ticket. For this lab, configure the authentication properties of the IIS server for Windows Authentication. Disable Anonymous authentication.

 

    To test this locally, from a domain-joined Windows machine, attempt to access the target service from an Internet Explorer browser. For example, if the IIS server’s host name is echosrv1.echo.charlie.com, then the browser URL request should point to http://echosrv1.echo.charlie.com. You will need to add this URL to the browser’s Trusted Intranet sites list to enable it to pass a Kerberos ticket. This is also a good first step in troubleshooting Kerberos SSO. If the IIS server cannot accept Kerberos tickets, and/or local domain-joined clients cannot authenticate to it via Kerberos, then APM Kerberos SSO will not work either.

 
#.	Create a pool that contains the IP address and port of the target service, add this pool, the access policy, and any other required settings to a new LTM virtual server, and test external access. The provided test page will indicate the name of the user (ex. bob.user) and the authentication type (Negotiate).
 
 
