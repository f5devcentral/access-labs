Kerberos Related Commands
==============================

2.	From the domain-joined client, open a command prompt and issue the “klist” command. Observe if the client has a ticket for the APM VIP. If the client has a ticket, that indicates that the client’s ability to do Kerberos is correct, the browser configuration is likely correct, and the 401 agent in the visual policy is triggering this authentication action. Between each test delete the client’s ticket cache:

klist purge

kinit

KVNO

