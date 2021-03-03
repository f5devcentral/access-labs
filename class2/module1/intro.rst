Lab Overview
================


UDF Blueprint
~~~~~~~~~~~~~~

Access Labs & Solutions Version 5

Lab Topology
~~~~~~~~~~~~

|image000|


The following components have been included in your lab environment:

- 2 x F5 BIG-IP VE (v15.1)
- 1 x Windows Jumphost- Server 2016
- 1 x Windows 2016 Server hosting AD, CA, OCSP & DNS
- 1 x Windows 2016 Server hosting IIS
- 1 x Ubuntu 16.04 LTS 
- 1 x Centos 7

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
| BIG-IP1.f5lab.local    | - Management 10.1.1.4   | - admin/admin            |
|                        | - External   10.1.10.4  |                          |
|                        | - Internal   10.1.20.4  |                          |
+------------------------+-------------------------+--------------------------+
| BIG-IP2.f5lab.local    | - Management 10.1.1.5   | - admin/admin            |
|                        | - External   10.1.10.5  |                          |
|                        | - Internal   10.1.20.5  |                          |
+------------------------+-------------------------+--------------------------+
| dc.f5lab.local         | - Management 10.1.1.7   | - admin/admin            |
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