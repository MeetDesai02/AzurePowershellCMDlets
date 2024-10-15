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





