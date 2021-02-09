Lab 1: Access Policy Frameworks
=====================================

Objectives
----------
Understand Access Policy Frameworks


Lab Requirements
----------------

-

Task 1: Intro to Per-Session Policy
---------------------------------------




Task 2: Intro to Per-Request Policy
--------------------------------------
The purpose of this lab is to familiarize the Student with Per Request Policies. The F5 Access Policy Manager (APM) provides two types of policies.

Access Policy - The access policy runs when a client initiates a session. Depending on the actions you include in the access policy, it can authenticate the user and perform group or class queries to populate session variables with data for use throughout the session.

Per-Request Policy - After a session starts, a per-request policy runs each time the client makes an HTTP or HTTPS request. A per-request policy can include a subroutine, which starts a subsession. Multiple subsessions can exist at one time. One access policy and one per-request are specified within a virtual server.

It’s important to note that APM first executes a per-session policy when a client attempts to connect to a resource. After the session starts then a per-request policy runs on each HTTP/HTTPS request. Per-Request policies can be utilized in a number of different scenarios; however, in the interest of time this lab will only demonstrate one method of leveraging Per-Request policies


Task 3: Example Use Cases
----------------------------



Task 4: Intro to Posture Assessments
-------------------------------------



Lab 1 is now complete.
