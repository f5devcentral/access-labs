Lab 2: Webtop Publication
============================================

In this lab, we will add a Webtop resource to the Access Policy
created in the previous lab.

Lab Requirements
----------------

Working HTTPS Virtual Server with Access Policy Created in Lab 1 (Lab 1 successfully completed).


Task 1 – Create a Webtop resource
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Expand the **Access** tab from the main menu on the left and navigate
   to **Webtops** > **Webtop Lists**.

#. Click **Create** to create a new Webtop called **lab101-webtop**,
   select Type “\ **Full**\ ”, uncheck “\ **Minmize To Tray**\ ” and
   click **Finished**.

	|image22|



Task 2 – Create Webtop Item
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#. Browse to **Access** > **Webtops >** **Webtop Link** and click the **+ (Plus Symbol)**

#. Complete the following entries.

      - Name: **www.f5.com**
      - Link Type Dropdown: **Application URI**
      - Applicatoin URI : **https://www.f5.com**
      - Application Caption : **www.f5.com**

	|image23|


Task 3 – Add Webtop resource to existing Access Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. Browse to **Access > Profiles/Policies > Access Profiles
   (Per-Session Policies)**, click on **Edit** for **lab101-psp**. A
   new tab should open to the Visual Policy Editor for **lab101-psp**.


#. In between the AD Auth APM Item and the Allow APM item click the + option to add an item.
   
	|image24|

#. Select the **Advanced Resource Assign** object. Click on the "Assignment Tab" and select the "Advanced Resource Assign"
   radio button. Click **Add Item**.

	|image25|

#. Then Click the "Add New Entry" button. 

	|image26|


#. Under the "Expression Section" click the "Add/Delete" button

	|image27|

#. Click on the **Webop Links** tab, and select the radio button for **www.f5.com**.

	|image28|
#. Click on the **Webtop** tab, select the radio button for **lab101-webtop**. Click the **Update** button at the bottom of the screen.

	|image29|


#. Click **Save**.

	|image30|

#. | At the top left of the browser window, click on **Apply Access
     Policy**, then close the tab.


Task 4 – Testing
~~~~~~~~~~~~~~

#. Open a web browser to the virtual server created in the previous lab
   by navigating to **https://server1.acme.com**. You will be presented
   with a Logon page similar to the one from the last lab.

#. Enter the following credentials:

	- Username: **user1**
	- Password: **user1**
	
	|image31|

#. Click **Logon**.

   This will open the APM Webtop landing page that shows the resources you
   are allowed to access. In this lab, we’ve only configured one resource: 
   **www.f5.com**, but you can add as many as you want and they will
   appear on this Webtop page.

   |image32|

.. |image22| image:: media/022.png
.. |image23| image:: media/023.png
.. |image24| image:: media/024.png
.. |image25| image:: media/025.png
.. |image26| image:: media/026.png
.. |image27| image:: media/027.png
.. |image28| image:: media/028.png
.. |image29| image:: media/029.png
.. |image30| image:: media/030.png
.. |image31| image:: media/031.png
.. |image32| image:: media/032.png


