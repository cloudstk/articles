Provisioning a New Azure SQL Database Server Using PowerShell
=============================================================
This article shows you how to create an Azure SQL Database services using Azure PowerShell.

Prerequisites
---------------------
Before you begin this tutorial, you must have the following:
* Azure Subscription, if you don't already have an Azure subscription,[create a free account](https://azure.microsoft.com/en-us/free/search/?&ef_id=EAIaIQobChMIsvT_-5ui5gIVA4jVCh0f6Qm1EAAYASAAEgJ1aPD_BwE:G:s&OCID=AID2000071_SEM_3xJK0DI6&MarinID=3xJK0DI6_341611205015_%2Bazure%20%2Bfree_b_c__60219755501_kwd-323834433994&lnkd=Google_Azure_Brand&dclid=CMDDybr6t-YCFVOA3godxTgK-g) .
* Azure Data Studio(ADS) with PowerShell Extension, in this tutorial, we will use ADS to edit and run PowerShell scripts, and establish a connection to your Azure SQL Server, see [How to use PowerShell in Azure Data Studio](https://azure.microsoft.com/en-us/resources/videos/azure-friday-how-to-use-powershell-in-azure-data-studio/#time=00h04m45s).


In this tutorial, we will look at the following:
-----------------------------------------------
* Provisioning a New Microsoft Azure SQL Database Server.
* Configuring a firewall rule for a Microsoft Azure SQL Database Server.
* Connecting to a Microsoft Azure SQL Database Server using ADS.

**Steps**:
-------------
1. Authenticate your Azure subscription, then start the creation process. as follows.  
First of all, you have to connect to your subscription using the **Connect-AzAccount** cmdlet.

```powershell
Connect-AzAccount
```
Running this command will open a Microsoft login window, as shown in figure 1.0. Log in using your Azure subscription creentials.

 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/connect-to-zure-subscription.jpg "icon")  

Figure 1.0: Connect to your Azure subscription.

2. Create a new resource group  
In this step, we will create an Azure Resource Group by using just a **Name** and **Location** parameters.
```powershell
$parameters = @{
    Name               = 'azsqldb-demo-rg'
    Location           = 'northeurope'
}
New-AzResourceGroup @parameters
```

You can see the output as shown in figure 2.
 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/new-resource-group.jpg "icon")  

Figure 2: The creation of an Azure Resouce Group.

3. Create an Azure SQL Server  
To create an Azure SQL Server instance, we used the following paramenters:  
```powershell
    $Username   = "cloudstksql"
    $Password   = "pa$$w@rd1" | ConvertTo-SecureString -AsPlainText -Force
    $Cred       = New-Object System.Management.Automation.PSCredential($Username,$Password)

$parameters = @{
    ResourceGroupName               = 'azsqldb-demo-rg'
    ServerName                      = 'cloudstksqlserver'
    Location                        = 'northeurope'
    SqlAdministratorCredentials     = $cred
    ServerVersion                   = '12.0'
}

New-AzSqlServer @parameters
```
 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/create-an-azure-sql-server.jpg "icon")  

Figure 3 : The creation of an Azure Resouce Group.

The server is ready, in the next step, we will create an Azure SQL Database.

4. Create an Azure SQL Database   
Let's start with the creation of new Azure SQL Database with the following parameters.  

```powershell
$parameters = @{
    ResourceGroupName               = 'azsqldb-demo-rg'
    ServerName                      = 'cloudstksqlserver'
    DatabaseName                    = 'cloudstkdemodb'
    MaxSizeGB                       =  250
    RequestedServiceObjectiveName   = 'S0'  
  }
New-AzureRmSqlDatabase @parameters
```

 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/creation-of-azure-sqldb.jpg "icon")  

 Figure 4 : The creation of an Azure Resouce Group.

5. Setting up Firewall rules    
To allow inbound access for an Azure SQL Server, you must add a specific IPs to the Azure SQL Server firewall rules.  
In this demo, we're going to define a specific IP address(your machine's IP) to connect
SQL Azure.   
You can set up a firewall rule with the following parameters:  
```powershell
$parameters = @{
    ResourceGroupName = 'azsqldb-demo-rg'
    ServerName        = 'cloudstksqlserver'
    FirewallRuleName  = 'AllowedIps'
    StartIpAddress    = 'xxx.xxx.xxx.xxx'
    EndIpAddress      = 'xxx.xxx.xxx.xxx'
}

New-AzSqlServerFirewallRule @parameters
```

 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/creation-of-azure-sqldb.jpg "icon")  

 Figure 5 : Setting up Firewall rules.

You're now ready to connect to your Azure SQL Server from your specified IP address.

5. Connecting to SQL Azure from Azure Data Studio(ASD)  
Connecting to Azure SQL server from ASD is like connenting to any of the SQL server. To do this, you will need to perform the following steps:  

* On the **Servers** menu, Click on **New Conenction** to open the Connection pane, as shown figure 6.  

 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/new-connection-using-ads "icon")    

Figure 6 : Click on **New Connection**.


* Fill in the following fields using the server name, user name, password and then click on **Connect** button to connect to Azure SQL server.  

 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/ads-connection-prompt.jpg "icon")  

Figure 6.1: **Connection** pane.


Once sucessfully connected to the Server, the new **cloudstkdemodb** appears in the list of databases, as shown figure 3.0.  


 ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/ads-az-sqlserver-object-explorer.jpg "icon")  

Figure 6.2: An Azure SQL server Object Explorer.  

-------------
In this article, we have looked at how to create an Azure SQL server database using PowerShell. We have also seteup the firewall and Finally, connected an Azure SQL Server with Azure Data Studio.