Getting Started
===================

To access your dedicated student lab environment, you will require a web browser and Remote Desktop Protocol (RDP) client software. The web browser will be used to access the Lab Training Portal. The RDP client will be used to connect to the Jump Host, where you will be able to access the BIG-IP management interfaces (HTTPS, SSH).

#. Click **DEPLOYMENT** located on the top left corner to display the environment

#. Click **ACCESS** next to jumpbox.f5lab.local

|image001|


#. Select your RDP resolution.  

#. The RDP client on your local host establishes a RDP connection to the Jump Host.

#.  login with the following credentials:
         - User: **f5lab\\user1**
         - Password: **user1**

#. Once logged on to the jumphost, you can access BIG-IP1's GUI via Chrome using bookmarks or by typing https://bigip1.f5lab.local

#. Login into the BIG-IP Configuration Utility with the following credentials:
         - User: **admin**
         - Password: **admin**

.. NOTE::
	 All work for this lab will be performed exclusively from the Windows
	 jumphost. No installation or interaction with your local system is
	 required.



UDF Blueprint
~~~~~~~~~~~~~~

Access Labs & Solutions Version 9

Lab Topology
~~~~~~~~~~~~

|image000|


The following components have been included in your lab environment:


.. Note:: BIG-IP2  and BIG-IP6 are offline by default.  Only boot these BIG-IPs when the lab specifies to do so.


- 4 x F5 BIG-IP VE (v16.0)
- 1 x Windows Server 2016 - jumphost.f5lab.local
- 1 x Windows 2016 Server - dc1.f5lab.local (AD, CA, OCSP & internal DNS) 
- 1 x Windows 2016 Server - iis.f5lab.local
- 1 x Centos 7 - web.f5lab.local

Lab Components
^^^^^^^^^^^^^^

The following table lists VLANS, IP Addresses and Credentials for all
components:


+------------------------+-------------------------+--------------------------+
| Component              | VLAN/IP Address(es)     | Credentials              |
+========================+=========================+==========================+
| jumpbox.f5lab.local    | - Management 10.1.1.10  | - user1/user1            |
|                        | - External   10.1.10.10 | - user2/user2            |
|                        | - Internal   10.1.20.10 |                          |
+------------------------+-------------------------+--------------------------+
| bigip1.f5lab.local     | - Management 10.1.1.4   | - admin/admin            |
|                        | - External              |                          |
|                        |     - 10.1.10.4         |                          |
|                        |     - 10.1.10.100       |                          |
|                        |     - 10.1.10.101       |                          |
|                        |     - 10.1.10.102       |                          |
|                        |     - 10.1.10.103       |                          |
|                        |     - 10.1.10.104       |                          |
|                        |     - 10.1.10.105       |                          |
|                        |     - 10.1.10.106       |                          |
|                        |     - 10.1.10.107       |                          |
|                        |     - 10.1.10.108       |                          |
|                        |     - 10.1.10.109       |                          |
|                        |     - 10.1.10.110       |                          |
|                        |     - 10.1.10.111       |                          |
|                        |     - 10.1.10.112       |                          |
|                        |     - 10.1.10.113       |                          |
|                        | - Internal   10.1.20.4  |                          |
+------------------------+-------------------------+--------------------------+
| bigip2.f5lab.local     | - Management 10.1.1.5   | - admin/admin            |
|                        | - External              |                          |
|                        |     - 10.1.10.5         |                          |
|                        |     - 10.1.10.200       |                          |
|                        |     - 10.1.10.201       |                          |
|                        |     - 10.1.10.202       |                          |
|                        |     - 10.1.10.203       |                          |
|                        |     - 10.1.10.204       |                          |
|                        |     - 10.1.10.205       |                          |
|                        |     - 10.1.10.206       |                          |
|                        |     - 10.1.10.207       |                          |
|                        |     - 10.1.10.208       |                          |
|                        |     - 10.1.10.209       |                          |
|                        |     - 10.1.10.210       |                          |
|                        |     - 10.1.10.211       |                          |
|                        |     - 10.1.10.212       |                          |
|                        |     - 10.1.10.213       |                          |
|                        | - Internal   10.1.20.5  |                          |
+------------------------+-------------------------+--------------------------+
| bigip5.f5lab.local     | - Management 10.1.1.11  | - admin/admin            |
|                        | - External              |                          |
|                        |     - 10.1.10.11        |                          |
|                        |     - 10.1.10.99        |                          |
|                        | - Internal              |                          |
|                        |     - 10.1.20.11        |                          |
|                        |     - 10.1.20.99        |                          |
+------------------------+-------------------------+--------------------------+
| bigip6.f5lab.local     | - Management 10.1.1.12  | - admin/admin            |
|                        | - External              |                          |
|                        |     - 10.1.10.12        |                          |
|                        |     - 10.1.10.199       |                          |
|                        | - Internal              |                          |
|                        |     - 10.1.20.12        |                          |
|                        |     - 10.1.20.199       |                          |
+------------------------+-------------------------+--------------------------+
| dc1.f5lab.local        | - Management 10.1.1.7   | - admin/admin            |
|                        | - Internal   10.1.20.7  |                          |
+------------------------+-------------------------+--------------------------+
| dc1.f5lab.local        | - Management 10.1.1.7   | - admin/admin            |
|                        | - Internal   10.1.20.7  |                          |
+------------------------+-------------------------+--------------------------+
| iis.f5lab.local        | - Management 10.1.1.6   | - admin/admin            |
|                        | - Internal              |                          |
|                        |    - 10.1.20.6          |                          |
|                        |    - 10.1.20.16         |                          |
+------------------------+-------------------------+--------------------------+
| web.f5lab.local        | - Management 10.1.1.9   |                          |
|                        | - Internal              |                          |
|                        |    - 10.1.20.9          |                          |
|                        |    - 10.1.20.19         |                          |
+------------------------+-------------------------+--------------------------+
| radius.f5lab.local     | - Management 10.1.1.8   |                          |
|                        | - Internal              |                          |
|                        |    - 10.1.20.8          |                          |
|                        |    - 10.1.20.18         |                          |
+------------------------+-------------------------+--------------------------+

.. |image000| image:: media/intro/000.png
.. |image001| image:: media/intro/001.png


