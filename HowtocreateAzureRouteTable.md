# How to create Azure Route Table

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Route tables" -> click on "Create route table" or "Add":

   + **Name:** Specify here a name for the new route table

   + **Subscription:** Select the relevant subscription name

   + **Resource group:** Select either existing or create a new resource group.

     For more information, see:

     https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups

   + **BGP route propagation:** Leave the default settings (Enabled)

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview#custom-routes

3. Click on Create

4. Wait for the deployment on the new route table to complete

5. From the "Route tables" window, click on the newly created route table

6. From the main pane, click on Tags -> add a new tag:

   + **Name:** Specify here Name
   + **Value:** Specify here the name of the newly created route table

7. Click on Save

8. From the main pane, click on Routes -> click on Add:

   + **Route name:** Specify here a name for the route within the route table

   + **Address prefix:** Specify here the destination IP address CIDR

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview#how-azure-selects-a-route

   + **Next hop type:** Select the relevant type

     For more information, see: 

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview

9. Click on OK

10. From the main pane, click on Subnets -> click on Associate:

    + **Virtual network:** Click to choose an existing VNet
    + **Subnet:** Click to choose an existing subnet

11. Click on OK

12. Wait for the task of subnet association to complete and click on the newly associated subnet

13. From the main pane, click on Network security group

    + **Network security group:** select an existing network security group from the list
    + **Route table:** select an existing route table from the list

14. Click on Save

15. Log off the Microsoft Azure Portal