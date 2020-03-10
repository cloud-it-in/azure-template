# azure-template
Collection of Azure .jason template for deployments
# .jason deployment template ( vnet with 3 subnet)
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
