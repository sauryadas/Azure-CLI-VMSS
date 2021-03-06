VMSS using a parameter file

Scenario – Create a VMSS using the parameter file

1)	Run the following commands to set up your storage account and network information.
> azure group create %rgname% %locname%
> azure storage account create -l %locname% -g %rgname% %stoname% --type GRS
> azure network vnet create -vv %rgname% %vnetname% %locname% 
> azure network public-ip create -vv %rgname% subnet %locname% 
> azure network vnet subnet create --vnet-name %vnetname% -vv %rgname% %subnetname% %locname% 
> azure network nic create --subnet-name %subnetname% --subnet-vnet-name %vnetname% -vv %rgname% %nicname% %locname%


2)	Copy paste the following text into a file called input.json or simply use 
100-VMSS-CreateUsingParameterFile-Input.json in the repository. This is essentially setting all your VMSS configurations in a json file. 

Edit the following highlighted lines with all your configuration information from Step 1
    {
      "provisioningState": null,
      "sku": {
        "capacity": "2",
        "name": "Standard_A0",
        "tier": "Standard"
      },
      "upgradePolicy": {
        "mode": "Manual"
      },
      "virtualMachineProfile": {
        "networkProfile": {
          "networkInterfaceConfigurations": [
            {
              "iPConfigurations": [
                {
                  "name": "test",
                  "subnet": {
                    "referenceUri": "/subscriptions/<your-subscriptionid>/resourceGroups/<your-resourceGroupName>/providers/Microsoft.Network/virtualNetworks/<your-virtualNetworkName>/subnets/<your-subnetName>"
                  }
                }
              ],
              "name": "test",
              "primary": "true"
            }
          ]
        },
        "oSProfile": {
          "computerNamePrefix": "test",
          "adminPassword": "xxx",
          "adminUsername": "xxx",
          "customData": null
        },
        "storageProfile": {
          "imageReference": {
            "offer": "WindowsServer",
            "publisher": "MicrosoftWindowsServer",
            "sku": "2008-R2-SP1",
            "version": "2.0.201506"
          },
          "oSDisk": {
            "caching": "None",
            "createOption": "FromImage",
            "name": "test",
            "operatingSystemType": null,
            "virtualHardDiskContainers": [
              "https://<your-storageAccountName>.blob.core.windows.net/test"
            ]
          }
        }
      },
      "id": "",
      "name": "test3vmss",
      "type": "",
      "location": "southeastasia",
      "tags": {}
    }


3)Run the following command with the right parameters
> azure vmss create-or-update --resource-group-name %rgname% --parameter-file %filename%
