Lab 1: Access Policy Frameworks
=====================================

Objectives
----------
In this lab we will work through the building blocks of Access Policy Manager. Much like the majority of the other modules around LTM they are policy based meaning you are binding a Profile
to the virtual server in question that you want to provide enhanced functionality. In this case those come in the form of Per-Session and Per-Request Policies

Lab Requirements
----------------

-

Task 1: Intro to Per-Session Policy
---------------------------------------
The per-session policy runs when a client initiates a session. (A per-session policy is also known as an access policy.)

Depending on the actions you include in the access policy, it can authenticate the user and perform other actions that populate session variables with data for use throughout the session.



Task 2: Intro to Per-Request Policy
--------------------------------------
The purpose of this lab is to familiarize the Student with Per Request Policies. The F5 Access Policy Manager (APM) provides two types of policies.

Access Policy - The access policy runs when a client initiates a session. Depending on the actions you include in the access policy, it can authenticate the user and perform group or class queries to populate session variables with data for use throughout the session.

Per-Request Policy - After a session starts, a per-request policy runs each time the client makes an HTTP or HTTPS request. A per-request policy can include a subroutine, which starts a subsession. Multiple subsessions can exist at one time. One access policy and one per-request are specified within a virtual server.

It’s important to note that APM first executes a per-session policy when a client attempts to connect to a resource. After the session starts then a per-request policy runs on each HTTP/HTTPS request. Per-Request policies can be utilized in a number of different scenarios; however, in the interest of time this lab will only demonstrate one method of leveraging Per-Request policies



Task 3: Intro to Posture Assessments
-------------------------------------
A device posture check can be used to continuously check the state of a macOS or Windows client. This feature provides asynchronous desktop client posture checking.
Using F5 Access Guard for Mac and Windows, administrators can now include the ability to transmit up-to-date device posture information to Access Policy Manager in a cryptographically signed HTTP header.
With a device posture check, you can check several categories of items on a client machine.

Antivirus
Endpoint State
Firewall
Hard Disk Encryption
Patch Management
Public File Sharing
System Health Agent

You can add these items in a per-request policy using subroutines only. You can configure any subroutine to be checked against the client either periodically, or on every request.
Continuous client checks in a subroutine are supported only on macOS and Windows. Continuous client checks require that the F5 Access Guard service and browser extension be installed, and that the administrator configures the F5 Access Guard configuration file to specify the items to be checked. Refer to the F5 Access Guard Configuration documentation for more information.


Task 4: Example Use Cases
----------------------------

Lab 1 is now complete.
