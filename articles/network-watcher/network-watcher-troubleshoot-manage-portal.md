---
title: Problembehandlung bei Azure Virtual Network-Gateways und -Verbindungen – Portal | Microsoft-Dokumentation
description: Auf dieser Seite wird erläutert, wie das Azure Network Watcher-Portal zur Problembehandlung verwendet wird.
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: jdial
ms.openlocfilehash: becc4f799e34aabba5c703f09e51a4b7d497c45a
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-network-watcher-from-azure-portal"></a>Problembehandlung bei Virtual Network-Gateways und -Verbindungen mit Azure Network Watcher im Azure-Portal

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST-API](network-watcher-troubleshoot-manage-rest.md)

Network Watcher bietet viele Funktionen zum Erfassen von Informationen über Ihre Netzwerkressourcen in Azure. Zu diesen Funktionen zählt die Ressourcenproblembehandlung. Die Ressourcenproblembehandlung kann über das Portal, PowerShell, die CLI oder die REST-API aufgerufen werden. Bei Aufruf untersucht Network Watcher die Integrität von Virtual Network-Gateways oder -Verbindungen und gibt entsprechende Ergebnisse zurück.

## <a name="before-you-begin"></a>Voraussetzungen

Dieses Szenario setzt voraus, dass Sie die Schritte unter [Erstellen einer Network Watcher-Instanz](network-watcher-create.md) bereits ausgeführt haben.

Eine Liste mit unterstützten Gatewaytypen finden Sie unter [Unterstützte Gatewaytypen](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Übersicht

Die Ressourcenproblembehandlung bietet die Möglichkeit zum Behandeln von Problemen, die bei Virtual Network-Gateways und -Verbindungen auftreten können. Wenn eine Anforderung an die Ressourcenproblembehandlung gesendet wird, werden Protokolle abgefragt und untersucht. Nach Abschluss der Untersuchung werden die Ergebnisse zurückgegeben. Anforderungen der Ressourcenproblembehandlung sind Anforderungen mit langer Ausführungszeit. Daher kann es mehrere Minuten dauern, bis ein Ergebnis zurückgegeben wird. Die Protokolle der Problembehandlung werden in einem Container in einem angegebenen Speicherkonto gespeichert.

## <a name="troubleshoot-a-gateway-or-connection"></a>Problembehandlung bei einem Gateway oder einer Verbindung

1. Navigieren Sie zum [Azure-Portal](https://portal.azure.com), und klicken Sie auf **Netzwerk** > **Network Watcher** > **VPN-Diagnose**.
2. Wählen Sie ein **Abonnement**, eine **Ressource** und einen **Speicherort** aus.
3. Die Ressourcenproblembehandlung gibt Daten zur Integrität der Ressource zurück. Sie speichert darüber hinaus auch für ein Speicherkonto relevante Protokolle zum Überprüfen. Klicken Sie auf **Speicherkonto**, um ein Speicherkonto auszuwählen.
4. Wählen Sie auf dem Blatt **Speicherkonten** ein vorhandenes Speicherkonto aus, oder klicken Sie auf **+ Speicherkonto**, um ein neues Speicherkonto zu erstellen.
5. Wählen Sie auf dem Blatt **Container** einen vorhandenen Container aus, oder klicken Sie auf **+ Container**, um einen neuen Container zu erstellen. Wenn Sie fertig sind, klicken Sie auf **Auswählen**.
6. Wählen Sie die Gateway- und Verbindungsressourcen für die Problembehandlung aus, und klicken Sie auf **Mit der Problembehandlung beginnen**.

Wenn mehrere Ressourcen ausgewählt sind, wird die Problembehandlung für Gatewayressourcen gleichzeitig ausgeführt. Für eine Verbindung und das zugehörige Gateway kann sie nicht gleichzeitig ausgeführt werden. Es wird empfohlen, die Problembehandlung für Gateways zuerst auszuführen, da die Problembehandlung einer Verbindung ein längerer Prozess ist. Während die VPN-Diagnose für eine Ressource durchgeführt wird, wird in der Spalte **Problembehandlungsstatus** der Status **Wird ausgeführt** angezeigt.

Nach Abschluss des Vorgangs wird in der Statusspalte **Fehlerfrei** oder **Fehlerhaft** angezeigt.

![Problembehandlung abgeschlossen][2]

## <a name="understanding-the-results"></a>Grundlegendes zu den Ergebnissen

Im Abschnitt **Details** des Fensters wird auf der Registerkarte **Status** der Status der letzten Problembehandlungsausführung für die ausgewählte Ressource angezeigt. Die Ergebnisse der letzten Diagnose werden xx Minuten nach der letzten Ausführung angezeigt.

|Eigenschaft  |BESCHREIBUNG  |
|---------|---------|
|Ressource     | Ein Link zur Ressource        |
|Speicherpfad     |  Pfad zum Speicherkonto und Container, die die Protokolle enthalten (sofern bei der Ausführung welche erstellt wurden). Diese Einstellung geht nach dem Verlassen des Portals verloren.        |
|Zusammenfassung     | Zusammenfassung der Ressourcenintegrität        |
|Detail     | Ausführliche Informationen zur Ressourcenintegrität        |
|Letzte Ausführung     | Die Uhrzeit der letzten Problembehandlung        |


Die Registerkarte **Aktion** enthält allgemeine Richtlinien zum Beheben des Problems. Wenn eine Aktion für das Problem ausgeführt werden kann, wird ein Link mit weiteren Anleitungen bereitgestellt. Falls es keine weitere Anleitungen gibt, enthält die Antwort die URL zum Öffnen einer Supportanfrage.  Weitere Informationen zu den Eigenschaften der Antwort und zu deren Inhalt finden Sie unter [Übersicht über die Network Watcher-Problembehandlung](network-watcher-troubleshoot-overview.md).


## <a name="next-steps"></a>Nächste Schritte

Wenn Einstellungen geändert wurden und die VPN-Konnektivität beenden, finden Sie unter [Verwalten von Netzwerksicherheitsgruppen](../virtual-network/manage-network-security-group.md) Informationen zum Ermitteln der fraglichen Netzwerksicherheitsgruppe und der Sicherheitsregeln.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
