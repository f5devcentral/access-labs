Lab 3: Add a Webtop link to an existing Webtop
==============================================


In this lab your will learn about the API calls necessary to modify an existing webtop by adding a new link to the Access Policy .  The Graphic below depicts the basic flow required for modifing policy via API.

    |image100|


Task 1 - Import Postman Collections
-----------------------------------------------------------------------

#. From the Jumpbox, open **Postman** via the desktop shortcut or toolbar at the bottom

    |image001|

#. Click **Yes** if prompted for "Do you want to allow this app to make changes to your device?"

    |image002|

#. Click **Import** located on the top left of the Postman application

    |image003|

#.  Click **Upload Files** 

    |image004|

#. Navigate to C:\\access-labs\\class4\\module2\\student_files, select **student-class4-module2-lab3.postman_collection.json**, and click **Open**

    |image005|

#.  Click **Import**

    |image006|

#. A collection called **student-class4-module2-lab3** will appear on the left side in Postman


Task 2 - Create A Webtop Policy
-----------------------------------------------------------------------

#.  Hover over the Collection name **student-class4-module2-lab3** with your mouse and click the **Arrow** icon.

    |image007|

#. Click the **Create Policy** folder. You will see two subfolders in the folder.

    |image008|

#.  Click the blue **Run**  button and Postman Runner will open.

    |image009|

#. Click the blue button **Run student-class...** and the API requests will start being sent to the BIG-IP.

    |image010|

#. The **Pass** circle will display a value 10.   
    
    |image011|

#. Open a browser and navigate to https://bigip1.f5lab.local

#. Login to the BIG-IP GUI with the following credentials:
        - Username: **admin**
        - Password: **admin**

#. Navigate to Access>>Profiles/Policies>>Access Profiles (Per-Session Policies).  Do not click the plus symbol.

    |image012|

#. The policy **class4-module2-lab3-psp** you created via automation is displayed.  Click **Edit** to view the policy in Visual Policy Editor(VPE).

    |image013|

#. The policy was successfully deployed using SAML Authenticaiton and an Advanced Resource Assign. Click on the **Advanced Resource Assign** Policy Item.

    |image014|

#. The Advanced Resource Assign contains a webtop and a single webtop link.  

    |image015|


Task 3 - Create a Webtop Link 
-----------------------------------------------------------------------

#. Expand the **student-class4-module2-lab3** collection, **Modify Policy Folder** folder, and then the Webtop Link subfolder. 

    |image016|

#. Click the request **bigip-create-customization group-resource** and then **Body**.  The body of this request specifies that we will be creating a webtop link resource.  One thing to note, all webtop link resources use "/Common/standard" as the source type evern if the policy is using "/Common/Modern".

    |image017|

#. Click the blue **send** button in the upper right corner.  You will receive a 200 OK status code with a response body.  This is an indication that the customization group was created.

    |image018|

#. Click the request **bigip-create-webtop-link** and then **Body**.  The body of this request creates the webtop link Resource.  The applicationUri JSON key contains the resource destination.  The Postman Variable ((DNS3_NAME)) is set to server2.acme.com   

    |image019|

#. Click the blue **send** button in the upper right corner.  You will receive a 200 OK status code with a response body.  This is an indication that the webtop link resource was created.

    |image020|

Task 4 - Add a webtop to an Advanced Resource Assign
-----------------------------------------------------------------------

    .. note::  When creating or modifying a policy it must be performed within a transaction.  A transaction occurs in multiple steps.  First, you create the transation by receiving a transaction ID from the BIG-IP.  Next, you pass subsequent configuration requests that contain the transaction ID header to the BIG-IP.  The BIG-IP does not process these requests.  Instead it holds those requests until the transaction is commited in the final step.  It's important to understand that transactions have an all or nothing approach.  Either every request in the transaction is process sucessfully or none of the configuration changes are made.  This is extremely important to ensure all the required information is there for building a working policy. To understand more about transactions please review XXXXXX.

#.  Since this policy change only requires the addition of a single we will only review the single request.   Click **bigip-create-agent-adv resource assign** and then **Body**.

#.  Notice the request method is a PATCH because the advanced resource assign agent exists.  We do not want to create the agent, but modify an existing agent.

#.  




.. |image001| image:: media/lab03/001.png
.. |image002| image:: media/lab03/002.png
.. |image003| image:: media/lab03/003.png
.. |image004| image:: media/lab03/004.png
.. |image005| image:: media/lab03/005.png
.. |image006| image:: media/lab03/006.png
.. |image007| image:: media/lab03/007.png
.. |image008| image:: media/lab03/008.png
.. |image009| image:: media/lab03/009.png
.. |image010| image:: media/lab03/010.png
.. |image011| image:: media/lab03/011.png
.. |image012| image:: media/lab03/012.png
.. |image013| image:: media/lab03/013.png
.. |image014| image:: media/lab03/014.png
.. |image015| image:: media/lab03/015.png
.. |image016| image:: media/lab03/016.png
.. |image017| image:: media/lab03/017.png
.. |image018| image:: media/lab03/018.png
.. |image019| image:: media/lab03/019.png
.. |image020| image:: media/lab03/020.png
.. |image021| image:: media/lab03/021.png
.. |image022| image:: media/lab03/022.png
.. |image023| image:: media/lab03/023.png
.. |image024| image:: media/lab03/024.png
.. |image025| image:: media/lab03/025.png
.. |image026| image:: media/lab03/026.png
.. |image027| image:: media/lab03/027.png
.. |image028| image:: media/lab03/028.png
.. |image029| image:: media/lab03/029.png
.. |image030| image:: media/lab03/030.png
.. |image031| image:: media/lab03/031.png
.. |image032| image:: media/lab03/032.png
.. |image033| image:: media/lab03/033.png
.. |image100| image:: media/lab03/100.png

