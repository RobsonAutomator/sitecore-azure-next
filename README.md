# sitecore-azure-next

@RobsonAutomator learning using Sitecore Azure Toolkit to deploy various Sitecore configurations.

## What not to do with Sitecore Azure Toolkit

1. Please not use 'admin' as yous SQL user becuse deployment will fail.
2. If you run deployment twice then your Sitecore installation will be destroyed 

## How to login to Azure account in automated and silent way ?

When you experiment with Sitecore deployment you need to login to your Azure account.
This simple task can be annoying then I will automate it details are described in my post: http://lets-share.senktas.net/2017/06/sitecore-on-azure-login.html

You can use [sitecore-automation](https://www.powershellgallery.com/packages/sitecore-automation/) module to login to Azure in secure and silent way.
```powershell
Import-Module sitecore-automation -MinimumVersion 1.3.0.4

# For first time you will be prompt for username and password
Login-AzureAccountSilent
```
## How to setup Azure storage for Sitecore deployment with ARM templates ?
If you want to use Azure RM templates to deploy Sitecore to Azure, you have to use Azure storage account. 
On blob storage, you should upload ARM JSON files and WDP ZIP packages. In this article, you can found how to configure Azure storage in the automated and convenient way.
http://lets-share.senktas.net/2017/09/sitecore-on-azure-storagepreparation.html

## How to check if Azure region is compatible with Sitecore deployment?

When you would like to deploy Sitecore on Azure you have to check if desired region fully supports Sitecore deployment.
You can do this manually using this [table](https://kb.sitecore.net/articles/617478) - or automate it. Details you can find here  http://lets-share.senktas.net/2017/07/sitecore-on-azure-test-sitecoreazuredeployment.html

```powershell
Import-Module sitecore-automation -MinimumVersion 1.3.0.4

# returns false if some resources are not supported in region
# -Verbose will display all not supported resources
Test-SitecoreAzureRegion -Location 'West Europe' -Verbose
```

## How to use shared access signatures (SAS) in an automated way ?

When you would like to deploy Sitecore on Azure you have to upload ARM templates and WDP files to Azure Storage.
Only fallowing files can be stored locally on your workstation:
- ARM master template file eg. 'C:\azuredeploy.json'
- ARM parameters file eg. 'C:\azuredeploy.parameters.json'
- Sitecore license file eg. 'C:\license.xml'

Any other files must be publicly visible on the Internet. If this is not a problem for you stop reading here.
If you would like to know how to provide secure access to ARM templates and WDPs files read this post http://lets-share.senktas.net/2017/07/sitecore-on-azure-sas-token.html

## Performance issue
https://kb.sitecore.net/articles/983839

