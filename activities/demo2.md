# User Steps:

* **Create a new Topology with a single Fortigate resource connected to a Test switch using a single VLAN on a single Port**
    * When connecting the Fortigate to a L2 Inventory Resource just select "New VLAN" from the right side panel within the "Topology" page; Velocity will know how to connect the Fortigate to a L2 switch based on the existing "Physical Connections" under the Inventory (otherwise you'll get a "Connection" error)
    * Below in this activity page you can find a sample Topology (\[demo#2\] Topology 1) that can be used for training purposes
    * Click (open in a new window) on "\[demo#2\] Topology 1" below in this activity page and go to the "Topology" page; click "Edit" to open the Topology for editing; click on "VLAN" cloud and check "ID" field in the left side of the page; you can define a custom VLAN ID or you can let Velocity choose a VLAN ID which is not used; Velocity is selecting the VLAN ID value from the "VLAN ID Set" which is defined for all Test switch resources independently (current set is \[10-1000\] for all Test switches). Change VLAN ID value and save Topology
    * From this activity page click on "Reserve" to start the Reservation; click on "Reservation of \[demo#2\] Topology 1" and go to the "Reservation" page
    * The Test switch "Driver" script is triggered to build the VLAN expected configuration and resolve the Reservation
    * For a single VLAN, Velocity is using tagging "untagged" to identify the request; this translates in sending specific commands through the console connection to create a mode access VLAN (Arista Test switch) or trunk native VLAN (Fortinet Test switch) using the VLAN ID from Topology
* **Create a new Topology with a single Fortigate resource connected to a Test switch using a multiple VLANs on multiple Ports**
    * When connecting the Fortigate to a L2 Inventory Resource just select "New MultiVLAN" from the right side panel within the "Topology" page; Velocity will know how to connect the Fortigate to a L2 switch based on the existing "Physical Connections" under the Inventory (otherwise you'll get a "Connection" error)
    * Below in this activity page you can find a sample Topology (\[demo#2\] Topology 2) that can be used for training purposes
    * Click (open in a new window) on "\[demo#2\] Topology 2" below in this activity page and go to the "Topology" page; click "Edit" to open the Topology for editing; click on "MultiVLAN" cloud and check "MultiVLAN Ports" panel in the left side of the page; click on "View port properties" to check the current definition for the "untagged" and "tagged" VLAN IDs values (please note that Port1 and Port2 have different VLAN ID sets)
    * Change VLAN IDs values and save Topology
    * From this activity page click on "Reserve" to start the Reservation; click on "Reservation of \[demo#2\] Topology 2" and go to the "Reservation" page
    * The Test switch "Driver" script is triggered to build the VLAN expected configuration and resolve the Reservation
    * For multiple VLANs, Velocity is using both "tagged" and "untagged" tagging to identify the request; this translates in sending specific commands through the console connection to create trunk native VLAN (for tagging "untagged") and trunk allowed-vlans (for tagging "tagged") using the VLAN IDs from Topology
* **Reserve Topology**  
    * Default Reservation duration is set to 15 minutes
    * If Reservation is successful you should see "Release" button to end Reservation; goto "Reservation" page
* **On Reservation Page:**
    * On "Information" tab you should see the Reservation status as Active
    * Goto "Resources" tab and check what Resources were added after the Topology got resolved; you should see Ports information from the Test switch and VLAN information per Port
    * If multiple VLANs are expected go to the "Topology" tab and check that "MultiVLAN" cloud is coloured in "green" meaning that VLAN configuration created by the "Driver" script was successful; you can select "MultiVLAN cloud" and validate VLAN IDs definition from "MultiVLAN Ports" panel
    * Goto "Automation" tab to see the configured mandatory automated tasks
* **Mandatory Automation Tasks:**
    * Goto "Topologies" section below this activity page and open Startup and Teardown tasks; these are mandatory tasks created by the Admin and configured to execute at the start and end of each Reservation
    * As soon as you hit "Reserve" on this Topology the mandatory Startup task to "Power On" executes for the Fortigate; Click on "Reservation of \[demo#1\] Topology" and in the Reservation page navigate to "Automation" tab; The script "optionAllDevicesPowerOn.fftc" (configured as mandatory Startup task) execution report can be displayed in real time if you click on "View report"
    * After Reservation is in Active state and Startup task execution is "Passed" you can stop the Reservation from the Reservation page and select "Run Tasks and Stop" option to trigger the "Driver" script (for cleanup the VLAN configuration), and the "Backup" and "Power Off" Teardown tasks execution; "Automation" tab displays scripts execution reports in real time
    * The "Backup" script "optionBackupVelocityReservationDetails.fftc" configured as mandatory Teardown task is creating a backup archive which is sent to the "Reservation"'s owner (User) email address; the email displays all "Reservation" detailed information about Topology, Resources, Ports and VLANs taken from Velocity as HTML format and also contains the configuration files from all "Fortigate firewall" and "Test switch" devices from Topology and the Topology file as TBML (The TBML file can be imported manually in Velocity)  
    * Check new email from "velocity@fortinet.com"; backup email sample below under Images section in this activity page 
    * All Fortigate devices should be Powered Off if they are not used in an active Reservation; these mandatory automated tasks to Power On/Off apply to "Fortigate Firewall" devices only (test switches which are shared among users will not be Powered Off by these automated tasks) 


# Images:
![Image from file](demo2.jpg)
![Image from file](demo2_2.jpg)

