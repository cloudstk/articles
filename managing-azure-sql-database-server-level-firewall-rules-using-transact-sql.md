Managing Azure SQL Database server-level firewall rules using T-SQL
====================================================================
Azure SQL Database uses firewall rules to control access to your server and databases by specifying ranges of IP addresses. The firewall rules can be defined at the server-level and at the database-level.    

There are several ways to configure Firewall rules for Azure SQL server. You can configure server-level IP firewall rules by using the Azure portal, PowerShell, REST API or T-SQL statements. 

In this tutorial, we will look at the following T-SQL statements to configure Server-level firewall rules.
**Select * from sys.firewall_rules** –  List all of the existing server-level firewall rules associated with your Azure SQL Database Server
**sp_set_firewall-rule** -  Create or updates server-level IP firewall rules
**sp_delete_firewall_rule** - Removes server-level IP firewall rules

**Steps**
----------------
1.	Open Azure Data Studio and connect to your Azure SQL server.
    On the **Servers** menu, Click on **New Connection** to open the **Connection** pane. Fill the connection details and then click on the **Connect** button to connect to Azure SQL Server, as shown in figure 1



    Figure 1 : 

2.	Open a New Query window on the master database and run the following query to list all the active server-level firewall rules on the server, as shown in figure 2.   
    ```
        Select * from sys.firewall_rules
    ```


    Figure 2.0 Listing the server-level firewall rules

3.	Run this query to add a new server-level firewall rule:
    ```
    Execute sp_set_firewall_rule @name = N'DKclientIP', 
        @start_ip_address   = 'xxx.xxx.xxx.xxx', 
        @end_ip_address     = 'xxx.xxx.xxx.xxx'
    ```

    Next, execute the following command to verify the added firewall rule.
    
    ```
    Select * from sys.firewall_rules
    ```
    In below figure 3, we can see now a new firewall rule added with the name as ‘DKclientIP’ and IP range from 0.0 to 3.. 



    Figure 3. : Verifying the added rule


    To update an existing server-level firewall rule, execute the sp_set_firewall_rule with the firewall rule name and IP addresses you want to update.
    
    ```
    Execute sp_set_firewall_rule @name = N'DKclientIP', 
        @start_ip_address   = 'xxx.xxx.xxx.xxx', 
        @end_ip_address     = 'xxx.xxx.xxx.xxx'
    ```

    Next, run the  **Select * from sys.firewall_rules** command to verify updated firewall rule.


    Figure 4: Verifying the updated firewall rule


4.	Execute the following command to delete an existing server-level firewall rule.

    Execute sp_delete_firewall_rule @name = N’DK_ClientIP’

    To verify, execute the following command.

    ```
    Select * from sys.firewall_rules
    ```





    Figure 5: Verifying the deleted firewall rule.


