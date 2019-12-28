Export an Azure App Service Certificate Using Kudu PowerShell
===========================================================

How to open Kudu PowerShell console
--------------------------
You can open Kudu Powershell console using the following:
1. If your Azure Web app URL is h<span>ttps://</span>mysite.azurewebsites.net/, then the URL of the Kudu will be h<span>ttps://</span>mysite.scm.azurewebsites.net/ .  Once authenticated, you can see a similar screen, as shown in figure 2.0, if Azure App Service is running on Windows.
2. In the left panel of the App Service, click on **Advanced Tools** and then click on **Go** link, as shown on figure 1.0. 

 ![Image](https://github.com/cloudstk/articles/blob/master/azure/media/azure-app-service-blade.jpg "icon")
        
        Figure 1.0: App Service blade


This will open the Kudu site of your App Service in a new window. On the **Debug console** menu, click on **PowerShell** to open the Kudu PowerShell console, as shown in figure 2.0.

 ![Image](https://github.com/cloudstk/articles/blob/master/azure/media/kudu-powershell-console.jpg "icon")

        Figure 2.0: The Kudu Service page.


Run the following PowerShell cmdlets to export the certificate.

```powershell
  Get-ChildItem  -Path cert:\localmachice\my  | Select-Object –first 1 | Export-Certifactte  -FilePath D:\home\site\wwwroot\cert.cer –Force
```

 ![Image](https://github.com/cloudstk/articles/blob/master/azure/media/cmdlet-to-export-the-certificate.jpg "icon")

           Figure 3.0: PowerShell cmdlets to export the certificate.


Then you can download the .cer extension file from the specified path.

You can see the following articles for reference:
* [Exports a certificate from a certificate store into a file ](https://docs.microsoft.com/en-us/powershell/module/pkiclient/export-certificate?view=win10-ps) 
* [Creating a local PFX copy of App Service Certificate ](https://azure.github.io/AppService/2017/02/24/Creating-a-local-PFX-copy-of-App-Service-Certificate.html) 


