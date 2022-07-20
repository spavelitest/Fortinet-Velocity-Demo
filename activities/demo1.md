# User Steps:

* **Create a new Topology with a single Fortigate resource added from Velocity Inventory**
    * Goto Library/Topologies page from Velocity top menu and click on "Add" to create a new Topology; select any available Fortigate firewall; make sure to fill in Name, Description and Tags fields for advanced Topology filtering; "Save" Topology 
    * L1 and L2 Inventory Resources are not available to choose from when creating a new Toplogy as they are used dynamically by Velocity when building L1 or L2 connections between Resources
    * Below you can find a sample Topology "\[demo#1\] Topology" that can be used for training purposes; open Topology link in a new tab and click "Edit" if you want to make changes; "Save" Topology after editing 

* **Reserve Topology**  
    * Default Reservation duration is 60 minutes
    * In this activity page click on "Reserve" topology to create a new Reservation; you should see "Release" button to end the Reservation

* **On Reservation Page:**
    * Open Reservation link in a new tab and wait for Reservation to become "Active"; on "Information" tab you should see the Reservation status as "Active" if Reservation is successful
    * Goto Topology tab and click on the Fortigate resource; the Topology page should open
    * Click on Fortigate resource and select "Actions" -> "HTTP"; a new HTTP connection to Fortigate should open in a new window
    * Click on Fortigate resource and select "Sessions" tab located in the left side of the page; inherited sessions tab should display the "console" session; run "console" session to open a new Console connection to Fortigate (console connection type is telnet)
    * Inside the console connection you should see "QuickCalls" menu in the top-left corner of the page; a list of console quickcalls (custom user actions) are implemented and available for use
    * Select "consoleLogin" and "Run Quickcall"; you should automatically connect to Resource via the console connection
    * Now, you can eiter use the console to enter any commands or use some of the avilable quickcalls to perform specific actions (some of the quickcalls require user input parameters) 
    * For example select "getPortSpeed" quickcall and enter port name parameter (e.g. port31) to display port name speed settings inside the console window
    * You may also try to save the Fortigate configuration by selecting "backupConfigTFTP" quickcall; for this Quickcall the User needs to enter "config_name" and "tftp" parameters values
    * Goto TFTP server (currently VDS is configured as TFTP server and can be accessed [here](https://10.210.107.20/tftp)
    * Click on Fortigate resource and select "VBOTS" tab located in the top-left corner of the page; "Power On", "Power Off" and "Power Cycle" user actions list should be available for use (please note that Power On/Off actions are implemented for Fortigate resources only; implementation is based on specific tag "optionPDU" assigned to "Fortigate Firewall" template)
    * For example run vBOT "Power Cycle" and check "Results" tab for the execution report; Click on "View report" to open the "Execution Report" page in a new window (you can check script result and execution messages for detailed information)
* **Mandatory Automation Tasks:**
    * Goto "Topologies" section below this activity page and open Startup and Teardown tasks; these are mandatory tasks created by the Admin and configured to execute at the start and end of each Reservation
    * As soon as you hit "Reserve" on this Topology the mandatory Startup task to "Power On" executes for the Fortigate; Click on "Reservation of \[demo#1\] Topology" and in the Reservation page navigate to "Automation" tab; The script "optionAllDevicesPowerOn.fftc" (configured as mandatory Startup task) execution report can be displayed in real time if you click on "View report"
    * After Reservation is in Active state and Startup task execution is "Passed" you can stop the Reservation from the Reservation page and select "Run Tasks and Stop" option to trigger "Power Off" Teardown task execution; "Automation" tab displays script "optionAllDevicesPowerOff.fftc" (configured as mandatory Teardown task) execution report
    * All Fortigate devices should be Powered Off if they are not used in an active Reservation; these mandatory automated tasks to Power On/Off apply to "Fortigate Firewall" devices only (test switches which are shared among users will not be Powered Off by these automated tasks) 


# Images:
![Image from file](demo1.jpg)
![Image from file](demo1_2.jpg)
