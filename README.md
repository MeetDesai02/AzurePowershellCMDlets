# Azure PowerShell Cmdlet Reference

## Setup and Authentication

### Install Azure PowerShell Module
```powershell
Install-Module -Name Az -AllowClobber -Scope CurrentUser
```
### Login To Azure
```powershell
Connect-AzAccount
```
## Resource Group Management
### Create a Resource Group
```powershell
New-AzResourceGroup -Name "MyResourceGroup" -Location "EastUS"
```
### Delete a Resource Group
```powershell
Remove-AzResourceGroup -Name "MyResourceGroup" -Force
```

## Virtual Machine Lifecycle
### Create a Virtual Machine
```powershell
New-AzVm -ResourceGroupName "MyResourceGroup" -Name "MyVM" -Location "EastUS" -Image "Win2019Datacenter" -Credential (Get-Credential)
```
### Stop a Virtual Machine
```powershell
Stop-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM" -Force
```
### Start a Virtual Machine
```powershell
Start-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM"
```
### Deallocate a Virtual Machine
```powershell
Stop-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM" -Deallocate
```
### Delete a Virtual Machine
```powershell
Remove-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM"
```

## Storage Account Lifecycle
### Create a Storage Account
```powershell
New-AzStorageAccount -ResourceGroupName "MyResourceGroup" -AccountName "mystorage$(Get-Random)" -Location "EastUS" -SkuName "Standard_LRS" -Kind "StorageV2" -AccessTier "Cool"
```
### Delete a Storage Account
```powershell
Remove-AzStorageAccount -ResourceGroupName "MyResourceGroup" -AccountName "mystorageAccountName"
```

## BLOB Container Lifecycle
### Create a BLOB
```powershell
$ctx = (Get-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorageAccountName").Context; New-AzStorageContainer -Name "myContainer" -Context $ctx
```
### Delete a BLOB
```powershell
Remove-AzStorageContainer -Name "myContainer" -Context $ctx
```

## File Share Lifecycle
### Create a File Share
```powershell
New-AzStorageShare -Name "myFileShare" -Context $ctx
```
### Delete a File Share
```powershell
Remove-AzStorageShare -Name "myFileShare" -Context $ctx
```

## Queue Lifecycle
### Create a Queue
```powershell
New-AzStorageQueue -Name "myQueue" -Context $ctx
```
### Delete a Queue
```powershell
Remove-AzStorageQueue -Name "myQueue" -Context $ctx
```

## Table Lifecycle
### Create a Table
```powershell
New-AzStorageTable -Name "myTable" -Context $ctx
```
### Delete a Table
```powershell
Remove-AzStorageTable -Name "myTable" -Context $ctx
```

## Azure App Service Management using PowerShell

This guide provides an overview of how to manage Azure App Service Plans and Web Apps using PowerShell cmdlets.

## 1. App Service Plan Management

### Create a New App Service Plan
```powershell
New-AzAppServicePlan -Name tempappplan -ResourceGroupName rg_temp -Location eastus -Tier Free
```

### Retrieve App Service Plan Details
```powershell
Get-AzAppServicePlan -ResourceGroupName rg_temp
```

### Modify an Existing App Service Plan
```powershell
Set-AzAppServicePlan -ResourceGroupName rg_temp -Name tempappplan -Tier Standard -WorkerSize Small
```

### Delete an App Service Plan
```powershell
Remove-AzAppServicePlan -ResourceGroupName rg_temp -Name tempappplan
```

## 2. Web App Management

### Create a New Web App
```powershell
New-AzWebApp -Name tempwebapp -ResourceGroupName rg_temp -AppServicePlan tempappplan
```

### Retrieve Web App Details
```powershell
Get-AzWebApp -ResourceGroupName rg_temp -Name tempwebapp
```

### Update Web App Settings
```powershell
Set-AzWebApp -ResourceGroupName rg_temp -Name tempwebapp -HttpsOnly $true
```

### Delete a Web App
```powershell
Remove-AzWebApp -ResourceGroupName rg_temp -Name tempwebapp
```

### Start or Stop a Web App
```powershell
Start-AzWebApp -ResourceGroupName rg_temp -Name tempwebapp
Stop-AzWebApp -ResourceGroupName rg_temp -Name tempwebapp
```

### Restart a Web App
```powershell
Restart-AzWebApp -ResourceGroupName rg_temp -Name tempwebapp
```

## 3. Configuration and Deployment Management

### Create a Deployment Slot
```powershell
New-AzWebAppSlot -ResourceGroupName rg_temp -Name tempwebapp -Slot staging
```

### Set Slot Configuration
```powershell
Set-AzWebAppSlotConfigName -ResourceGroupName rg_temp -Name tempwebapp -Slot staging -AppSettingNames "MySetting"
```

### Swap Deployment Slots
```powershell
Set-AzWebAppSlotSwap -ResourceGroupName rg_temp -Name tempwebapp -SourceSlotName staging -DestinationSlotName production
```

### Retrieve Publishing Profile
```powershell
Get-AzWebAppPublishingProfile -ResourceGroupName rg_temp -Name tempwebapp
```

## 4. Scaling and Diagnostic Management

### Set Autoscaling Rules
```powershell
Set-AzWebAppScaleRule -ResourceGroupName rg_temp -Name tempwebapp -CpuPercentage 80 -InstanceCount 3
```

### Retrieve Diagnostic Settings
```powershell
Get-AzWebAppDiagnosticSetting -ResourceGroupName rg_temp -Name tempwebapp
```

### Configure Diagnostic Settings
```powershell
Set-AzWebAppDiagnosticSetting -ResourceGroupName rg_temp -Name tempwebapp -ApplicationLogging $true
```
