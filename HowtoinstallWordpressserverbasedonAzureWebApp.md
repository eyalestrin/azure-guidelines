# How to install Wordpress server based on Azure Web App

## How to install Azure CLI Tools

1. Login to the machine using privileged account.

2. Download the latest build of Azure CLI.

   + Windows download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest

   + Linux download instruction and location:

     https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?view=azure-cli-latest



## How to login to an Azure subscription

1. Login to an Azure account, from command prompt:

   `az login`

2. Run the command below to list the available subscriptions:

   `az account list --output table`

3. Run the command below to change the context to a specific Azure subscription:

   `az account set --subscription "MySubscription"`

   Note: Replace **“MySubscription”** with the relevant subscription name

4. Run the command below to verify the currently selected Azure subscription:

   `az account show`



## Installation phase

1. Run the command below to create a new resource group:

   `az group create --name MyResourceGroup --location MyLocation`

   Note 1: Replace **MyResourceGroup** with your own relevant group name

   Note 2: Replace **MyLocation** with the target location, from the list below:

   https://azure.microsoft.com/en-us/global-infrastructure/locations/

2. Run the command below to create a new Azure App Service plan:

   `az appservice plan create -n wordpressappservice -g MyResourceGroup -l MyLocation --is-linux --sku S1`

   Note 1: The above command should be written as single line

   Note 2: Replace **wordpressappservice** with your own app service plan name (Alphanumeric, without space or special characters)

   Note 3: Replace **MyResourceGroup** with the previously create resource group

   Note 4: Replace **MyLocation** with the same region as the resource group

3. Run the command below to create a new MySQL database:

   `az mysql server create -g MyResourceGroup -n MyDBServerName --admin-user MyDBUserName --admin-password "MyDBPassword" -l MyLocation --ssl-enforcement Disabled --sku-name B_Gen5_1 --version 5.7`

   Note 1: The above command should be written as single line

   Note 2: Replace **MyResourceGroup** with the previously create resource group

   Note 3: Replace **MyDBServerName** with your own MySQL server name

   Note 4: Replace **MyDBUserName** with your own MySQL username

   Note 5: Replace **MyDBPassword** with a complex password for the MySQL database account

   Note 6: Replace **MyLocation** with the same region as the resource group

4. Run the command below to configure firewall rule for accessing the MySQL database:

   `az mysql server firewall-rule create -g MyResourceGroup --server MyDBServerName --name AllowAppService --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0`

   Note 1: The above command should be written as single line

   Note 2: Replace **MyResourceGroup** with the previously create resource group

   Note 3: Replace MyDBServerName with your own MySQL server name

5. Run the command below to create a new database for the Wordpress application:

   `az mysql db create --resource-group MyResourceGroup --server-name MyDBServerName --name MyWordPressDBName`

   Note 1: The above command should be written as single line

   Note 2: Replace **MyResourceGroup** with the previously create resource group

   Note 3: Replace **MyDBServerName** with your own MySQL server name

   Note 4: Replace **MyWordPressDBName** with your own custom WordPress database name

6. Run the command below to configure the Wordpress App service:

   `az webapp create -n MyAppServiceName -g MyResourceGroup --plan wordpressappservice -i "wordpress"`

   Note 1: The above command should be written as single line

   Note 2: Replace **MyAppServiceName** with your own app service name

   Note 3: Replace **MyResourceGroup** with the previously create resource group

7. Run the command below to configure the WordPress App service database connection settings:

   `az webapp config appsettings set -n MyDBServerName -g MyResourceGroup --settings WORDPRESS_DB_HOST= MyDBServerName.mysql.database.azure.com WORDPRESS_DB_USER="MyDBUserName@MyDBServerName.mysql.database.azure.com" WORDPRESS_DB_PASSWORD="MyDBPassword"`

   Note 1: The above command should be written as single line

   Note 2: Replace **MyDBServerName** with your own MySQL server name

   Note 3: Replace **MyResourceGroup** with the previously create resource group

   Note 4: Replace **MyDBUserName** with your own MySQL username

   Note 5: Replace **MyDBPassword** with a complex password for the MySQL database

8. Exit the command prompt

9. Login to the Azure portal:

   https://portal.azure.com/

10. From the left pane, click on Resource Groups -> select the newly created resource group -> from the main pane, click on Tags:

    + **Name:** Specify here “Project”
    + **Value:** Specify here a value to represent the project name

11. Click on Save

12. From the upper search field, write “App Service plans” -> Select the newly create service plan -> From the main pane, click on “Tags”:

    + **Name:** Specify here “Project”
    + **Value:** Specify here a value to represent the project name

13. Click on Save
14. From the upper search bar of the Azure portal, write “Azure Database for MySQL servers” -> click to enter the properties of the newly created MySQL database -> From the main pane, click on “Tags”:
    + **Name:** Specify here “Project”
    + **Value:** Specify here a value to represent the project name
15. Click on Save
16. From the upper search bar of the Azure portal, write “App Services” -> Select the newly create App services:
    + From the Overview page, write down the URL
    + From the Tags page:
      + **Name:** Specify here “Project”
      + **Value:** Specify here a value to represent the project name
      + Click on Save

17. Log off the Azure Portal



## WordPress initial configuration

1. Open a browser and specify the FQDN name of the Wordpress app service.
2. From the language selection page, select English and click Continue
3. Click on “Let’s go!”
4. From the Welcome wizard page:
   + Specify the web site title
   + Specify your own username
   + Write down the password and store it in a safe location
   + Specify an email address for notifications (prefer to use a mailing list)
5. Click Install WordPress