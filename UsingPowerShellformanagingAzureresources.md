# Using PowerShell for managing Azure resources

## How to configure PowerShell for managing Azure resources (Windows platform)

 1. Login to the machine using privileged account.

2. Follow the instructions below to install the latest build of PowerShell:

   https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7

3. From command prompt, run the command below to invoke PowerShell:

   `pwsh`

   Note: You need to run cmd.exe or pwsh.exe as administrator.

4. Run the command below to find out the current PowerShell version:

   `$PSVersionTable.PSVersion`

5. In-case you currently have version older than 5.1, follow the article below to locate the download URL for upgrading to the latest version of PowerShell:

   https://docs.microsoft.com/en-us/powershell/scripting/install/migrating-from-windows-powershell-51-to-powershell-7?view=powershell-7

6. Run the command below to install Azure cmdlet for PowerShell:

   `Install-Module -Name Az -AllowClobber -Force`

7. Run the commands below to update to the latest Azure cmdlet for PowerShell:

   `Update-Module -Name Az -Force`

8. To view the installed versions of Az, run the command below:

   `Get-InstalledModule -Name Az | select Name,Version`
   



## How to configure PowerShell for managing Azure resources (RHEL/CentOS platform)

1. Login to the machine using privileged account.

2. Run the command below to register the RedHat 7 or CentOS 7 repository:

   `curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo`

3. Run the command below to install PowerShell:

   `sudo yum install -y powershell`

4. From command prompt, run the command below to invoke PowerShell:

   `sudo pwsh`

5. Run the command below to find out the current PowerShell version:

   `$PSVersionTable.PSVersion`

6. Run the command below to install Azure cmdlet for PowerShell:

   `Install-Module -Name Az -AllowClobber -Force`

7. Run the commands below to update to the latest Azure cmdlet for PowerShell:

   `Update-Module -Name Az -Force`

8. To view the installed versions of Az, run the command below:

   `Get-InstalledModule -Name Az | select Name,Version`
   



## How to configure PowerShell for managing Azure resources (Ubuntu 18.04 platform)

1. Login to the machine using privileged account.

2. Run the command below to register the Ubuntu 18.04 repository:

   `wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb`

   `sudo dpkg -i packages-microsoft-prod.deb`

   `sudo apt-get update`

   `sudo add-apt-repository universe`

3. Run the command below to install PowerShell:

   `sudo apt-get install -y powershell`

4. From command prompt, run the command below to invoke PowerShell:

   `pwsh`

5. Run the command below to find out the current PowerShell version:

   `$PSVersionTable.PSVersion`

6. Run the command below to install Azure cmdlet for PowerShell:

   `Install-Module -Name Az -AllowClobber -Force`

7. Run the commands below to update to the latest Azure cmdlet for PowerShell:

   `Update-Module -Name Az -Force`

8. To view the installed versions of Az, run the command below:

   `Get-InstalledModule -Name Az | select Name,Version`



## How to configure PowerShell for managing Azure resources (Debian 10 platform)

1. Login to the machine using privileged account.

2. Run the command below to register the Debian 10 repository:

   `wget https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb`

   `sudo dpkg -i packages-microsoft-prod.deb`

   `sudo apt-get update`

3. Run the command below to install PowerShell:

   `sudo apt-get install -y powershell`

4. From command prompt, run the command below to invoke PowerShell:

   `pwsh`

5. Run the command below to find out the current PowerShell version:

   `$PSVersionTable.PSVersion`
   
6. Run the command below to install Azure cmdlet for PowerShell:

   `Install-Module -Name Az -AllowClobber -Force`

7. Run the commands below to update to the latest Azure cmdlet for PowerShell:

   `Update-Module -Name Az -Force`

8. To view the installed versions of Az, run the command below:

   `Get-InstalledModule -Name Az | select Name,Version`



## Common PowerShell commands for Azure

+ Login to an Azure account:

  `Connect-AzAccount`

+ List available subscriptions:

  `Get-AzSubscription`

+ Change the context to a specific Azure subscription:

  `Set-AzContext -SubscriptionId <subscription_id>`

  Note: Replace **<subscription_id>** with the relevant subscription ID

+ Run the command below to suppress warning messages:

  `Set-Item Env:\SuppressAzurePowerShellBreakingChangeWarnings "true"`



## Resource group related commands

+ List available resource groups:

  `Get-AzResourceGroup`

+ Create a new Azure resource group:

  `New-AzResourceGroup -Name <ResourceGroup_Name> -Location <Location_>`

  Note 1: Replace **<ResourceGroup_Name>** with your own relevant group name

  Note 2: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Example:

  `New-AzResourceGroup -Name RG01 -Location "West Europe"`



## Networking related commands

+ List available virtual networks:

  `Get-AzVirtualNetwork`

+ List available subnets

  `Get-AzVirtualNetwork -Name <Virtual Network Name> -ResourceGroupName <Resource Group Name> | Get-AzureRmVirtualNetworkSubnetConfig | Format-Table`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Virtual_Network_Name>** with the relevant VNET

  Note 3: Replace **<Resource_Group_Name>** with the relevant resource group name

  Example:

  `Get-AzVirtualNetwork -Name VNET01 -ResourceGroupName RG01 | Get-AzVirtualNetworkSubnetConfig | Format-Table`

+ Create a new virtual network and a new subnet:

  `$subnetConfig = New-AzVirtualNetworkSubnetConfig -Name <SubnetName> -AddressPrefix <Subnet address prefix CIDR>`

  `New-AzVirtualNetwork -ResourceGroupName <Resource Group Name> -Location <Location> -Name <Virtual network name> -AddressPrefix <Virtual network address prefix CIDR> -Subnet $subnetConfig`

  Note 1: The above commands should be written in a single line (for each command)

  Note 2: Replace **<Subnet_Name>** with a relevant subnet name

  Note 3: Replace **<Subnet_address_prefix_CIDR>** with relevant value (see example below)

  Note 4: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 5: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 6: Replace **<Virtual_network_name>** with relevant value (see example below)

  Note 7: Replace **<Virtual_network_address_prefix_CIDR>** with relevant value (see example below)

  Example:

  `$subnetConfig = New-AzVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24`

  `New-AzVirtualNetwork -ResourceGroupName RG01 -Location "UK West" -Name VNET01 -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig`

+ List all available network security groups:

  `Get-AzNetworkSecurityGroup`

+ Create a new network security group:

  `New-AzNetworkSecurityGroup -ResourceGroupName <Resource Group Name> -Location <Location> -Name <Network security group name>`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 3: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 4: Replace **<Network_security_group_name>** with relevant value (see example below)

  Example:

  `New-AzNetworkSecurityGroup -ResourceGroupName RG01 -Location "UK West" -Name myNetworkSecurityGroup`

+ List all available rules inside a network security group:

  `Get-AzNetworkSecurityGroup -ResourceGroupName <Resource Group Name> -Name <Network security group name> | Get-AzNetworkSecurityRuleConfig | Format-Table`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 3: Replace **<Network_security_group_name>** with relevant value (see example below)

  Example:

  `Get-AzNetworkSecurityGroup -ResourceGroupName RG01 -Name myNetworkSecurityGroup | Get-AzNetworkSecurityRuleConfig | Format-Table`

+ Create a new rule inside an existing network security group:

  `$nsgRule = New-AzNetworkSecurityRuleConfig -Name <Security rule name> -Protocol Tcp -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389 -Access Allow`

  `New-AzNetworkSecurityGroup -ResourceGroupName <Resource Group Name> -Location <Location> -Name <Network security group name> -SecurityRules $nsgRule -Force`

  Note 1: The above commands should be written in a single line (for each command)

  Note 2: Replace **<Security_rule_name>** with relevant value (see example below)

  Note 3: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 4: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 5: Replace **<Network_security_group_name>** with relevant value (see example below)

  Example:

  `$nsgRule = New-AzNetworkSecurityRuleConfig -Name AllowRDP -Protocol Tcp -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 3389 -Access Allow`

  `New-AzNetworkSecurityGroup -ResourceGroupName RG01 -Location "West Europe" -Name myNetworkSecurityGroup -SecurityRules $nsgRule –Force`

+ List available public IP addresses assigned to virtual machines:

  `Get-AzPublicIpAddress`



## Virtual machine related commands

+ List available virtual machines in a subscription:

  `Get-AzVM`

+ List available virtual machines in a specific resource group:

  `Get-AzVM -ResourceGroupName <Resource Group Name>`

  Note: Replace **<Resource_Group_Name>** with relevant value

+ Get information about a specific virtual machine inside a resource group:

  `Get-AzVM -ResourceGroupName <Resource group name> -Name <VM Name>`

  Note 1: Replace **<Resource_Group_Name>** with relevant value

  Note 2: Replace **<VM_Name>** with the relevant value

+ Start a virtual machine inside a specific resource group:

  `Start-AzVM -ResourceGroupName <Resource group name> -Name <VM Name>`

  Note 1: Replace **<Resource_Group_Name>** with relevant value

  Note 2: Replace **<VM_Name>** with the relevant value

+ Restart a virtual machine inside a specific resource group:

  `Restart-AzVM -ResourceGroupName <Resource group name> -Name <VM Name>`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Resource_Group_Name>** with relevant value

  Note 3: Replace **<VM_Name>** with the relevant value

+ Stop a virtual machine inside a specific resource group:

  `Stop-AzVM -ResourceGroupName <Resource group name> -Name <VM Name>`

  Note 1: Replace **<Resource_Group_Name>** with relevant value

  Note 2: Replace **<VM_Name>** with the relevant value

+ List available virtual machine sizes for a region:

  `Get-AzVMSize -Location <Location>`

  Note: Replace <Location_> with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

+ List available virtual machine image publishers for a region:

  `Get-AzVMImagePublisher -Location <Location>`

  Note: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

+ List available offer types for a publisher (such as Vendor)

  `Get-AzVMImageOffer -Location <Location> -PublisherName <Publisher Name>`

  Note 1: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 2: Replace **<Publisher_Name>** with a relevant value (such as MicrosoftWindowsServer or RedHat)

  Example:

  `Get-AzVMImageOffer -Location "West Europe" -PublisherName MicrosoftWindowsServer`

+ List available virtual machine image SKU’s for a region:

  `Get-AzVMImageSku -Location <Location> -PublisherName <Publisher Name> -Offer <Offer name>`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 3: Replace **<Publisher_Name>** with the relevant value (see example below)

  Note 4: Replace **<Offer_Name>** with the relevant value (see example below)

  Example:

  `Get-AzVMImageSku -Location "West Europe" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"`



## Storage related commands

+ List available storage accounts:

  `Get-AzStorageAccount | Select StorageAccountName, Location`

+ Create an empty new storage account:

  `New-AzStorageAccount -ResourceGroupName <Resource Group Name> -AccountName <Storage account name> -Location <Location> -SkuName <Storage account type>`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 3: Replace **<Storage_account_name>** with a unique value between 3-24 characters (numbers and lower-case letters)

  Note 4: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 5: Replace **<Storage_account_type>** with a value from the list below:

  https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview

  Example:

  `New-AzStorageAccount -ResourceGroupName RG01 -AccountName mystorageacct01 -Location “West Europe” -SkuName Standard_LRS`

+ Create a new storage account and a new blob storage container:

  `$storageAccount = New-AzStorageAccount -ResourceGroupName <Resource Group Name> -Name <Storage account name> -SkuName <Storage account type> -Location <Location> -Kind Storage`

  `$ctx = $storageAccount.Context`

  `$containerName = <Container name>`

  `New-AzStorageContainer -Name $containerName -Context $ctx -Permission blob`

  Note 1: The above commands should be written in a single line (for each command)

  Note 2: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 3: Replace **<Storage_account_name>** with a unique value between 3-24 characters (numbers and lower-case letters)

  Note 4: Replace **<Storage_account_type>** with a value from the list below:

  https://docs.microsoft.com/en-us/azure/storage/common/storage-account-overview

  Note 5: Replace **<Location_>** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 6: Replace **<Container_name>** with a relevant and unique value

  Example:

  `$storageAccount = New-AzStorageAccount -ResourceGroupName RG01 -Name mystorageacct01 -SkuName Standard_LRS -Location “West Europe” -Kind Storage`

  `$ctx = $storageAccount.Context`

  `$containerName = "quickstartblobs"`

  `New-AzStorageContainer -Name $containerName -Context $ctx -Permission blob`

+ Remove a storage account:

  `Remove-AzStorageAccount -ResourceGroupName <Resource Group Name> -AccountName <Storage account name> –Force`

  Note 1: The above command should be written in a single line

  Note 2: Replace **<Resource_Group_Name>** with relevant value (see example below)

  Note 3: Replace **<Storage_account_name>** with the relevant value

  Example:

  `Remove-AzStorageAccount -ResourceGroupName RG01 -AccountName mystorageacct01 –Force`