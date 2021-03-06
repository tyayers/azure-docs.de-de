---
title: DNS-Alias für Azure SQL-Datenbank | Microsoft-Dokumentation
description: Ihre Anwendungen können eine Verbindung mit einem Alias für den Namen Ihres Azure SQL-Datenbankservers herstellen. In der Zwischenzeit können Sie SQL-Datenbank, auf die der Alias verweist, jederzeit ändern, um Tests und andere Vorgänge zu vereinfachen.
services: sql-database
author: MightyPen
manager: craigg
ms.service: sql-database
ms.custom: DNS alias
ms.topic: article
ms.date: 02/05/2018
ms.reviewer: genemi;ayolubek
ms.author: dmalik
ms.openlocfilehash: 1793f44026db55d17fabde5fb92bc46795109418
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dns-alias-for-azure-sql-database"></a>DNS-Alias für Azure SQL-Datenbank

Azure SQL-Datenbank weist einen DNS-Server (Domain Name System) auf. PowerShell und REST-APIs akzeptieren [Aufrufe zum Erstellen und Verwalten von DNS-Aliase](#anchor-powershell-code-62x) für den Namen Ihres SQL-Datenbankservers.

Anstelle des Namens des Azure SQL-Datenbankservers kann ein *DNS-Alias* verwendet werden. Clientprogramme können den Alias in den Verbindungszeichenfolgen angeben. Der DNS-Alias stellt eine Übersetzungsebene bereit, die Ihre Clientprogramme an verschiedene Server umleiten kann. Durch diese Ebene wird Ihnen die Schwierigkeit erspart, alle Clients und deren Verbindungszeichenfolgen zu suchen und zu bearbeiten.

Zu den allgemeinen Verwendungsmöglichkeiten für einen DNS-Alias zählen Folgende:

- Erstellen Sie einen einprägsamen Namen für einen Azure SQL-Server.
- Bei der Erstentwicklung kann Ihr Alias auf einen SQL-Datenbanktestserver verweisen. Wenn die Anwendung online geschaltet wird, können Sie den Alias auf den Produktionsserver verweisen. Für den Übergang zwischen Test und Produktion sind keine Änderungen an den Konfigurationen mehrerer Clients erforderlich, die mit dem Datenbankserver verbunden sind.
- Nehmen Sie an, dass die einzige Datenbank in Ihrer Anwendung auf einen anderen SQL-Datenbankserver migriert wurde. In diesem Fall können Sie den Alias ändern, ohne die Konfigurationen mehrerer Clients ändern zu müssen.

#### <a name="domain-name-system-dns-of-the-internet"></a>Internet-DNS (Domain Name System)

Das Internet basiert auf dem DNS. Das DNS übersetzt die Anzeigenamen in den Namen Ihres Azure SQL-Datenbankservers.

## <a name="scenarios-with-one-dns-alias"></a>Szenarien mit einem DNS-Alias

Nehmen Sie an, Sie müssen Ihr System auf einen neuen Azure SQL-Datenbankserver umstellen. Bisher mussten Sie jede Verbindungszeichenfolge in jedem Clientprogramm suchen und aktualisieren. Doch nun muss nur eine Aliaseigenschaft aktualisiert werden, wenn in den Verbindungszeichenfolgen ein DNS-Alias enthalten ist.

Das DNS-Aliasfeature von Azure SQL-Datenbank kann in folgenden Szenarien hilfreich sein:

#### <a name="test-to-production"></a>Test bis Produktion

Bei der Entwicklung der Clientprogramme verwenden Sie einen DNS-Alias in den Verbindungszeichenfolgen. Sie ändern die Eigenschaften des Alias dahingehend, dass sie auf eine Testversion Ihres Azure SQL-Datenbankservers verweisen.

Wenn das neue System später in der Produktion online geschaltet wird, können Sie die Eigenschaften des Alias dahingehend aktualisieren, dass sie auf den SQL-Datenbankproduktionsserver verweisen. Es sind keine Änderung an den Clientprogrammen erforderlich.

#### <a name="cross-region-support"></a>Regionsübergreifende Unterstützung

Bei einer Notfallwiederherstellung wird Ihr SQL-Datenbankserver möglicherweise in eine andere geografische Region verschoben. Bei einem System, bei dem ein DNS-Alias verwendet wurde, kann die Erfordernis zum Suchen und Aktualisieren aller Verbindungszeichenfolgen für sämtliche Clients vermieden werden. Stattdessen können Sie einen Alias dahingehend aktualisieren, dass er auf den neuen SQL-Datenbankserver verweist, der nun Ihre Datenbank hostet.




## <a name="properties-of-a-dns-alias"></a>Eigenschaften eines DNS-Alias

Die folgenden Eigenschaften gelten für sämtliche DNS-Aliase Ihres SQL-Datenbankservers:

- *Eindeutiger Name*: Jeder Aliasname, den Sie erstellen, ist auf allen Azure SQL-Datenbankservern eindeutig – genauso wie Servernamen.

- *Server ist erforderlich*: Ein DNS-Alias kann nur dann erstellt werden, wenn er auf genau einen Server verweist und der Server bereits vorhanden ist. Ein aktualisierter Alias muss immer genau auf einen vorhandenen Server verweisen.
    - Wenn Sie einen SQL-Datenbankserver löschen, löscht das Azure-System auch alle DNS-Aliase, die auf den Server verweisen.

- *Nicht an eine beliebige Region gebunden*: DNS-Aliase sind nicht an eine Region gebunden. DNS-Aliase können dahingehend aktualisiert werden, dass sie auf einen Azure SQL-Datenbankserver in einer beliebigen geografischen Region verweisen.
    - Wenn ein Alias jedoch für den Verweis auf einen anderen Server aktualisiert wird, müssen beide Server im selben Azure-*Abonnement* vorhanden sein.

- *Berechtigungen*: Für die Verwaltung eines DNS-Alias benötigt der Benutzer die Berechtigungen *Servermitwirkender* oder höhere Berechtigungen. Weitere Informationen finden Sie unter [Erste Schritte mit der rollenbasierten Zugriffssteuerung im Azure-Portal](../role-based-access-control/overview.md).





## <a name="manage-your-dns-aliases"></a>Verwalten von DNS-Aliase

REST-APIs und PowerShell-Cmdlets werden Ihnen für die programmgesteuerte Verwaltung Ihrer DNS-Aliase zur Verfügung gestellt.

#### <a name="rest-apis-for-managing-your-dns-aliases"></a>REST-APIs für die Verwaltung Ihrer DNS-Aliase

<!-- TODO
??2 "soon" in the following live sentence, is not the best situation.
TODO update this subsection very soon after REST API docu goes live.
Dev = Magda Bojarska
Comment as of:  2018-01-26
-->

Die Dokumentation für die REST-APIs finden Sie an folgendem Webspeicherort:
- [Azure SQL-Datenbank-REST-API](https://docs.microsoft.com/rest/api/sql/)

Darüber hinaus können sich die REST-APIs in GitHub unter folgendem Link befinden:
- [Azure SQL-Datenbank-Server, DNS-Alias-REST-APIs](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/sql/resource-manager/Microsoft.Sql/preview/2017-03-01-preview/serverDnsAliases.json)

<a name="anchor-powershell-code-62x"/>

#### <a name="powershell-for-managing-your-dns-aliases"></a>PowerShell für die Verwaltung Ihrer DNS-Aliase

Es sind PowerShell-Cmdlets verfügbar, die die REST-APIs aufrufen.

Ein Codebeispiel von PowerShell-Cmdlets, das für die Verwaltung von DNS-Aliase zu verwenden ist, ist unter folgendem Link dokumentiert:
- [PowerShell für den DNS-Alias für Azure SQL-Datenbank](dns-alias-powershell.md)


Die im Codebeispiel verwendeten Cmdlets lauten wie folgt:
- [New-AzureRMSqlServerDNSAlias](https://docs.microsoft.com/powershell/module/AzureRM.Sql/New-AzureRmSqlServerDnsAlias?view=azurermps-5.1.1): Erstellt einen neuen DNS-Alias im Azure SQL-Datenbankdienstsystem. Der Alias verweist auf Azure SQL-Datenbankserver 1.
- [Get-AzureRMSqlServerDNSAlias](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServerDnsAlias?view=azurermps-5.1.1): Ruft alle DNS-Aliase auf, die SQL-Datenbankserver 1 zugewiesen sind, und listet diese auf.
- [Set-AzureRMSqlServerDNSAlias](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Set-AzureRmSqlServerDnsAlias?view=azurermps-5.1.1): Ändert den Servernamen, auf dessen Verweis der Alias konfiguriert ist, von Server 1 in SQL-Datenbankserver 2.
- [Remove-AzureRMSqlServerDNSAlias](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Remove-AzureRmSqlServerDnsAlias?view=azurermps-5.1.1): Entfernt den DNS-Alias aus SQL-Datenbankserver 2 anhand des Aliasnamens.


Die oben angegebenen Cmdlets wurden zum Modul **AzureRM.Sql** ab Modulversion 5.1.1 hinzugefügt.




## <a name="limitations-during-preview"></a>Einschränkungen in der Vorschauversion

Für einen DNS-Alias gelten gegenwärtig die folgenden Einschränkungen:

- *Verzögerung von bis zu 2 Minuten*: Es dauert bis zu zwei Minuten, bis ein DNS-Alias aktualisiert oder entfernt wird.
    - Abgesehen von einer kurzen Verzögerung stellt der Alias den Verweis von Clientverbindungen mit dem Legacyserver umgehend ein.

- *DNS-Suche*: Derzeit besteht die einzige autoritative Möglichkeit darin, anhand einer [DNS-Suche ](https://docs.microsoft.com/windows-server/administration/windows-commands/nslookup) zu überprüfen, auf welchen Server ein bestimmter DNS-Alias verweist.

- *[Tabellenüberwachung wird nicht unterstützt](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md):* Sie können keinen DNS-Alias für einen Azure SQL-Datenbankserver verwenden, für den die *Tabellenüberwachung* für eine Datenbank aktiviert ist.
    - Die Tabellenüberwachung wurde eingestellt.
    - Es wird empfohlen, auf [Blobüberwachung](sql-database-auditing.md) umzusteigen.




## <a name="related-resources"></a>Zugehörige Ressourcen

- Informationen zur Notfallwiederherstellung finden Sie unter [Übersicht über die Geschäftskontinuität mit Azure SQL-Datenbank](sql-database-business-continuity.md).



## <a name="next-steps"></a>Nächste Schritte

- [PowerShell für den DNS-Alias für Azure SQL-Datenbank](dns-alias-powershell.md)

