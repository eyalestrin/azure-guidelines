# Best practices for Azure cost optimization

## Low Utilization virtual machines

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Virtual machines"

3. Select an existing virtual machine

4. From the overview pane, change “Show data for last” to 7 days

5. If the CPU utilization is less than 3% and network utilization is less than 2%, the selected virtual machine qualifies as candidate for an idle instance.

6. Decide if you wish to delete the virtual machine.

7. To delete the virtual machine -> from the upper pane, click on Delete and confirm the action.

8. Log off the Azure portal



## Unassociated public IP Addresses

1. Login to the Azure Portal:

   https://portal.azure.com/

2. From the upper search pane, write "Public IP addresses"

3. Select an existing public IP address from the list

4. From the overview pane, check if the “Associate to” field is empty.

5. If the IP is not associated to any resource, from the upper pane, click on Delete and confirm the action.

6. Log off the Azure portal

 