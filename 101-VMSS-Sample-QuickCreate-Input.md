Azure CLI for VMSS � Quick create VMSS

Scenario - Quick create a VM, attach an extension and delete the VMSS

1)	Quick Create a VMSS using the following command
> azure vmss quick-create --resource-group-name %rgname% --name %vmssname% --location %locname% --admin-username %admin-username% --admin-password %admin-password% -- image-urn %publisherName:offer:skus:version%

Example: > azure vmss quick-create -g testrg -n test -l westus -Q MicrosoftWindowsServer:WindowsServer:2008-R2-SP1:2.0.20151022  -u usr -p pwd			

2)	View the VMSS you just created
>  azure vmss list-all
> azure vmssvm list --resource-group-name %rgname% --virtual-machine-scale-set-name %vmssname%

3)	Attach a Docker extension to your VMSS
Create a parameter-file <name>.json and copy paste the following OR simply use the 
101-VMSS- QuickCreate-Input.json in the repository 

Update the name of the VMSS and location in the file
    {
      "virtualMachineProfile": {
        "extensionProfile": {
          "extensions": [
            {
              "autoUpgradeMinorVersion": false,
              "extensionType": "DockerExtension",
              "protectedSettings": "",
              "provisioningState": "",
              "publisher": "Microsoft.Azure.Extensions",
              "settings": "",
              "typeHandlerVersion": "1.0",
              "name": "test",
              "location":  "westus"
            }
          ]
        }
      },
      "name": "<Your VMSS name>",
      "location": "<Location of your VMSS>"
    }

Run the following command:

> azure vmss create-or-update --resource-group-name %rgname% --parameter-file %filename%

Navigate to this link to view your resource group and then go all the way down to the VMSS you just created to see the extension added. Please see below.


4)	Delete a VM
> azure vmss delete --resource-group-name %rgname% --vm-scale-set-name %vmssname%