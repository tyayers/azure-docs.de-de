---
title: Überprüfen des Datenverkehrs mit der IP-Datenflussüberprüfung in Azure Network Watcher – Azure CLI | Microsoft-Dokumentation
description: Dieser Artikel beschreibt, wie Sie mithilfe der Azure CLI überprüfen, ob bei einem virtuellen Computer eingehender und ausgehender Datenverkehr zugelassen oder verweigert wird.
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: b7122b632dca99eba6fae058beb644f945f67872
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2018
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Überprüfen mit der IP-Datenflussüberprüfung (einer Komponente von Azure Network Watcher), ob bei einem virtuellen Computer eingehender und ausgehender Datenverkehr zugelassen oder verweigert wird

> [!div class="op_single_selector"]
> - [Azure-Portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure-REST-API](network-watcher-check-ip-flow-verify-rest.md)


Die IP-Datenflussüberprüfung ist ein Feature von Network Watcher, mit dem Sie überprüfen können, ob bei einem virtuellen Computer eingehender oder ausgehender Datenverkehr zugelassen wird. Dieses Szenario eignet sich zum Abrufen des aktuellen Status der Kommunikation eines virtuellen Computers mit einer externen Ressource oder einem Back-End. Anhand der IP-Datenflussüberprüfung können Sie überprüfen, ob die NSG-Regeln (Netzwerksicherheitsgruppe) ordnungsgemäß konfiguriert sind, und eine Problembehandlung für Datenflüsse durchführen, die durch die NSG-Regeln blockiert werden. Ein weiterer Grund für die Verwendung der IP-Datenflussüberprüfung besteht darin sicherzustellen, dass Datenverkehr, der blockiert werden soll, durch die NSG ordnungsgemäß blockiert wird.

In diesem Artikel wird unsere Befehlszeilenschnittstelle der nächsten Generation für das Resource Manager-Bereitstellungsmodell verwendet, Azure CLI 2.0, die für Windows, Mac und Linux verfügbar ist.

Um die Schritte in diesem Artikel ausführen zu können, müssen Sie [die Azure-Befehlszeilenschnittstelle für Mac, Linux und Windows (Azure CLI) installieren](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Voraussetzungen

Dieses Szenario setzt voraus, dass Sie die Schritte unter [Erstellen einer Network Watcher-Instanz](network-watcher-create.md) bereits durchgeführt haben, um eine Network Watcher-Instanz zu erstellen, bzw. dass Sie eine vorhandene Instanz von Network Watcher verwenden. Ferner wird davon ausgegangen, dass eine Ressourcengruppe mit einem gültigen virtuellen Computer vorhanden ist und verwendet werden kann.

## <a name="scenario"></a>Szenario

Dieses Szenario verwendet die IP-Datenflussüberprüfung, um zu überprüfen, ob ein virtueller Computer mit einer bekannten Bing-IP-Adresse kommunizieren kann. Wenn der Datenverkehr abgelehnt wird, wird die Sicherheitsregel zurückgegeben, die den jeweiligen Datenverkehr verweigert. Weitere Informationen zur IP-Datenflussüberprüfung finden Sie in der [Übersicht zur IP-Datenflussüberprüfung](network-watcher-ip-flow-verify-overview.md).

## <a name="get-a-vm"></a>Abrufen eines virtuellen Computers

Die IP-Datenflussüberprüfung testet den bei einer IP-Adresse eines virtuellen Computers eingehenden oder ausgehenden Datenverkehr von einem bzw. an ein Remoteziel. Eine ID eines virtuellen Computers ist zum Ausführen des Cmdlets erforderlich. Wenn Sie die ID des virtuellen Computers bereits kennen, können Sie diesen Schritt überspringen.

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-the-nics"></a>Abrufen der NICs

Die IP-Adresse eines Netzwerkadapters auf dem virtuellen Computer ist erforderlich. Rufen Sie mit dem folgenden Befehl die an den virtuellen Computer angefügten Netzwerkadapter ab. Wenn Sie die IP-Adresse bereits kennen, die Sie auf dem virtuellen Computer testen möchten, können Sie diesen Schritt überspringen.

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a>Ausführen der IP-Datenflussüberprüfung

Führen Sie das Cmdlet `az network watcher test-ip-flow` aus, um den Datenverkehr zu testen. In diesem Beispiel wird die erste IP-Adresse des ersten Netzwerkadapters verwendet.

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> Für die IP-Datenflussüberprüfung ist es erforderlich, dass die VM-Ressource für die Ausführung zugeordnet wird.

## <a name="review-results"></a>Überprüfen der Ergebnisse

Nach der Ausführung von `az network watcher test-ip-flow` werden die Ergebnisse zurückgegeben. Das folgende Beispiel zeigt die im vorhergehenden Schritt zurückgegebenen Ergebnisse.

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a>Nächste Schritte

Wenn Datenverkehr fälschlicherweise blockiert wird, finden Sie unter [Verwalten von Netzwerksicherheitsgruppen](../virtual-network/manage-network-security-group.md) Informationen zum Ermitteln der Netzwerksicherheitsgruppe und der definierten Sicherheitsregeln.

Informationen zur Überwachung Ihrer NSG-Einstellungen finden Sie unter [Überwachen von Netzwerksicherheitsgruppen (NSG) mit Network Watcher](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
