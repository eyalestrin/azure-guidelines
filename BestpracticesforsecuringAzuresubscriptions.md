# Best practices for securing Azure subscriptions

## Configure MFA (Multi-Factor Authentication) for any account with owner privileges

In-order to avoid potential compromise of credentials, it is recommended to configure multi-factor authentication for any account with owner privilege.

1. Install Microsoft Authenticator app on your mobile device, as instructed:

   https://docs.microsoft.com/en-us/azure/active-directory/user-help/multi-factor-authentication-end-user-manage-settings#add-or-change-your-phone-number

2. Login to the Azure Portal:

   https://portal.azure.com/

3. From the top right pane, click on your username

4. Click on View account

5. Under "Manage account", click on "Additional security verification"

6. Under "How would you like to respond", click on "Set up Authenticator app"

7. Follow the on-screen instructions, including using your mobile device to scan the QR code, and then select Next

8. You'll be asked to approve a notification through the Microsoft Authenticator app, to verify your information.

9. Select Save

10. Logoff the Azure Portal



## Limit number of inbound ports

Allowing large number of inbound ports access Azure resources increase the chance of network breach. Limit the number of inbound ports to required ports only and to specific resources or specific subnets.

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Network Security Groups"

3. From the main pane, select an existing Network Security Group

4. From the main pane, click on Inbound security rules

5. Review all inbound rules

   Note: It is highly recommended that inbound access on SSH (port 22TCP) or RDP (port 3389TCP) will be limited to specific IP address or IP range from known source location.

6. Update the Network Security Group as needed

7. Save the Network Security Group

8. Log off the Azure portal



## SQL Server Access Restricted

Allowing unnecessary inbound access to Azure SQL Server increase the chance of network breach. Limit the inbound access to your Azure SQL servers to required sources only.

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Azure SQL"

3. For each SQL server

4. Click on Firewall / Virtual Networks

5. Ensure that the firewall rules exist, and no rule has Start IP of 0.0.0.0 and End IP of 0.0.0.0 or other combinations which allows access to wider public IP ranges

6. Configure the source CIDR/IP to the required subnet or required IP address.

7. Log off the Azure portal



## Storage Blob Container Public Access

Allowing public access to storage blob containers increase the chance of data breach. Make sure no storage blob container is publicly accessible.

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Storage accounts"

3. From the main pane, select a storage account from the list

4. For each storage account, go to Containers under BLOB SERVICE

5. For each container, click Access policy

6. Ensure that Public access level is set to Private (no anonymous access)

7. Log off the Azure portal