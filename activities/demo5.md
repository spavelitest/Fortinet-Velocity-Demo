# User Steps:

* **Create a new Topology with a Fortigate resource connected to L2 switch and use Port Speed and Port Split options (Automation scripts)**
    * When connecting the Fortigate to a L2 switch just select "New VLAN" from the right side panel within the "Topology" page; Velocity will know how to connect the Fortigate to a L2 switch based on the existing "Physical Connections" under the Inventory (otherwise you'll get a "Connection" error) 
    * Click (open in a new window) on "\[demo#5\] Topology 1" below in this activity page and go to the "Topology" page; click "Edit" to open the Topology for editing; click on "VLAN" cloud and check "ID" field in the left side of the page; you can define a custom VLAN ID or you can let Velocity choose a VLAN ID which is not used. Change VLAN ID value and save Topology
    * From this activity page click on "Reserve" to start the Reservation; click on "Reservation of \[demo#5\] Topology 1" and go to the "Reservation" page; the VLAN expected configuration is created by the Driver script; Under "Automation" tab you can see the mandatory Startup tasks being executed in real time by viewing the Report; Under "Information" tab you can check when Reservation becomes Active
    * After Reservation becomes Active you may want to perform a "set" Port Speed and/or "set/unset" Port Split actions; Below in this activity page you can find "Automation scripts" section for more details (please see snapshot below under Images section)
* **Reserve Topology**  
    * Default Reservation duration is set to 60 minutes
    * If Reservation is successful you should see "Release" button to end Reservation; goto "Topologies/Automation" section below in this activity page 
* **On Reservation Page:**
    * On "Information" tab you should see the Reservation status as Active
    * Goto "Resources" tab and check what Resources were added after the Topology got resolved; you should see Ports and VLAN information per Port
* **Automation Scripts:**
    * Open the drop-down menu from "Topologies/Automation" section below in this activity page and check existing options; there are 4 scripts available - you may notice that all of their names start with "tool(something).fftc" - this notation is used to identify them as scripts which require the User to input parameters values for execution; in contrast all mandatory automation task names start with "option(something).fftc" - indicating that there is no need for the User to input any parameter value
    * For "Port Speed" actions you should try automated script "toolSetPortSpeed.fftc" and click on "Run with Options"; the Automation Assets page opens with the script details; go to "Parameters" tab and input values for required Parameters ("device_name", "device_port" and "port_speed"); then click Run and you'll get back to the activity page and can view the script execution report in real time (please see snapshot below under Images)
    * "Port Speed" script execution triggers an Auto-Discover so that Ports information gets updated in Velocity; you can go and check Resource Port Speed property from Inventory (please see snapshot below under Images) 
* **Mandatory Automation Tasks:**
    * Goto "Topologies" section below this activity page and open Startup and Teardown tasks; these are mandatory tasks created by the Admin and configured to execute at the start and end of each Reservation
    * As soon as you hit "Reserve" on this Topology the mandatory Startup task to "Power On" executes for the Fortigate; Click on "Reservation of \[demo#4\] Topology 1" and in the Reservation page navigate to "Automation" tab; The script "optionAllDevicesPowerOn.fftc" (configured as mandatory Startup task) execution report can be displayed in real time if you click on "View report"
    * Startup task "optionSetMgmtIpAddr.fftc" will be executed ONLY IF property "Dynamic ipAddress" of the Fortigate is set to "yes" (by default "Dynamic ipAddress" resource property is set to "no"); Only Fortigate devices have this property and you'll need to "Edit" the Fortigate resource before you reserve the Topology and the startup task execution starts; Auto-Discover will update the new ipAddress property of the Fortigate
    * The "Backup" script "optionBackupVelocityReservationDetails.fftc" configured as mandatory Teardown task is creating a backup archive which is sent to the "Reservation"'s owner (User) email address; the email displays all "Reservation" detailed information about Topology, Resources, Ports and VLANs taken from Velocity as HTML format and also contains the configuration files from all "Fortigate firewall" and "Management switch" devices from Topology and the Topology file as TBML (The TBML file can be imported manually in Velocity)  
    * Expect new email from "velocity@fortinet.com" and check the new assigned management ipAddress for the Fortigate resource
    * Teardown task "optionRestoreDefaultMgmtIpAddr.fftc" will bring back the default Management ipAddress on the Fortigate based on the resource unique "Name" property; Auto-Discover is triggered again to update the default ipAddress and default VLAN configuration on the Management switch (default management VLAN ID is "1020")
    * All Fortigate devices should be Powered Off if they are not used in an active Reservation; these mandatory automated tasks to Power On/Off apply to "Fortigate Firewall" devices only (test switches which are shared among users will not be Powered Off by these automated tasks) 


# Images:
![Image from file](demo5_1.jpg)
![Image from file](demo5_2.jpg)
![Image from file](demo5_3.jpg)

