---
title: Creare i gruppi di sicurezza di rete - interfaccia della riga di comando di Azure | Microsoft Docs
description: Informazioni su come creare e distribuire i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure.
services: virtual-network
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4827fabf1d8cde366dda8b3a782a2fefe01db8d5
ms.sourcegitcommit: 34e0b4a7427f9d2a74164a18c3063c8be967b194
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/31/2018
---
# <a name="create-network-security-groups-using-the-azure-cli"></a>Creare i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

I comandi di esempio dell'interfaccia della riga di comando di Azure riportati di seguito prevedono un ambiente semplice esistente in base allo scenario precedente. 

## <a name="create-the-nsg-for-the-frontend-subnet"></a>Creare il gruppo di sicurezza di rete per la subnet `FrontEnd`

Per creare un gruppo di sicurezza di rete denominato *NSG-FrontEnd* in base allo scenario precedente, seguire la procedura seguente:

1. Se questa operazione non è stata ancora eseguita, installare e configurare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure usando il comando [az login](/cli/azure/reference-index#az_login). 

2. Creare un gruppo di sicurezza di rete usando il comando [azure network nsg create](/cli/azure/network/nsg#az_network_nsg_create). 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Parametri
   
   * `--resource-group`: nome del gruppo di risorse in cui viene creato il gruppo di sicurezza di rete. Per questo scenario, *TestRG*.
   * `--location`: area di Azure in cui viene creato il nuovo gruppo di sicurezza di rete. Per questo scenario, *westus*.
   * `--name`: nome per il nuovo gruppo di sicurezza di rete. Per questo scenario, *NSG-FrontEnd*.

    L'output previsto include svariate informazioni, tra cui un elenco di tutte le regole predefinite. L'esempio seguente mostra le regole predefinite usando un filtro di query JMESPATH con il formato di output `table`:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Output:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Creare una regola che consenta l'accesso alla porta 3389 (RDP) da Internet con il comando [azure network nsg rule create](/cli/azure/network/nsg/rule#az_network_nsg_rule_create).

    > [!NOTE]
    > A seconda della shell in uso potrebbe essere necessario modificare il carattere `*` negli argomenti seguenti per non espandere l'argomento prima dell'esecuzione.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    Output previsto:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    Parametri

    * `--resource-group testrg`: il gruppo di risorse da usare. Si noti che non fa distinzione tra maiuscole e minuscole.
    * `--nsg-name NSG-FrontEnd`: nome del gruppo di sicurezza di rete in cui viene creata la regola.
    * `--name rdp-rule`: nome per la nuova regola.
    * `--access Allow`: livello di accesso per la regola (Deny o Allow).
    * `--protocol Tcp`: protocollo (TCP, UDP o *).
    * `--direction Inbound`: direzione di connessione (Inbound o Outbound).
    * `--priority 100`: priorità per la regola.
    * `--source-address-prefix Internet`: prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.
    * `--source-port-range "*"`: porta o intervallo di porte di origine. Porta che ha aperto la connessione.
    * `--destination-address-prefix "*"`: prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.
    * `--destination-port-range 3389`: porta o intervallo di porte di destinazione. Porta che riceve la richiesta di connessione.



4. Creare una regola consenta l'accesso alla porta 80 (HTTP) da Internet con il comando **azure network nsg rule create**.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    Output previsto:
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. Associare il gruppo di sicurezza di rete alla subnet **FrontEnd** con il comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#az_network_vnet_subnet_update).
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Output previsto:
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-the-nsg-for-the-backend-subnet"></a>Creare il gruppo di sicurezza di rete per la subnet `BackEnd`
Per creare un gruppo di sicurezza di rete denominato *NSG-BackEnd* in base allo scenario precedente, seguire la procedura seguente.

1. Creare il gruppo di sicurezza di rete `NSG-BackEnd` con **az network nsg create**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    Come nel passaggio 2 precedente, l'output previsto contiene svariate informazioni, incluse le regole predefinite.
   
2. Creare una regola che consenta l'accesso alla porta 1433 (SQL) dalla subnet `FrontEnd` con il comando **az network nsg rule create**.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    Output previsto:

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. Creare una regola che neghi l'accesso a Internet usando il comando **az network nsg rule create**.
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    Output previsto:
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. Associare il gruppo di sicurezza di rete alla subnet `BackEnd` usando il comando **az network vnet subnet set**.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Output previsto:
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
