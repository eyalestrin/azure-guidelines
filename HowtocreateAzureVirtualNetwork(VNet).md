# How to create Azure Virtual Network (VNet)

1. Login to the Microsoft Azure Portal:

   https://portal.azure.com/

2. From the upper search field, specify "Virtual Networks"

3. From the main pane, click on "Create virtual network" or "Add":

   + **Name:** Specify a name for the new VNet

   + **Address space:** 10.0.0.0/16

     Note: Replace the address space according to your needs.

     For more information, see:

     https://docs.microsoft.com/en-in/azure/virtual-network/virtual-network-ip-addresses-overview-arm

   + **Subscription:** Select the relevant subscription name

   + **Resource group:** Select either existing or create a new resource group.

     For more information, see:

     https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups

   + **Location:** Select a region close to your location

   + **Subnet:** Select either existing or create a new subnet.

     For more information, see: 

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-subnet

   + **Address range:** 10.0.0.0/24

     Note: Replace the address range according to your needs.

     For more information, see:

     https://docs.microsoft.com/en-in/azure/virtual-network/virtual-network-ip-addresses-overview-arm

   + **DDoS protection:** Leave the default settings (Basic)

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/ddos-protection-overview

   + **Service endpoints:** Leave the default settings (Disabled)

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview

4. Click on Create

5. Wait for the deployment on the new VNet to complete

6. From the "Virtual networks" window, click on the newly created VNet

7. From the main pane, click on Tags -> add a new tag:

   + **Name:** Specify here Name
   + **Value:** Specify here the name of the newly created VNet

8. Click on Save

9. Log off the Microsoft Azure Portal