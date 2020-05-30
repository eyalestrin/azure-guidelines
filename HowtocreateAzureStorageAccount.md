# How to create Azure Storage Account

1. Login to the Microsoft Azure Portal:

   https://portal.azure.com/

2. From the upper search field, specify "Storage accounts"

3. From the main pane, click on "Create storage account" or "Add":

   + **Name:** Specify here the name of the storage account

   + **Deployment model:** Select "Resource manager"

   + **Account kind:** Select "General-purpose v2 (GPv2)"

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/common/storage-account-options

   + **Location:** Select a region close to your location

   + **Replication:** In case you don't have special requirement for redundancy, select "Locally-redundant storage (LRS)"

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/common/storage-redundancy

   + **Performance:** Select "Standard"

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction

   + **Access tier:** Select "Hot"

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blob-storage-tiers

   + **Secure transfer required:** Select "Enabled"

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/common/storage-require-secure-transfer

   + **Subscription:** Select the relevant subscription name

   + **Resource group:** Select either existing or create a new resource group

     For more information, see:

     https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview#resource-groups

   + **Virtual networks:** Select "Enabled" and select an existing virtual network (VNet) and subnet from the list

4. Click on Create

5. Wait for the storage account creation process to complete

6. From the "Storage account" page -> select the newly created storage account from the list

7. From the main pane, click on Tags -> add a new tag:

   + **Name:** Specify here Name
   + **Value:** Specify here the name of the newly created storage account

8. Click on Save

9. From the main pane, click on Encryption -> select "Use your own key" -> Encryption key: Select from Key Vault:

   + **Key Vault:** Select an existing key vault or create a new vault

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption-customer-managed-keys

   + Encryption key: Create a new key:

     + **Options:** Select Generate
     + **Name:** Specify here the name of the storage account encryption key
     + **Key Type:** Select RSA
     + **RSA Key Size:** Select 2048
     + **Enabled:** Select Yes

10. Click on Create

11. Click on Save

12. From the main pane, click on "Firewalls and virtual networks":

    + **Allow access from:** Make sure "Selected networks" is checked
    + **Address range:** Specify here a static public IP address or your organization public address/CIDR

13. Click on Save

14. Close the Storage accounts tabs

15. Log off the Microsoft Azure Portal