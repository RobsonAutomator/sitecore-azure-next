# sitecore-azure-next

@RobsonAutomator learning using Sitecore Azure Toolkit to deploy various Sitecore configurations.

## How to login to Azure account in automated and silent way ?

When you experiment with Sitecore deployment you need to login to your Azure account.
This simple task can be annoying then I will automate it details are described in my post: http://lets-share.senktas.net/2017/06/sitecore-on-azure-login.html

You can use [sitecore-automation](https://www.powershellgallery.com/packages/sitecore-automation/) module to login to Azure in secure and silent way.
```powershell
Import-Module sitecore-automation -MinimumVersion 1.3.0.4

# For first time you will be prompt for username and password
Login-AzureAccountSilent
```

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

