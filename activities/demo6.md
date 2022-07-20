# User Steps:

* **Create a new Topology with a Fortigate resource connected to L2 switch and using LAG feature for port connectivity (Automation scripts)**
    * When connecting the Fortigate to a L2 switch just select "New VLAN" from the right side panel within the "Topology" page; Velocity will know how to connect the Fortigate to a L2 switch based on the existing "Physical Connections" under the Inventory (otherwise you'll get a "Connection" error) 
    * For LAG feature training click (open in a new window) on "\[demo#6\] Topology 1" below in this activity page and go to the "Topology" page; click "Edit" to open the Topology for editing; click on "VLAN" cloud and check "ID" field in the left side of the page; you can define a custom VLAN ID or you can let Velocity choose a VLAN ID which is not used; Please notice that connection type is "LAG"; this is the indicator that the User wants to build LAG Ports dynamicaly by using mandatory automation tasks and tool scripts 
    * For LAG feature dynamic implementation you'll need to define a LAG connection type. There 3 different LAG connection types: "LAG" - to build LAG ports on the Link (both ends), "LAG_FGT" - to build LAG ports only on Fortigate end and "LAG_SW" - to build LAG ports only on L2 Test switch side. In the Topology page click Edit and select the connection between Fortigate firewall and L2 Test switch (please see snapshot under Imgaes section below)
    * For testing connection type "LAG" please click on "Reservation of \[demo#6\] Topology 1" and go to the "Reservation" page; the VLAN expected configuration is created by the Driver script; Under "Automation" tab you can see the mandatory Startup tasks being executed in real time by viewing the Report; Under "Information" tab you can check when Reservation becomes Active
    * For testing connection types "LAG_FGT" and "LAG_SW" please click on "Reservation of \[demo#6\] Topology 2" and go to the "Reservation" page
    * Check "Automation scripts" and "Mandatory Automation Tasks" sections below for details about LAG feature automation
* **Reserve Topology**  
    * Default Reservation duration is set to 60 minutes
    * If Reservation is successful you should see "Release" button to end Reservation; goto "Topologies/Automation" section below in this activity page 
* **On Reservation Page:**
    * On "Information" tab you should see the Reservation status as Active
    * Goto "Resources" tab and check what Resources were added after the Topology got resolved; you should see Ports and VLAN information per Port   
* **Mandatory Automation Tasks:**
    * Goto "Topologies" section below this activity page and open Startup and Teardown tasks; these are mandatory tasks created by the Admin and configured to be executed at the start and end of each Reservation; execution reports are displayed in real time if you click on "View report" link
    * Startup mandatory task "optionAllDevicesPowerOn.fftc - will "Power On" all Fortigate firewall devices as soon as you hit "Reserve" on the Topology
    * Startup mandatory task "optionSetLagPorts.fftc" - will build LAG ports configuration based on the connection type value from Topology ("LAG", "LAG_FGT" or "LAG_SW"); The User doesn't have to input any parameter for LAG configuration; Auto-Discover is automatically triggered to update Resources ports information; the LAG port is automatically added to the existing VLAN ID from Topology
    * Teardown mandatory task "optionBackupVelocityReservationDetails.fftc" - is used to build a backup archive which is sent to the "Reservation"'s owner (User) email address; the email displays "Reservation" detailed information about Topology, Resources, Ports and VLANs information taken from Velocity as HTML format; it also contains the configuration files from the Devices involved in the Topology and the Topology file as TBML (the TBML file can be imported manually in Velocity)  
    * Teardown mandatory task "optionUnsetLagPorts.fftc" - will destroy LAG configuration from Topology devices and will restore previous port configuration; Auto-Discover is automatically triggered to update Resources ports infomation
    * Teardown mandatory task "optionAllDevicesPowerOff.fftc" - will "Power Off" all Fortigate firewall devices from Topology; if not used in an Active Reservation all Fortigate devices should be powered off
    * **Automation Scripts:**
    * Open the drop-down menu from "Topologies/Automation" section below in this activity page and check existing options; there is a total of 2 scripts available for both topologies - you may notice that all of their names start with "tool(something).fftc" - this notation is used to identify them as scripts which require the User to input parameters values for execution; in contrast all mandatory automation task names start with "option(something).fftc" - indicating that there is no need for the User to input any parameter value
    * While the Reservation is Active the User has the availability to create/dstroy LAG ports configuration on demand; the "tool" scripts apply to a sigle Device and require specific Parameters for execution
    * To build LAG ports on-demand you can try automated script "toolSetLagPorts.fftc" and click on "Run with Options"; the Automation Assets page opens with the script details; go to "Parameters" tab and input values for Parameters ("device_name", "device_port", "sw_mode", "untagged_vlan_id", "tagged_vlan_id" and "po_number"); then click Run and you'll get back to the activity page and can view the script execution report in real time
    * To unset LAG ports on-demand you can try automated script "toolUnsetLagPorts.fftc" and click on "Run with Options"; the Automation Assets page opens with the script details; go to "Parameters" tab and input values for Parameters ("device_name", "device_port", and "po_number") to remove LAG configuration; then click Run and you'll get back to the activity page and can view the script execution report in real time 


# Images:
![Image from file](demo6_1.jpg)
![Image from file](demo6_2.jpg)


