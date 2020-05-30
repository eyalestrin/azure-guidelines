# How to create Windows Virtual Machine and perform login using RDP

## Create Azure VM from the management console

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the left pane, click on "Virtual machines" -> from the main pane, click on "Create Virtual machines" -> select a Windows flavor -> select a deployment model -> choose "Resource Manager" -> click on Create

3. Fill-in the following details:

   + **Name**: Specify here machine hostname

   + **VM disk type**: Select the disk type according to your needs

     For more information and pricing details, see:

     https://azure.microsoft.com/en-us/pricing/details/managed-disks/

   + **User name**: Specify here the username of the administrator of the VM

   + **Password**: Specify here complete password and confirm it

   + **Subscription**: Select an existing Azure subscription

   + **Resource group**: Select either existing or create a new resource group

     For more information, see: 

     https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups

   + **Location:** Select a region close to your location

4. Click OK

5. Choose a size -> select VM type according to your needs

   For more information and pricing, see:

   https://azure.microsoft.com/en-us/pricing/details/virtual-machines/windows/

6. Fill-in the following details:

   + **Availability set**: Select this option in case your virtual machine requires high availability

     For more information, see: 

     https://docs.microsoft.com/en-us/azure/virtual-machines/windows/tutorial-availability-sets

   + **Disk type and managed disks**: Select the settings according to your needs

     For more information and pricing details, see:

     https://azure.microsoft.com/en-us/pricing/details/managed-disks/

   + **Virtual network**: Select a VNet according to your needs

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview

   + **Subnet**: Select the relevant subnet

     For more information, see: 

     https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-subnet

   + **Public IP address**: Leave the default settings

   + **Network security group**: Select Advanced -> select either to create a new network security group or to select an existing network security group

     For more information, see:

     https://docs.microsoft.com/en-us/azure/virtual-network/security-overview

   + **Extensions**: Leave the default settings

   + **Enable auto-shutdown**: Select either off (the virtual machine will remain up and running) or on (and configure automatic shutdown on daily basis)

     For more information, see: 

     https://blogs.msdn.microsoft.com/uk_faculty_connection/2017/09/12/azure-virtual-machine-auto-shutdown/

   + **Monitoring**: Leave the default settings

   + **Register with Azure Active Directory:** Choose either Yes or No

     For more information, see:

     https://docs.microsoft.com/en-us/azure/active-directory-domain-services/active-directory-ds-join-windows-vm-template

   + **Backup:** Choose either Disabled or Enabled

     For more information, see:

     https://docs.microsoft.com/en-us/azure/backup/backup-azure-arm-vms-prepare

7. Click OK

8. Click Create

9. Wait for the machine deployment process to complete

10. From the left pane, click on "Virtual Machines" -> select the newly created virtual machine from the list

11. From the main pane, click on Tags -> add a new tag:

    + **Name**: Specify here Name
    + **Value:** Specify here the hostname of the newly created virtual machine

12. Click on Save

13. From the main pane, click on "Update management"

14. Fill-in the following details:

    + **Location**: Select a region close to your location

    + **Log Analytics workspace**: Choose either an existing or create default workspace

      For more information, see:

      https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace

    + **Automation account subscription**: Select an existing Azure subscription

    + **Automation account**: Choose either an existing account or create a new account

      For more information, see: 

      https://docs.microsoft.com/en-us/azure/automation/automation-quickstart-create-account

15. Click on Enable

16. Close the virtual machine tabs

17. Logoff the Microsoft Azure Portal



## Login to Azure Virtual machine

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the left pane, click on "Virtual machines" -> locate the relevant virtual machine -> click on the machine name -> from the overview page, write down the "Public IP address" (or "DNS name", if configured)

3. Log off the Azure Portal

4. Run Microsoft "Remote Desktop Connection" client

5. On the computer field, specify either the EC2 instance "IPv4 Public IP" or "Public DNS (IPv4)"

6. Click Connect

7. Specify username and password in-order to login to the virtual machine