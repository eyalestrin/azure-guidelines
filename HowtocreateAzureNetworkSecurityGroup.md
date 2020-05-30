# How to create Azure Network Security Group

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Network Security Groups" -> click on "Create network security group" or "Add":

   + **Name:** Specify a name for the new network security group

   + **Subscription:** Select the relevant subscription name

   + **Resource group:** Select either existing or create a new resource group

     For more information, see:

     https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups

   + **Location:** Select a region close to your location

3. Click on Create

4. Wait for the deployment on the new network security group to complete

5. From the "Network Security Groups" window, click on the newly created network security group

6. From the main pane, click on Tags -> add a new tag:

   + **Name:** Specify here Name
   + **Value:** Specify here the name of the newly created network security group

7. Click on Save

8. From the main pane, click on Inbound security rules -> click on Add -> use the example below in-order to create an inbound rule:

   + **Source:** Select IP Address
   + **Source IP addresses/CIDR ranges:** Specify here a static public IP address or your organization public address/CIDR
   + **Source port ranges:** Leave the default
   + **Destination:** Select IP Addresses
   + **Destination IP addresses/CIDR ranges:** Specify here public IP address of an Azure Virtual machine
   + **Destination port ranges:** Specify here 22
   + **Protocol:** TCP
   + **Action:** Allow
   + **Priority:** Leave the default settings
   + **Name:** Specify here a description for the new rule (for example: Inbound SSH access)

9. Click on Add

   For more information about creation of inbound or outbound rules, see:

   https://docs.microsoft.com/en-us/azure/virtual-machines/windows/nsg-quickstart-portal

10. From the main pane, click on Network interfaces -> click on Associate -> select an existing network interface from the list

11. Click on OK

12. From the main pane, click on Subnets -> click on Associate -> select an existing subnet from the list

13. Click on OK

14. Logoff the Microsoft Azure Portal

    