ldifde 
=============



From the Windows domain controller, issue an ldifde command to dump the current KVNO value for the account:
ldifde -f c:\spn.out -d "DC=ECHO,DC=CHARLIE,DC=com" -l *,msDS-KeyVersionNumber -r "(serviceprincipalname=HTTP/www.kerberosiscool*)" -p subtree
where:
-f is the name of the output file
-d is the distinguishedName of the domain
-l is the list of attributes to collect
-r is the LDAP search filter
-p is the LDAP search scope
Look for "msDS-KeyVersionNumber" string in the output file.

From the BIG-IP, issue the klist command against the stored keytab file:
klist –ekt <path the keytab file>
where:
-e indicates to show the encryption type
-k indicates to show keys held in a keytab file (vs. local cache)
-t indicates to show the entry timestamp for each keytab
 