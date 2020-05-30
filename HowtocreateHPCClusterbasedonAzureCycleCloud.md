# How to create HPC Cluster based on Azure CycleCloud

## Installing Azure CLI

1. Login to the machine using privileged account.

2. Download the latest build of Azure CLI:

   + Windows download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest

   + Linux download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?view=azure-cli-latest



## Login to the Azure subscription

1. Run the command below to login to the Azure subscription:

   `az login`

2. List available subscriptions:

   `az account list --output table`

3. Change the context to a specific Azure subscription:

   `az account set --subscription "My Subscription"`

   Note: Replace **"My Subscription”** with the relevant subscription name

4. Run the command below to verify the currently selected Azure subscription:

   `az account show`



## Configure CycleCloud pre-requirements

1. From a command prompt, run the command below to configure a service principal:

   `az ad sp create-for-rbac --name CycleCloudApp-MySubscription --years 1`

   Note: Replace **CycleCloudApp-MySubscription** with a unique name, relevant to the target Azure subscription

2. Document the command output (**appId**, **displayName**, **name**, **password**, **tenant**)

3. From Linux command prompt, run the command below to generate SSH key pair:

   `ssh-keygen -f ~/.ssh/id_rsa -m pem -t rsa -N "" -b 4096`



## Deploy the Azure CycleCloud

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the left pane click on Subscriptions -> from the main pane, click on “global subscriptions filter” -> make sure the target Azure subscription is the only subscription selected

3. Inside the top search pane, write “Marketplace”

4. Inside the “Search the Marketplace” field, write “Azure CycleCloud”

5. Click on Create:

   + **Subscription**: Select the target subscription name

   + **Resource group**: Select “Create new”

   + **Virtual machine name**: Specify here the Azure CycleCloud VM name

   + **Region**: Specify a region close to your location (such as **West Europe**)

     Note: For full list of regions, see:

     https://azure.microsoft.com/en-us/global-infrastructure/locations/

   + **Availability options**: Leave the default settings

   + **Image**: Leave the default “Azure CycleCloud”

   + **Size**: For small HPC cluster, you may select Standard D2s v3 (2 vCPU, 8GB), otherwise, leave the default Standard D4s v3 (4 vCPU, 16GB)

   + **Authentication type**: SSH public key

   + **Username**: Specify here a username for the cluster admin account (for SSH login to the machine)

     Note: Remember to document this detail for future use

   + **SSH public key:** Paste here the content of the SSH public key (**id_rsa.pub**) previously created

6. Click Next: Disks

   + **OS disk type** – For test purpose or small scale cluster, select “Standard SSD”

     For production or large scale cluster, select “Premium SSD”

7. Click Next: Networking

   + **Virtual network**: Leave default settings
   + **Subnet**: Leave default settings
   + Configure network security group: Click on “Create new” -> leave the default settings -> click OK

8. Click Next: Management

   + **Boot diagnostics:** Select Off

9. Click Next: Advanced -> click Next: Tags

   + **Name**: Specify here Project
   + **Value:** Specify here Azure subscription name

10. Click Next: Review + create
11. Click on Create
12. Wait for the deployment process to complete
13. When the deployment process completes, click on Go to resource
14. From the newly created VM “Overview” page, locate the Public IP address and document it.



## Azure CycleCloud Initial Setup

1. Open a Browser, and go the URL below:

   https://my_cyclecloud_ip/

   Note 1: Replace **My_CycleCloud_IP** with the public IP address of the CycleCloud VM

   Note 2: Ignore the SSL certificate warning (by default CycleCloud is deployed with self-signed certificate)

2. **Site name**: specify here unique name for the cluster

3. Click Next

4. Select “I agree” and click Next

   + **User ID**: Specify an admin account for managing the CycleCloud
   + **Name**: Specify a full name for the CycleCloud admin account
   + **Password**: Specify here complex password for the CycleCloud admin account and confirm the password
   + **SSH public key:** Paste here the content of the SSH public key (**id_rsa.pub**)

5. Click on Done
6. On the “No Account Configured” page, click on “Click here”
   + **Account Name**: Specify here the service principal name previously created
   + **Tenant ID**: Specify here the “tenant” information of the service principal
   + **Application ID**: Specify here appId of the service principal
   + **Application Secret:** Specify here the service principal password
7. Click on “Validate Credentials”
   + **Default Location**: Select the same region where the CycleCloud was deployed into (such as West Europe)
   + **Resource Group**: Select the resource group where the CycleCloud was deployed into
   + **Storage Account:** Specify a name for a storage account (up to 24 characters, lowercase and numbers)

8. Click on Save



## Azure CycleCloud configuration and cluster installation phase

1. Login using SSH to the CycleCloud server (using the public IP address from the Azure portal, and the SSH key previously created)

2. Copy the SSH key pair generated at the beginning of the guideline into the CycleCloud server, subfolder **/home/cycleadmin/.ssh**

   Note: Replace **cycleadmin** with the CycleCloud admin account (to login using SSH)

3. Run the commands below to change the ownership of the SSH key pair:

   `cd ~`

   `chown cycleadmin:cycleadmin ~/.ssh/id_rsa ~/.ssh/id_rsa.pub`

   Note: Replace **cycleadmin** with the CycleCloud admin account (to login using SSH)

4. Run the commands below to change the permissions of the SSH key pair:

   `chmod 600 ~/.ssh/id_rsa`

   `chmod 644 ~/.ssh/id_rsa.pub`

5. Duplicate the CycleCloud Key:

   `cp ~/.ssh/id_rsa ~/.ssh/cyclecloud.pem`

6. Run from CLI the command below to initialize the cluster:

   `cyclecloud initialize`

   + **CycleServer URL**: Change the value to https://localhost/
   + **Detected untrusted certificate**: Yes
   + **CycleServer username**: Specify here the previously created CycleCloud admin account
   + **CycleServer password**: Specify here the password for the CycleCloud admin account

   Note: The configuration will be saved into **~/.cycle/config.ini**



## Lustre deployment

1. Login to the CycleCloud server using SSH

2. Run the commands below to install Git:

   `sudo yum install git`

3. Run the command below to download from the CycleCloud Lustre Git repository:

   `cd ~`
   `git clone https://github.com/hmeiland/cyclecloud-lustre.git`
   `cd cyclecloud-lustre`

4. Run the command below to list the CycleCloud lockers:

   `cyclecloud locker list`

   Note: Document the output of the above command

5. Run the command below to upload a CycleCloud project:

   `cyclecloud project upload <locker-from-previous-step>`

   Note: Replace **<locker_from_previous_step>** with the value of the list command

6. Run the command below to import the Lustre template:

   `cyclecloud import_template -f templates/lustre.txt`

7. Open a Browser and login to the CycleCloud web console:

   https://my_cyclecloud_ip/

   Note 1: Replace **My_CycleCloud_IP** with the public IP address of the CycleCloud VM

   Note 2: Ignore the SSL certificate warning (by default CycleCloud is deployed with self-signed certificate)

8. From the left pane, click on Clusters -> from the main pane, click on Lustre icon

   + **Cluster name:** Specify here cyclecloud-lustre

9. Click on Next -> Networking -> On the region, select the target region where the CycleCloud is deployed into (such as West Europe)-> Subnet ID -> select the subnet where the CycleCloud server is deployed into -> click Next -> Advanced Settings -> leave the default settings -> click Next -> Lustre Settings:
   + **Blob Account**: Specify here the name of Azure storage account previously created (from within the Azure Portal -> Storage accounts)
   + **Blob Key**: Specify here 1st storage account access key (from within the Azure Portal -> Storage accounts -> Access keys)
   + **Blob container:** Specify here the name of the Azure blob container (from within the Azure Portal -> Storage accounts -> Blobs)

10. Click on Save

11. From the **cyclecloud-lustre** page, click on Start -> click OK

12. Wait for the new cluster process deployment to complete (2 cluster nodes will be created and the status will appear in green, without errors)

13. Log off the CycleCloud web console

14. Return to the CycleCloud server SSH console

15. Run the command below to view the status of the Lustre cluster:

    `cyclecloud show_cluster cyclecloud-lustre`

    Note: **cyclecloud-lustre** is the Lustre cluster name we have previously created



## Slurm cluster deployment

1. Login to the CycleCloud server using SSH

2. Run the command below to download from Slurm Git repository:

   `cd ~`
   `git clone https://github.com/andreas-wilm/cyclecloud-dingo-compute`
   `cd cyclecloud-dingo-compute`

3. Run the command below to list the CycleCloud lockers:

   `cyclecloud locker list`

   Note: Document the output of the above command

4. Run the command below to upload a CycleCloud project:

   `cyclecloud project upload <locker-from-previous-step>`

   Note: Replace **<locker_from_previous_step>** with the value of the list command

5. Run the command below to import the Slurm template:

   `cyclecloud import_template -f templates/dingo-compute.txt`

6. Open a Browser and login to the CycleCloud web console:

   https://my_cyclecloud_ip/

   Note 1: Replace **My_CycleCloud_IP** with the public IP address of the CycleCloud VM

   Note 2: Ignore the SSL certificate warning (by default CycleCloud is deployed with self-signed certificate)

7. From the left pane, click on Clusters -> from the lower pane, click on + sign (Add) -> from the main pane, click on the **“dingo-compute”** icon

   + **Cluster name**: Slurm
   + **Region**: Select the target region where the CycleCloud is deployed into (such as West Europe)
   + **Subnet ID:** select the subnet where the CycleCloud server is deployed into

8. Click Next -> Advanced Settings -> leave the default settings -> click Next -> Virtual Machines:

   + **Master VM Type**: For small HPC cluster, you may select Standard D2s v3 (2 vCPU, 8GB), otherwise, leave the default Standard D4s v3 (4 vCPU, 16GB)

   + **Execute VM Type**: For small cluster, select Standard D4s v3 (4 vCPU, 16GB), for high performance cluster, select a VM type from the list:

     https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes-hpc

     Note: In-case you have requirement for Infiniband, select VM type from the above list that specifically says it support Infiniband

   + **Max Cores**: Specify here the maximum number of cores in the cluster, once the auto-scaling is enabled

   + **Low Priority:** Select this feature if you have requirement for cost and your workload support that fact that a VM might be taken by Azure and you code support continuous running from a new VM

9. Click Next
   + **Lustre Cluster**: Select the name of the Lustre cluster
   + **Slurm Version:** Specify the build of Slurm (such as 17.11.12-1)

10. Click Save
11. From the Slurm page, click on Start -> click OK
12. Wait for the new cluster process deployment to complete (A cluster node will be created and the status will appear in green, without errors)
13. Log off the CycleCloud web console
14. Return to the CycleCloud server SSH console

15. Run the command below to view the status of the Lustre cluster:

    `cyclecloud show_cluster Slurm`



## Check HPC cluster status

1. To make sure a Slurm cluster was successfully created and mounted to Lustre file system, login to the Master node VM using SSH

   Note: The Master node public IP address can be found inside the Azure Portal -> Virtual Machines or from the CycleCloud web console -> Clusters -> Slurm

2. Run the commands below to check the Slurm cluster status:

   `sinfo`
   `squeue`

3. Run the command below to make sure the Lustre file system was automatically mounted inside the Master node:

   `mount | grep lustre`



## Terminate the entire Azure CycleCloud environment

 Follow the instructions in the link below:

https://docs.microsoft.com/en-us/azure/cyclecloud/end-cluster

Note: In-case you used an existing Azure resource group, you have to manually select the CycleCloud resources and delete them



## References

+ Azure CycleCloud Quickstarts

https://docs.microsoft.com/en-us/azure/cyclecloud/quickstart-install-cyclecloud

+ Azure CycleCloud Quickstart 2: Create and Run a Simple HPC Cluster

https://docs.microsoft.com/en-us/azure/cyclecloud/quickstart-create-and-run-cluster

+ Manual Installation

https://docs.microsoft.com/en-us/azure/cyclecloud/installation

+ Creating a Slurm/MPI/Lustre HPC cluster with Azure CycleCloud

https://andreas-wilm.github.io/2019-07-05-slurm-cluster-with-lustre/

+ Cluster Templates

https://docs.microsoft.com/en-us/azure/cyclecloud/cluster-templates

+ CycleCloud Slurm

https://github.com/Azure/cyclecloud-slurm

+ Parallel Virtual File Systems on Microsoft Azure

https://azure.microsoft.com/mediahandler/files/resourcefiles/parallel-virtual-file-systems-on-microsoft-azure/PVFS%20on%20Azure%20Guide.pdf
