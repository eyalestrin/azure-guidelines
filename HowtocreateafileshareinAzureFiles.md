# How to create a file share in Azure Files

## Creating a file share

1. Login to the Microsoft Azure Portal:

   https://portal.azure.com/

2. From the upper search field, specify "Storage accounts"

3. From the "Storage account" page -> select the relevant storage account name

4. From the overview pane, click on Files

5. Click on "File share":

   + Name: Specify here a name for the file share

   + Quota: Specify here the quota (in GB) of the new file share

     For more information, see:

     https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share

6. Click on OK
7. Close the Storage accounts tabs
8. Logoff the Microsoft Azure Portal



## Connecting to an Azure Storage

1. Download the Azure Storage Explorer from:

   https://azure.microsoft.com/en-us/features/storage-explorer/

2. Launch Microsoft Azure Storage Explorer

3. From the "Connect to Azure Storage" page, select "Add an Azure Account" -> click on Sign in

4. Specify credentials to access the Azure Portal

5. From the main pane, under "Account Management", select the relevant subscription and click Apply

6. From the main pane, under "Explorer", expand the relevant subscription -> expand "Storage Accounts" -> expand the storage account name -> expand "File Shares"

7. Click on the relevant share name and view the content of the share

8. To change access permissions to the share, from the main pane, right click on the relevant share name -> click on "Manage Access Policies" -> click on Add -> after making the changes, click on Save

9. From the right pane, use the "Upload" button to upload new files to the share

10. From the right pane, use the "Download" button to download files from the share

11. To exit the Azure Storage Explorer, use File -> Quit



## Mount a file share and access the share in Windows

1. Login to the Microsoft Azure Portal:

   https://portal.azure.com/

2. From the upper search field, specify "Storage accounts"

3. From the "Storage account" page -> select the relevant storage account name

4. From the main pane, click on "Access keys" -> from the right pane, copy on of the storage account keys into memory or write it into a temporary file

5. Close the Storage accounts tabs

6. Logoff the Microsoft Azure Portal

7. Login to the target Windows machine

8. Open File Explorer

9. Navigate to the "This PC" item on the left-hand side of the window. This will change the menus available in the ribbon. Under the Computer menu, select "Map Network Drive"

10. Select the Drive letter and enter the UNC path \\**<storage-account-name>**.file.core.windows.net<share-name>

    Note 1: Replace the **<storage-account-name>**, with the actual storage account name

    Note 2: Replace the <share-name>, with the relevant share name

11. Select "Reconnect at sign-in" and "Connect using different credentials"
12. Click on Finish
13. Use the Storage Account Name prepended with Azure\ as the username and a Storage Account Key as the password
14. Select "Remember my credentials" -> click OK

