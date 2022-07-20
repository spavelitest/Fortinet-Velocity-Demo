# User Steps:

* **Create a new Topology with a single Fortigate resource connected to a L2 Test switch using single/multiple VLAN(s) on single/multiple Port(s)**
    * When connecting the Fortigate to a L2 switch just select "New VLAN"/"New MultiVLAN" from the right side panel within the "Topology" page; Velocity will know how to connect the Fortigate to a L2 switch based on the existing "Physical Connections" under the "Inventory" (otherwise you'll get a "Connection" error)
    * For VLAN feature training there are 2 Topologies available below in this activity page; "\[demo#2\] Topology 1" - for single VLAN ("New VLAN") feature and "\[demo#2\] Topology 2" - for multiple VLANs ("New MultiVLAN") dynamic implementation
    * Open Topology link in a new tab and click "Edit"; click on "VLAN" cloud and check "ID" field in the left side of the page; you can define a custom VLAN ID or you can let Velocity choose a VLAN ID for you; Velocity is selecting the VLAN ID value from the "VLAN ID Set" which is defined for all Test switch resources independently (current set is \[10-1000\] for all Test switches); or click on "MultiVLAN" cloud and check "MultiVLAN Ports" panel in the left side of the page; click on "View port properties" to display the current definition for the "untagged" and "tagged" VLAN IDs values (please see snapshot under Images section below); please notice that Port1 and Port2 can have different VLAN ID sets
    * The L2 Test switch "Driver" script is designed to build the VLAN expected configuration and resolve the Reservation
    * For a single VLAN, Velocity is using tagging "untagged" to identify the request; this translates in sending specific commands through the console connection to create a mode access VLAN (Arista L2 Test switch) or trunk native VLAN (Fortinet L2 Test switch) using the VLAN ID from Topology
    * For multiple VLANs, Velocity is using both "tagged" and "untagged" tagging to identify the request; this translates in sending specific commands through the console connection to create trunk native VLAN (for tagging "untagged") and trunk allowed-vlans (for tagging "tagged") using the VLAN IDs from Topology
    * "Save" Topology after editing

* **Reserve Topology**  
    * Default Reservation duration is set to 15 minutes
    * In this activity page click on "Reserve" topology to create a new Reservation; you should see "Release" button to end the Reservation

* **On Reservation Page:**
    * Open Reservation link in a new tab and wait for Reservation to become "Active"; on "Information" tab you should see the Reservation status as "Active" if Reservation is successful 
    * Goto "Topology" tab and check Driver execution for VLAN configuration; if multiple VLANs are expected check that "New MultiVLAN" cloud is coloured in "green" meaning that VLAN configuration created by the "Driver" script was successful; you can select "MultiVLAN cloud" and validate VLAN IDs definition from "MultiVLAN Ports" panel
    * Goto "Resources" tab and check what Resources were added after the Topology got resolved; you should see Ports and VLAN information per Port 
    * Goto "Automation" tab and check madatory tasks execution reports

* **Mandatory Automation Tasks:**
    * Goto "Topologies" section below this activity page and open Startup and Teardown tasks; these are mandatory tasks created by the Admin and configured to be executed at the start and end of each Reservation; execution reports are displayed in real time if you click on "View report" link
    * Startup mandatory task "optionAllDevicesPowerOn.fftc - will "Power On" all Fortigate firewall devices as soon as you hit "Reserve" on the Topology
    * Teardown mandatory task "optionBackupVelocityReservationDetails.fftc" - is used to build a backup archive which is sent to the "Reservation"'s owner (User) email address; the email displays "Reservation" detailed information about Topology, Resources, Ports and VLANs information taken from Velocity as HTML format; it also contains the configuration files from the Devices involved in the Topology and the Topology file as TBML (the TBML file can be imported manually in Velocity); Expect new email from "velocity@fortinet.com" (please see snapshot under Images section below) 
    * Teardown mandatory task "optionAllDevicesPowerOff.fftc" - will "Power Off" all Fortigate firewall devices from Topology; if not used in an Active Reservation all Fortigate devices should be powered off

# Images:
![Image from file](demo2.jpg)
![Image from file](demo2_2.jpg)

