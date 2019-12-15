
# Provision VMs

What you need to know

* How to provision a Windows VM using the portal
* Provision a Linux VM using the portal
* Provision Linux and Windows VMs using PowerShell
* Provision Linux and Windows VMs using the CLI
* Provision Linux and Windows VMs using an ARM template

## Windows VMs

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli

https://docs.microsoft.com/en-us/azure/virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-quick

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/tutorial-manage-vm

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/csharp

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/powershell-samples

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/template-description

https://docs.microsoft.com/en-us/azure/virtual-machines/windows/ps-template

## Linux VMs

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-powershell

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/powershell-samples

https://docs.microsoft.com/en-us/azure/virtual-machines/linux/create-ssh-secured-vm-from-template


## PLuralsight

https://app.pluralsight.com/library/courses/microsoft-azure-deploying-multiple-virtual-machines/table-of-contents


## Windows VM via CLI

[quick start](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli)

`az group create --name cli-vms --location eastus`

`az vm create \
    --resource-group cli-vms \
    --name cli-vm \
    --image win2016datacenter \
    --admin-username azureuser \
    --admin-password pass@word1pass@word1`

By default, only RDP connections are opened when you create a Windows VM in Azure. Use az vm open-port to open TCP port 80 for use with the IIS web server:

`az vm open-port --port 80 --resource-group cli-vms --namecli-vm`

RDP into VM, and run in PowerShell
`Install-WindowsFeature -name Web-Server -IncludeManagementTools`

clean up

`az group delete --name cli-vms`

## Windows VM using PowerShell

simple:

`New-AzVM `
  -ResourceGroupName $resourceGroup `
  -Name $vmName `
  -Location $location `
  -ImageName "Win2016Datacenter" `
  -VirtualNetworkName "myVnet" `
  -SubnetName "mySubnet" `
  -SecurityGroupName "myNetworkSecurityGroup" `
  -PublicIpAddressName "myPublicIp" `
  -Credential $cred `
  -OpenPorts 3389`

fully configured

`# Variables for common values
$resourceGroup = "myResourceGroup"
$location = "westeurope"
$vmName = "myVM"

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

New-AzResourceGroup -Name $resourceGroup -Location $location

$subnetConfig = New-AzVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzVirtualNetwork -ResourceGroupName $resourceGroup -Location $location `
  -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

$pip = New-AzPublicIpAddress -ResourceGroupName $resourceGroup -Location $location `
  -Name "mypublicdns$(Get-Random)" -AllocationMethod Static -IdleTimeoutInMinutes 4

$nsgRuleRDP = New-AzNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
  -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
  -DestinationPortRange 3389 -Access Allow

$nsg = New-AzNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
  -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP

$nic = New-AzNetworkInterface -Name myNic -ResourceGroupName $resourceGroup -Location $location `
  -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzVMOperatingSystem -Windows -ComputerName $vmName -Credential $cred | `
Set-AzVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzVMNetworkInterface -Id $nic.Id

New-AzVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig`