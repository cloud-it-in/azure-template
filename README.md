# azure-template
Collection of Azure .json template for deployments

# Vnet with 3 subnets - # .json deployment template ( vnet with 3 subnet)
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "virtualNetworks_vnet_cloud_it_in_name": {
            "defaultValue": "vnet-cloud-it-in",
            "type": "String"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Network/virtualNetworks",
            "apiVersion": "2019-11-01",
            "name": "[parameters('virtualNetworks_vnet_cloud_it_in_name')]",
            "location": "eastus",
            "tags": {
                "Vnet Name": "cloud-it-in"
            },
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "10.0.0.0/16"
                    ]
                },
                "subnets": [
                    {
                        "name": "cloud-it-in-subnet1",
                        "properties": {
                            "addressPrefix": "10.0.0.0/24",
                            "delegations": [],
                            "privateEndpointNetworkPolicies": "Enabled",
                            "privateLinkServiceNetworkPolicies": "Enabled"
                        }
                    },
                    {
                        "name": "cloud-it-in-subnet2",
                        "properties": {
                            "addressPrefix": "10.0.1.0/24",
                            "delegations": [],
                            "privateEndpointNetworkPolicies": "Enabled",
                            "privateLinkServiceNetworkPolicies": "Enabled"
                        }
                    },
                    {
                        "name": "cloud-it-in-subnet3",
                        "properties": {
                            "addressPrefix": "10.0.2.0/24",
                            "delegations": [],
                            "privateEndpointNetworkPolicies": "Enabled",
                            "privateLinkServiceNetworkPolicies": "Enabled"
                        }
                    }
                ],
                "virtualNetworkPeerings": [],
                "enableDdosProtection": false,
                "enableVmProtection": false
            }
        },
        {
            "type": "Microsoft.Network/virtualNetworks/subnets",
            "apiVersion": "2019-11-01",
            "name": "[concat(parameters('virtualNetworks_vnet_cloud_it_in_name'), '/cloud-it-in-subnet1')]",
            "dependsOn": [
                "[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_vnet_cloud_it_in_name'))]"
            ],
            "properties": {
                "addressPrefix": "10.0.0.0/24",
                "delegations": [],
                "privateEndpointNetworkPolicies": "Enabled",
                "privateLinkServiceNetworkPolicies": "Enabled"
            }
        },
        {
            "type": "Microsoft.Network/virtualNetworks/subnets",
            "apiVersion": "2019-11-01",
            "name": "[concat(parameters('virtualNetworks_vnet_cloud_it_in_name'), '/cloud-it-in-subnet2')]",
            "dependsOn": [
                "[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_vnet_cloud_it_in_name'))]"
            ],
            "properties": {
                "addressPrefix": "10.0.1.0/24",
                "delegations": [],
                "privateEndpointNetworkPolicies": "Enabled",
                "privateLinkServiceNetworkPolicies": "Enabled"
            }
        },
        {
            "type": "Microsoft.Network/virtualNetworks/subnets",
            "apiVersion": "2019-11-01",
            "name": "[concat(parameters('virtualNetworks_vnet_cloud_it_in_name'), '/cloud-it-in-subnet3')]",
            "dependsOn": [
                "[resourceId('Microsoft.Network/virtualNetworks', parameters('virtualNetworks_vnet_cloud_it_in_name'))]"
            ],
            "properties": {
                "addressPrefix": "10.0.2.0/24",
                "delegations": [],
                "privateEndpointNetworkPolicies": "Enabled",
                "privateLinkServiceNetworkPolicies": "Enabled"
            }
        }
    ]
}



# Custom Script Extensions - To Install ISS on VM through Custome Script Extentions

Create a new file as "InstallIIS.ps1" and place the following commands in the file:

import-module servermanager
add-windowsfeature web-server -includeallsubfeature
>> Go to Extention >> Choose Custom Script >> ( Poweshell Custom Script"
>> Attach and upload the file and execute.

** Please note of the scripts have reboots as a part of the script, it is not ideal to do it through extention. The alternate ways would be through DSC ( Desired State Configuration) or use other tools like Chef / Puppet.



# Custom Script Extensions for Linux Virtual Machines - Practice commands

// Apply custom script extensions for a Linux Virtual Machine

az vm extension set --resource-group azuredemo --vm-name linuxvm --name customScript --publisher Microsoft.Azure.Extensions --settings customscript.json

This chapter has the configuration file attached as a resource. Please ensure you have a GitHub account and attach the URL for your account.

In the GitHub account , create a repository and add a file named install_web.sh1 that has the following contents

apt-get update -y && apt-get upgrade -y

apt-get install -y nginx


# Alternate method is cloud-init for Linux VM
make a yaml script file

#cloud-config
package_upgrade: true
packages:
  - nginx
  
  
# Poweshell DSC  (Desired state configuration)
Make a Poweshell Scrift fule PS1
