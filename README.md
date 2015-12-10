# Azure-CLI-VMSS
Azure CLI VM Scale Sets (VMSS) 

We recently released VM Scale Sets (VMSS) for public preview and we would love you folks to help us beta test the new Azure VMSS commands that have been added to the Azure CLI tool. 

With the new build, you can perform simple operations directly on scale sets or individual VM’s within scale sets. Below is a simple example, 

Usage: azure vmss quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>

Example: azure vmss quick-create -g testrg -n test -l westus -Q MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:2.0.20151022  -u usr -p pwd

Usage: azure vmss delete --resource-group-name %rgname% --vm-scale-set-name %vmssname%

Please see the document in this repository for debugging installation issues and sample scenarios to run.

Please raise issues in this repository for any feedback you may have.

