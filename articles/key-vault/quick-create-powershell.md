---
title: 'Azure-Schnellstart: Erstellen einer Key Vault-Instanz – PowerShell | Microsoft-Dokumentation'
description: ''
services: key-vault
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: ''
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.custom: mvc
ms.date: 04/18/2018
ms.author: barclayn
ms.openlocfilehash: e980eafc5bd70a15de11239c7543a7f1dde4ef64
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2018
---
# <a name="quickstart-create-an-azure-key-vault-using-powershell"></a>Schnellstart: Erstellen einer Azure Key Vault-Instanz mit PowerShell

Azure Key Vault ist ein Clouddienst, der als sicherer Geheimnisspeicher fungiert. Dadurch können Schlüssel, Kennwörter, Zertifikate und andere Geheimnisse sicher gespeichert werden. Weitere Informationen zu Key Vault finden Sie in der [Übersicht](key-vault-overview.md). In dieser Schnellstartanleitung erstellen Sie einen Schlüsseltresor mithilfe von PowerShell. Anschließend speichern Sie ein Geheimnis in dem neu erstellten Tresor.

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

Wenn Sie PowerShell lokal installieren und verwenden möchten, müssen Sie für dieses Tutorial mindestens Version 5.1.1 des Azure PowerShell-Moduls verwenden. Führen Sie `Get-Module -ListAvailable AzureRM` aus, um die Version zu finden. Wenn Sie ein Upgrade ausführen müssen, finden Sie unter [Installieren des Azure PowerShell-Moduls](/powershell/azure/install-azurerm-ps) Informationen dazu. Wenn Sie PowerShell lokal ausführen, müssen Sie auch `Login-AzureRmAccount` ausführen, um eine Verbindung mit Azure herzustellen.

```azurepowershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Erstellen Sie mit [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) eine Azure-Ressourcengruppe. Eine Ressourcengruppe ist ein logischer Container, in dem Azure-Ressourcen bereitgestellt und verwaltet werden. 

```azurepowershell
New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS
```

## <a name="create-a-key-vault"></a>Erstellen eines Schlüsseltresors

Als Nächstes erstellen Sie eine Key Vault-Instanz. Für diesen Schritt benötigen Sie einige Informationen:

In dieser Schnellstartanleitung lautet der Name für die Key Vault-Instanz zwar „Contoso KeyVault2“, Sie müssen jedoch einen eindeutigen Namen verwenden.

- **Tresorname:** Contoso-Vault2
- **Ressourcengruppenname:** ContosoResourceGroup
- **Standort:** USA, Osten

```azurepowershell
New-AzureRmKeyVault -VaultName 'Contoso-Vault2' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
```

Die Ausgabe dieses Cmdlets zeigt Eigenschaften des neu erstellten Schlüsseltresors. Beachten Sie die beiden folgenden Eigenschaften:

* **Tresorname:** In diesem Beispiel wird **Contoso-Vault2** verwendet. Sie verwenden diesen Namen für andere Schlüsseltresor-Cmdlets.
* **Tresor-URI:** https://contosokeyvault.vault.azure.net/ in diesem Beispiel. Anwendungen, die Ihren Tresor über die zugehörige REST-API nutzen, müssen diesen URI verwenden.

Nach der Tresorerstellung ist Ihr Azure-Konto das einzige Konto, das zum Ausführen von Vorgängen für diesen neuen Tresor berechtigt ist.

![Ausgabe nach Abschluss des Befehls zur Erstellung des Schlüsseltresors](./media/quick-create-powershell/output-after-creating-keyvault.png)

## <a name="adding-a-secret-to-key-vault"></a>Hinzufügen eines Geheimnisses zu Key Vault

Ein Geheimnis kann dem Tresor mit wenigen Schritten hinzugefügt werden. In diesem Fall wird ein Kennwort hinzugefügt, das von einer Anwendung verwendet werden kann. Das Kennwort heißt **ExamplePassword** und enthält den Wert **Pa$$w0rd**.

Geben Sie zunächst Folgendes ein, um den Wert „Pa$$w0rd“ in eine sichere Zeichenfolge zu konvertieren:

```azurepowershell
$secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force
```

Geben Sie dann die folgenden PowerShell-Befehle ein, um in Key Vault ein Geheimnis namens **ExamplePassword** mit dem Wert **Pa$$w0rd** zu erstellen:

```azurepowershell
$secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'ExamplePassword' -SecretValue $secretvalue
```

Geben Sie Folgendes ein, um den Wert im Geheimnis als Nur-Text anzuzeigen:

```azurepowershell
(get-azurekeyvaultsecret -vaultName "Contosokeyvault" -name "ExamplePassword").SecretValueText
```

Sie haben nun eine Key Vault-Instanz erstellt sowie ein Geheimnis gespeichert und abgerufen.

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

 Andere Schnellstartanleitungen und Tutorials in dieser Sammlung bauen auf dieser Schnellstartanleitung auf. Falls Sie mit weiteren Schnellstartanleitungen und Tutorials fortfahren möchten, sollten Sie die Ressourcen nicht bereinigen.

Wenn Sie die Ressourcen nicht mehr benötigen, führen Sie den Befehl [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) aus, um die Ressourcengruppe, die Key Vault-Instanz und alle dazugehörigen Ressourcen zu löschen.

```azurepowershell
Remove-AzureRmResourceGroup -Name ContosoResourceGroup
```

## <a name="next-steps"></a>Nächste Schritte

In dieser Schnellstartanleitung haben Sie eine Key Vault-Instanz erstellt und einen Softwareschlüssel darin gespeichert. Das Tutorial zu Webanwendungen mit Key Vault enthält weitere Informationen zu Key Vault und zur Verwendung mit Ihren Anwendungen.

> [!div class="nextstepaction"]
> [Verwenden des Azure-Schlüsseltresors aus einer Webanwendung](key-vault-use-from-web-application.md)
