# Using Azure CLI for managing Azure resources

## Installing Azure CLI

1. Login to the machine using privileged account.

2. Download the latest build of Azure CLI.

   + Windows download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest

   + RHEL/CentOS download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-yum?view=azure-cli-latest

   + Ubuntu/Debian download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-apt?view=azure-cli-latest



## Common Azure CLI commands

1. Login to an Azure account, from command prompt:

   `az login`

2. List available subscriptions:

   `az account list --output table`

3. Change the context to a specific Azure subscription:

   `az account set --subscription "My Subscription"`

   Note: Replace **“My Subscription”** with the relevant subscription name

4. Run the command below to verify the currently selected Azure subscription:

   `az account show`



## Resource group related commands

+ Create a new Azure resource group:

  `az group create --name MyResourceGroup --location MyLocation`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyLocation** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

+ List information about a resource group:

  `az group show --name MyResourceGroup --output table`

  Note: Replace **MyResourceGroup** with your own relevant group name



## Networking related commands

+ List available virtual networks:

  `az network vnet list --output table`

+ List available subnets (Run the command as a single line):

  `az network vnet subnet list --resource-group MyResourceGroup --vnet-name MyVNet --output table`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVNet** with the relevant VNET name

+ Create a new virtual network and a new subnet (Run the command as a single line):

  `az network vnet create --resource-group MyResourceGroup -n MyVnet --address-prefix <Virtual network address prefix CIDR> --subnet-name MySubnet --subnet-prefix <Subnet address prefix CIDR>`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVNet** with the relevant VNET name

  Note 3: Replace **MySubnet** with the target subnet name

  Note 4: Replace **<Virtual_network_address_prefix_CIDR>** with relevant value (see example below)

  Note 5: Replace **<Subnet_address_prefix_CIDR>** with relevant value (see example below)

  Example:

  `az network vnet create --resource-group MyResourceGroup -n MyVnet --address-prefix 10.0.0.0/16 --subnet-name MySubnet --subnet-prefix 10.0.0.0/24`

+ List all available network security groups:

  `az network nsg list --output table`

+ Create a new network security group:

  `az network nsg create --resource-group MyResourceGroup -n MyNsg`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyNsg** with the target network security group

+ List all default available rules inside a network security group (Run the command as a single line):

  `az network nsg show --resource-group MyResourceGroup -n MyNsg --query "defaultSecurityRules[]" --output table`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyNsg** with the target network security group

+ List all available rules inside a network security group (Run the command as a single line):

  `az network nsg rule list --resource-group MyResourceGroup --nsg-name MyNsg --output table`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyNsg** with the target network security group

+ Create a new RDP rule inside an existing network security group (Run the command as a single line)

  `az network nsg rule create --resource-group MyResourceGroup --nsg-name MyNsg -n AllowRDP --priority 500 --source-address-prefixes Internet --destination-port-ranges 3389 --access Allow --protocol Tcp --description "Allow RDP"`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyNsg** with the target network security group

  Note 3: Replace **AllowRDP** with the relevant rule name

  Note 4: Replace **3389** with the relevant port number

  Note 5: Replace **"Allow RDP"** with the relevant rule description

+ List available public IP addresses assigned to virtual machines:

  `az network public-ip list --output table`



## Virtual machine related commands

+ List available virtual machines in a subscription:

  `az vm list --output table`

+ List available virtual machines in a specific resource group:

  `az vm list --resource-group MyResourceGroup --output table`

  Note: Replace **MyResourceGroup** with your own relevant group name

+ Create a Linux VM:

  `az vm create -n MyVm --resource-group MyResourceGroup --image Centos --data-disk-sizes-gb 10 20 --size Standard_DS2_v2 --vnet-name MyVnet --subnet MySubnet --admin-username myusername --generate-ssh-keys`

  Note 1: Run the above command as single line

  Note 2: Replace **MyResourceGroup** with your own relevant group name

  Note 3: Replace **MyVm** with the target virtual machine hostname

  Note 4: Replace **MyVNet** with the relevant VNET name

  Note 5: Replace **MySubnet** with the target subnet name

  Note 6: Replace **myusername** with the relevant value

+ Get information about a specific virtual machine inside a resource group:

  `az vm show --resource-group MyResourceGroup -n MyVm`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVm** with the target virtual machine hostname

+ Show VM power state:

  `az vm show --resource-group MyResourceGroup -n MyVm -d --query "powerState"`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVm** with the target virtual machine hostname

+ Start a virtual machine inside a specific resource group:

  `az vm start --resource-group MyResourceGroup -n MyVm`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVm** with the target virtual machine hostname

+ Restart a virtual machine inside a specific resource group:

  `az vm restart --resource-group MyResourceGroup -n MyVm`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVm** with the target virtual machine hostname

+ Stop a virtual machine inside a specific resource group:

  `az vm stop --resource-group MyResourceGroup -n MyVm`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **MyVm** with the target virtual machine hostname

+ List available virtual machine sizes for a region:

  `az vm list-sizes -l MyLocation --output table`

  Note: Replace **MyLocation** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

+ List available virtual machine image publishers for a region:

  `az vm image list-publishers -l MyLocation --output table`

  Note: Replace **MyLocation** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

+ List available virtual machine image SKU’s for a region:

  `az vm list-skus -l MyLocation --output table`

  Note: Replace **MyLocation** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/



## Storage related commands

+ List available storage accounts:

  `az storage account list`

+ Create an empty new storage account:

  `az storage account create -n mystorageaccount01111 --resource-group MyResourceGroup -l MyLocation --sku Standard_LRS`

  Note 1: The above command should be written as single line

  Note 2: Replace **MyResourceGroup** with your own relevant group name

  Note 3: Replace **MyLocation** with the target location, from the list below:

  https://azure.microsoft.com/en-us/global-infrastructure/locations/

  Note 4: Replace **mystorageaccount01111** with a unique storage account name between 3-24 characters (numbers and lower-case letters)

+ Remove a storage account (Run as a single line):

  `az storage account delete -n mystorageaccount01111 --resource-group MyResourceGroup`

  Note 1: Replace **MyResourceGroup** with your own relevant group name

  Note 2: Replace **mystorageaccount01111** with the relevant storage account name