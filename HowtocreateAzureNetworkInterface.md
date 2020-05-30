# How to create Azure Network Interface

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Network interfaces" -> click on "Create network interface" or "Add":

   + **Name:** Specify here a name for the new network interface

   + **Virtual network:** Select an existing VNet from the list

   + **Subnet:** Select an existing subnet from the list

   + **Private IP address assignment:** Leave the default settings

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-ip-addresses-overview-arm

   + **Network security group:** Select either to create a new network security group or to select an existing network security group

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/security-overview

   + **Private IP address (IPv6):** Leave the default settings

   + **Subscription:** Select the relevant subscription name

   + **Resource group:** Select either existing or create a new resource group

     For more information, see:

     https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups

   + **Location:** Select a region close to your location

3. Click on Create

4. Wait for the deployment on the new network interface to complete

5. From the "Network interfaces" window, click on the newly created network interface

6. From the main pane, click on Tags -> add a new tag:

   + **Name:** Specify here Name
   + **Value:** Specify here the name of the newly created network interface

7. Click on Save

8. From the main pane, click on IP configurations -> from the right pane, under Name, select an existing interface:

   + **Public IP address settings:** Select Enable in-case this interface will be internet facing and click to configure required settings -> select an existing public IP address and choose to create a new one

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-public-ip-address

   + **Private IP address settings:** Leave the default settings

9. Click on Save
10. From the main pane, click on DNS servers -> either choose "Inherit from virtual network" or select "Custom" and specify an IP address of a DNS server
11. Click on Save
12. Log off the Microsoft Azure Portal