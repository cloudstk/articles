Provisioning an Azure VM with PowerShell
=======================================
This article shows you how to create an Azure VM using Azure PowerShell.

Prerequisites
---------------------
Before you begin this tutorial, you must have the following:
* Azure Subscription, if you don't already have an Azure subscription,[create a free account](https://azure.microsoft.com/en-us/free/search/?&ef_id=EAIaIQobChMIsvT_-5ui5gIVA4jVCh0f6Qm1EAAYASAAEgJ1aPD_BwE:G:s&OCID=AID2000071_SEM_3xJK0DI6&MarinID=3xJK0DI6_341611205015_%2Bazure%20%2Bfree_b_c__60219755501_kwd-323834433994&lnkd=Google_Azure_Brand&dclid=CMDDybr6t-YCFVOA3godxTgK-g) .
* Visual Studio Code(VSCode) with PowerShell Extension, in this tutorial, we will use VScode for PowerShell Development, see [Using Visual Studio Code for PowerShell Development](https://docs.microsoft.com/en-us/powershell/scripting/components/vscode/using-vscode?view=powershell-6).



**Steps**:
-------------
1. Authenticate your Azure subscription, then start the creation process as follows.  
First of all, you have to connect to your subscription using the **Connect-AzAccount** cmdlet.
```powershell
    Connect-AzAccount
    ```  
    Running this command will open a Microsoft login window, as shown in figure 1.0. Log in using your Azure subscription creentials.

    ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/connect-to-zure-subscription.jpg "icon")  

    Figure 1.0: Connect to your Azure subscription.

    On completion of a successful login, it will display the following information, as shown below figure 1.1

    ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/connect-azaccount.jpg "icon")  

    Figure 1.1: Successful login information.

2. Create Resoucr Group
 Create an Azure resource group with **New-AzResourceGroup**. A resource group is a logical container into which Azure resources are deployed and managed.

  In this step, we will create an Azure Resource Group by using just a **Name** and **Location** parameters.
```powershell
    $parameters = @{
        Name               = 'azvm-demo-rg'
        Location           = 'northeurope'
    }
        New-AzResourceGroup @parameters
    ```

    You can see the output as shown in figure 2.

    ![Image](https://github.com/cloudstk/articles/blob/master/sql-database/media/new-resource-group.jpg "icon")  

    Figure 2: The creation of an Azure Resouce Group.

3. Provisioning a New Azure VM.
    To provision a new VM, run the **New-AzVm** with the following parameters:
    ```powershell
    $parameters = @{
        ResourceGroupName               = 'azvm-demo-rg'
        Location                        = 'northeurope'
        VirtualNetworkName              = 'demovmVnet'
        SubnetName                      = 'demovmSubnet'
        SecurityGroupName               = 'demovmNSG'
        PublicIpAddressName             = 'demovmPublicIP'
        }
        New-AZvm @parameters
    ```

    The VM deployment process can take several minutes to complete. Once the deployment is complete, you can see the output as shown in figure 3.

3. Connect to the VM using PowerShell
    Once a VM is deployed, you can connect to the VM using PowerShell by running the **Enable-PSRemoting** cmdlet:


