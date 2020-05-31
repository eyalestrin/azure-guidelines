# How to mount Azure Blob Storage inside a Linux machine

## Get information about credentials file

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search field, write “Storage accounts”
3. From the main pane, click on the target storage account name -> from the main pane, click on Access keys -> write the following details on a temporary location for future use:
   + Storage account name
   + Key 1 -> Key

4. Log off the Azure Portal



## Blob Fuse installation

1. Login using SSH to the target Linux machine using privileged account.

2. Follow the instructions below to install the Blobfuse:

   https://github.com/Azure/azure-storage-fuse/wiki/1.-Installation

3. Run the command `sudo vi /opt/connection.cfg` to create config file with the following content:

   `accountName <account-name>`
   `accountKey <account-key-name>`
   `containerName <container-name>`

   Note 1: Replace **<account_name>** with the value of the storage account name from the Azure portal

   Note 2: Replace **<account_key_name>** with the value of the “key” from the Azure portal

   Note 3: Replace **<container_name>** with the target Azure blob storage container name

4. Change the permissions of the connection.cfg file

   `sudo chown MyUser:MyUser /opt/connection.cfg`
   `sudo chmod 600 /opt/connection.cfg`

   Note: Replace **MyUser** with the username you have logged into the Linux machine



## Mount phase

1. Run the commands below to change permissions for the Azure blob storage:

   `sudo mkdir -p /dev/cloudstorage`
   `sudo mkdir -p /dev/cloudstoragetmp`
   `sudo chown -R MyUser:MyUser /dev/cloudstorage/`
   `sudo chown -R MyUser:MyUser /dev/cloudstoragetmp/`

   Note: Replace **MyUser** with the username you have logged into the Linux machine

2. Run the command below (as as single line) to mount the Azure blob storage:

   `blobfuse /dev/cloudstorage --tmp-path=/dev/cloudstoragetmp --config-file=/opt/connection.cfg`

3. To view the content of the Azure blob storage, switch to the new mount point:

   `cd /dev/cloudstorage`



## Unmount phase

1. When completing the work on the bucket, from the Linux SSH console, and run the commands below to unmount the Azure blob Storage:

   `cd ~`
   `fusermount -u /dev/cloudstorage`

2. Logoff the Linux machine



## Additional references regarding permanent mount using FSTAB

+ https://blogs.msdn.microsoft.com/uk_faculty_connection/2019/02/20/blobfuse-is-an-open-source-project-developed-to-provide-a-virtual-filesystem-backed-by-the-azure-blob-storage/
+ https://github.com/Azure/azure-storage-fuse/wiki/1.-Installation
+ https://docs.microsoft.com/en-us/azure/storage/blobs/storage-how-to-mount-container-linux