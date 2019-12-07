Copy Data From On-Premise SQL Server To Azure SQL Database Using Azure Data Factory(ADF) User Interface(UI)
========================================================

This article shows you how to use Azure Data Factory  to copy data from on-promise SQL server source to an Azure SQL database destination.

**Prerequisites**

Before you begin this tutorial, you must have the following:

* Azure Subscription, if you don't already have an Azure subscription, create a [free account](https://www.google.com/aclk?sa=l&ai=DChcSEwiy9P_7m6LmAhUDiNUKHR_pCbUYABAAGgJ3cw&sig=AOD64_3nuMiolM8L8ymifrYSIi_n6QuLkg&q=&ved=2ahUKEwjd7Pb7m6LmAhWul4sKHbl2BrMQ0Qx6BAgREAE&adurl=).
* On-premises SQL Server database: You can use SQL Sever Management Studio(SSMS) or Azure Data Studio to create sample database.
* Azure SQL Database: If you don’t have an Azure SQL database, see Create a single database in an Azure SQL Database article for steps to create one.


**Steps:**
1.	Creating  a sample table an on-promises SQL server database and Azure SQL database.
There are several ways to connect to SQL server. In this tutorial, I am using SSMS to connect both on-premises and Azure SQL server database. 
Here, I assume you have successfully connected both on-promises SQL server database and Azure SQL database.  

1.1 **Creating a sample table an on-promises  SQL server database**  
In this step, we will create a sample table called ‘orders’ in the **EverestCycleStores** database and will put a few records into it. We will use this sample data as a source to copy data into the Azure SQL database. The below SQL scripts are used to create orders table and insert sample data into it. The created table shown in figure 1.1.
