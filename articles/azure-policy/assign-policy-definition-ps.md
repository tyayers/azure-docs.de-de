---
title: 'Schnellstartanleitung: Erstellen einer Richtlinienzuweisung zum Identifizieren nicht konformer Ressourcen in Ihrer Azure-Umgebung mithilfe von PowerShell | Microsoft-Dokumentation'
description: In dieser Schnellstartanleitung erstellen Sie mithilfe von PowerShell eine Azure Policy-Zuweisung zum Identifizieren nicht konformer Ressourcen.
services: azure-policy
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 04/10/2018
ms.topic: quickstart
ms.service: azure-policy
ms.custom: mvc
ms.openlocfilehash: 5fa6db380d790e002aa43b19fe77f4fc3c39b7da
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="quickstart-create-a-policy-assignment-to-identify-non-compliant-resources-using-the-azure-rm-powershell-module"></a>Schnellstartanleitung: Erstellen einer Richtlinienzuweisung zum Identifizieren nicht konformer Ressourcen mithilfe des Azure RM-PowerShell-Moduls

Zum Verständnis der Konformität in Azure müssen Sie zunächst wissen, wie Sie den Status Ihrer Ressourcen ermitteln. Im Rahmen dieser Schnellstartanleitung erstellen Sie eine Richtlinienzuweisung zur Identifizierung von virtuellen Computern, die keine verwalteten Datenträger verwenden. Im Anschluss identifizieren Sie virtuelle Computer, die mit der Richtlinienzuweisung *nicht konform* sind.

Mit dem AzureRM-PowerShell-Modul werden Azure-Ressourcen über die Befehlszeile oder in Skripts erstellt und verwaltet. In dieser Anleitung erfahren Sie, die Sie mit AzureRM eine Richtlinienzuordnung erstellen. Die Richtlinie identifiziert nicht konforme Ressourcen in Ihrer Azure-Umgebung.

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/) erstellen, bevor Sie beginnen.

## <a name="prerequisites"></a>Voraussetzungen

- Stellen Sie vor Beginn sicher, dass die aktuelle Version von PowerShell installiert ist. Ausführliche Informationen finden Sie unter [Installieren und Konfigurieren von Azure PowerShell](/powershell/azureps-cmdlets-docs).
- Aktualisieren Sie Ihr AzureRM-PowerShell-Modul auf die neueste Version. Wenn Sie eine Installation oder ein Upgrade ausführen müssen, finden Sie unter [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps) (Installieren des Azure PowerShell-Moduls) Informationen dazu.
- Registrieren Sie den Ressourcenanbieter Policy Insights mithilfe von Azure PowerShell. Durch die Registrierung des Ressourcenanbieters wird sichergestellt, dass das Abonnement mit ihm verwendet werden kann. Um einen Ressourcenanbieter zu registrieren, benötigen Sie die Berechtigungen zum Ausführen des Vorgangs „Aktion registrieren“ für den Ressourcenanbieter. Dieser Vorgang ist in den Rollen „Mitwirkender“ und „Besitzer“ enthalten. Führen Sie den folgenden Befehl aus, um den Ressourcenanbieter zu registrieren:

  ```
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.PolicyInsights
  ```

  Weitere Informationen zum Registrieren und Anzeigen von Ressourcenanbietern finden Sie unter [Ressourcenanbieter und -typen](../azure-resource-manager/resource-manager-supported-services.md).

## <a name="create-a-policy-assignment"></a>Erstellen einer Richtlinienzuweisung

In dieser Schnellstartanleitung erstellen Sie eine Richtlinienzuweisung und weisen die Definition *Audit Virtual Machines without Managed Disks* (Virtuelle Computer ohne verwaltete Datenträger überwachen) zu. Mit dieser Richtliniendefinition werden Ressourcen identifiziert, die die in der Richtliniendefinition festgelegten Bedingungen nicht erfüllen.

Führen Sie die folgenden Befehle aus, um eine neue Richtlinienzuweisung zu erstellen:

```powershell
$rg = Get-AzureRmResourceGroup -Name "<resourceGroupName>"
$definition = Get-AzureRmPolicyDefinition | where {$_.properties.displayName -eq "Audit VMs that do not use managed disks"}
New-AzureRMPolicyAssignment -Name "Audit Virtual Machines without Managed Disks" -Scope $rg.ResourceId -PolicyDefinition $definition -Sku @{Name='A1';Tier='Standard'}
```

In diesen Befehlen werden folgende Informationen verwendet:

- **Name:** Der Anzeigename für die Richtlinienzuweisung. Verwenden Sie in diesem Fall *Audit Virtual Machines without Managed Disks Assignment* (Zuweisung für die Überwachung virtueller Computer ohne verwaltete Datenträger).
- **Definition:** Die Richtliniendefinition, auf deren Grundlage Sie die Zuweisung erstellen. In diesem Fall ist es die Richtliniendefinition: *Audit Virtual Machines without Managed Disks* (Virtuelle Computer ohne verwaltete Datenträger überwachen).
- **Bereich:** Ein Bereich bestimmt, für welche Ressourcen oder Ressourcengruppe die Richtlinienzuweisung erzwungen wird. Er kann von einem Abonnement bis zu Ressourcengruppen reichen. Ersetzen Sie &lt;scope&gt; durch den Namen Ihrer Ressourcengruppe.
- **SKU:** Dieser Befehl erstellt eine Richtlinienzuweisung mit dem Standard-Tarif. Der Standard-Tarif ermöglicht eine skalierbare Verwaltung, Compliancebewertung und Problembehandlung. Weitere Details zu Tarifen finden Sie auf der [Preisseite für Azure Policy](https://azure.microsoft.com/pricing/details/azure-policy).


Sie können nun nicht konforme Ressourcen identifizieren, um den Konformitätszustand Ihrer Umgebung nachzuvollziehen.

## <a name="identify-non-compliant-resources"></a>Identifizieren nicht konformer Ressourcen

Verwenden Sie folgende Informationen, um Ressourcen zu identifizieren, die mit der erstellten Richtlinienzuweisung nicht konform sind. Führen Sie die folgenden Befehle aus:

```powershell
$policyAssignment = Get-AzureRmPolicyAssignment | where {$_.properties.displayName -eq "Audit Virtual Machines without Managed Disks"}
```

```powershell
$policyAssignment.PolicyAssignmentId
```

Weitere Informationen zu Richtlinienzuweisungs-IDs finden Sie unter [Get-AzureRMPolicyAssignment](/powershell/module/azurerm.resources/get-azurermpolicyassignment).

Führen Sie als Nächstes den folgenden Befehl aus, um die Ressourcen-IDs der nicht konformen Ressourcen abzurufen, die in einer JSON-Datei ausgegeben werden:

```powershell
armclient post "/subscriptions/<subscriptionID>/resourceGroups/<rgName>/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2017-12-12-preview&$filter=IsCompliant eq false and PolicyAssignmentId eq '<policyAssignmentID>'&$apply=groupby((ResourceId))" > <json file to direct the output with the resource IDs into>
```
Ihre Ergebnisse sollten in etwa wie im folgenden Beispiel aussehen:


```
{
"@odata.context":"https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest",
"@odata.count": 3,
"value": [
{
    "@odata.id": null,
    "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
      "ResourceId": "/subscriptions/<subscriptionId>/resourcegroups/<rgname>/providers/microsoft.compute/virtualmachines/<virtualmachineId>"
    },
    {
      "@odata.id": null,
      "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
      "ResourceId": "/subscriptions/<subscriptionId>/resourcegroups/<rgname>/providers/microsoft.compute/virtualmachines/<virtualmachine2Id>"
         },
{
      "@odata.id": null,
      "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
      "ResourceId": "/subscriptions/<subscriptionName>/resourcegroups/<rgname>/providers/microsoft.compute/virtualmachines/<virtualmachine3ID>"
         }

]
}
```

Die Ergebnisse sind vergleichbar mit dem, was üblicherweise in der Azure-Portalansicht unter **Nicht konforme Ressourcen** zu sehen ist.


## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Nachfolgende Anleitungen in dieser Sammlung bauen auf diesem Schnellstart auf. Wenn Sie mit weiteren Tutorials fortfahren möchten, sollten Sie die in diesem Schnellstart erstellten Ressourcen nicht bereinigen. Wenn Sie nicht fortfahren möchten, können Sie die erstellte Zuweisung mit dem folgenden Befehl löschen:

```powershell
Remove-AzureRmPolicyAssignment -Name "Audit Virtual Machines without Managed Disks Assignment" -Scope /subscriptions/<subscriptionID>/<resourceGroupName>
```

## <a name="next-steps"></a>Nächste Schritte

In diesem Schnellstart haben Sie eine Richtliniendefinition zum Identifizieren nicht kompatibler Ressourcen in Ihrer Azure-Umgebung zugewiesen.

Weitere Informationen zum Zuweisen von Richtlinien, die die Konformität **zukünftig** erstellter Ressourcen sicherstellen, finden Sie im folgenden Tutorial:

> [!div class="nextstepaction"]
> [Erstellen und Verwalten von Richtlinien](./create-manage-policy.md)
