---
title: Schutz von in Azure Stack bereitgestellten VMs | Microsoft-Dokumentation
description: Richtlinien zum Schutz von in Azure Stack bereitgestellten virtuellen Computern.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 4e5833cf-4790-4146-82d6-737975fb06ba
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: 02get-started-article
ms.date: 02/27/2018
ms.author: mabrigg
ms.reviewer: hector.linares
ms.openlocfilehash: 0e74c6af36130d206456634548f452a1f1a2d4af
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="protect-virtual-machines-deployed-on-azure-stack"></a>Schutz von in Azure Stack bereitgestellten virtuellen Computern

*Gilt für: integrierte Azure Stack-Systeme und Azure Stack Development Kit*

In diesem Artikel werden die Richtlinien beschrieben, um in Azure Stack bereitgestellte Benutzer-VMs zu schützen.

Zum Schutz vor Datenverlusten und ungeplanten Ausfallzeiten müssen Sie einen Sicherungs- oder Notfallwiederherstellungsplan für Ihre Benutzeranwendungen und -daten implementieren. Dieser Plan ist für jede Anwendung eindeutig, folgt jedoch einem Framework, der im Zuge einer weitreichenden Geschäftskontinuitäts- und Notfallwiederherstellungsstrategie Ihrer Organisation entwickelt wurde. Allgemeine Muster und Vorgehensweisen für die Anwendungsverfügbarkeit und -resilienz finden Sie im Azure Architecture Center unter [Entwerfen robuster Anwendungen für Azure](https://docs.microsoft.com/azure/architecture/resiliency).

## <a name="azure-stack-infrastructure-recovery"></a>Wiederherstellung der Azure Stack-Infrastruktur

Benutzer müssen ihre VMs unabhängig von den Azure Stack-Infrastrukturdiensten schützen.

Wenn die Azure Stack-Cloud längere Zeit offline ist oder dauerhaft nicht wiederhergestellt werden kann, müssen Sie einen Plan besitzen, damit Ihre Anwendung weiterhin Benutzeranforderungen mit minimalen Ausfallzeiten verarbeitet. Der Betreiber der Azure Stack-Cloud ist für die Ausarbeitung eines Wiederherstellungsplans für die zugrunde liegende Azure Stack-Infrastruktur und die Dienste zuständig. Weitere Informationen finden Sie im Artikel [Wiederherstellen nach schwerwiegendem Datenverlust](https://docs.microsoft.com/azure/azure-stack/azure-stack-backup-recover-data). 

Der Wiederherstellungsplan für Azure Stack-Infrastrukturdienste umfasst nicht die Wiederherstellung von benutzerseitigen VMs, Speicherkonten oder Datenbanken. Als Anwendungsbesitzer sind Sie für die Implementierung eines Wiederherstellungsplans für Ihre Anwendungen und Daten verantwortlich.
 
## <a name="sourcetarget-combinations"></a>Quelle/Ziel-Kombinationen

Jede Azure Stack-Cloud wird in einem Rechenzentrum bereitgestellt. Für die Wiederherstellung Ihrer Anwendungen ist eine separate Umgebung erforderlich. Bei der Umgebung kann es sich um eine separate Azure Stack-Cloud in einem anderen Rechenzentrum oder die öffentliche Azure-Cloud handeln. Von Ihren Anforderungen hinsichtlich der Datenhoheit und des Datenschutzes hängt ab, welche Wiederherstellungsumgebung für Ihre Anwendung erforderlich ist. Bei der Aktivierung des Schutzes für die Anwendungen können Sie für jede Anwendung eine bestimmte Wiederherstellungsoption auswählen. So können Anwendungen in einem Abonnement enthalten sein, das Daten in einem anderen Rechenzentrum sichert. In einem anderen Abonnement können Sie Daten in der öffentlichen Azure-Cloud replizieren. 
 
Planen Sie Ihre Sicherungswiederherstellungs- und Notfallwiederherstellungsstrategie für die einzelnen Anwendungen, um das Ziel für jede Anwendung zu bestimmen. So kann Ihre Organisation die Größe der lokal erforderlichen Speicherkapazität entsprechend anpassen und den Verbrauch in der öffentlichen Cloud kalkulieren. 

|  | Globale Azure-Umgebung | Azure Stack-Bereitstellung in einem von CSP betriebenem Rechenzentrum | Azure Stack-Bereitstellung in einem vom Kunden betriebenen Rechenzentrum |
|------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **Azure Stack-Bereitstellung in einem von CSP betriebenen Rechenzentrum** | Es werden Benutzer-VMs für die von CSP betriebene Azure Stack-Instanz bereitgestellt. Benutzer-VMs werden über eine Sicherung oder ein Failover direkt in Azure wiederhergestellt. | CSP betreibt die primären und sekundären Instanzen von Azure Stack in seinen eigenen Rechenzentren. Benutzer-VMs werden wiederhergestellt, oder es wird ein Failover zwischen den beiden Azure Stack-Instanzen durchgeführt. | CSP betreibt Azure Stack am primären Standort. Das Rechenzentrum des Kunden ist das Wiederherstellungs- oder Failoverziel. |
| **Azure Stack-Bereitstellung in einem vom Kunden betriebenen Rechenzentrum** | Es werden Benutzer-VMs für die vom Kunden betriebene Azure Stack-Instanz bereitgestellt. Benutzer-VMs werden über eine Sicherung oder ein Failover direkt in Azure wiederhergestellt. | Der Kunde betreibt die primären und sekundären Instanzen von Azure Stack in seinen eigenen Rechenzentren. Benutzer-VMs werden wiederhergestellt, oder es wird ein Failover zwischen den beiden Azure Stack-Instanzen durchgeführt. | Der Kunde betreibt Azure Stack am primären Standort. Das Rechenzentrum von CSP ist das Wiederherstellungs- oder Failoverziel. |

![Quelle/Ziel-Kombinationen](media\azure-stack-manage-vm-backup\vm_backupdataflow_01.png)

## <a name="application-recovery-objectives"></a>Ziele für die Anwendungswiederherstellung

Um die beste Vorgehensweise zum Schutz Ihrer Anwendungen in Azure Stack ermitteln zu können, müssen Sie den Umfang der Ausfallzeiten und Datenverluste festlegen, die Ihre Organisation bezüglich der einzelnen Anwendungen tolerieren kann. Die Werte für den Umfang der Ausfallzeiten und Datenverluste müssen ermittelt werden, um einen Wiederherstellungsplan zu entwickeln und zu implementieren, der die Auswirkungen auf Ihre Organisation minimiert. Für die einzelnen Anwendungen sollten Sie Folgendes in Erwägung ziehen:  
 - **Recovery Time Objective (RTO)**  
Die RTO ist der maximal zulässige Zeitraum, in dem eine Anwendung nach einem Vorfall nicht verfügbar sein darf. Wenn RTO bei Ihnen 90 Minuten beträgt, müssen Sie dazu in der Lage sein, die Anwendung innerhalb von 90 Minuten nach Beginn eines Notfalls wieder in den Ausführungszustand zu versetzen. Falls für die RTO ein niedriger Wert angesetzt ist, führen Sie ggf. eine zweite Bereitstellung durchgehend im Standby aus, um vor einem regionalen Ausfall geschützt zu sein.
 - **Recovery Point Objective (RPO)**  
RPO ist der maximale Zeitraum bei einem Notfall, in dem ein Datenverlust zulässig ist. Wenn Sie Daten beispielsweise in einer einzelnen Datenbank ohne Replikation in anderen Datenbanken speichern und stündliche Sicherungen durchführen, können Daten für bis zu eine Stunde verloren gehen.
 
RTO und RPO sind geschäftliche Anforderungen. Führen Sie eine Risikobewertung durch, um die RTO und RPO der Anwendung zu definieren. Eine weitere gängige Metrik ist **Mean Time to Recover** (MTTR) – der durchschnittliche Zeitraum, der zur Wiederherstellung der Anwendung nach einem Ausfall erforderlich ist. MTTR ist ein empirischer Fakt eines Systems. Wenn der MTTR-Wert größer als der RTO-Wert ist, führt ein Ausfall des Systems zu einer nicht akzeptablen geschäftlichen Störung, weil es nicht möglich ist, das System innerhalb des definierten RTO-Zeitraums wiederherzustellen.

### <a name="backup-restore"></a>Sicherungswiederherstellung

Das Schema zum Schutz der am häufigsten verwendeten VM-basierten Anwendungen ist die Verwendung von Sicherungssoftware. Die Sicherung einer VM umfasst in der Regel das Betriebssystem, die Betriebssystemkonfiguration, Anwendungsbinärdateien und Anwendungsdaten. Die Sicherungen werden durch Erstellen einer Momentaufnahme der Volumes, Datenträger oder der gesamten VM erstellt. Mit Azure Stack haben Sie die Möglichkeit, innerhalb des Kontexts des Gastbetriebssystems oder über Speicher- und Compute-APIs von Azure Stack Sicherungen durchzuführen. Azure Stack unterstützt nicht die Durchführung von Sicherungen auf Hypervisorebene. 
 
![Sicherungswiederherstellung](media\azure-stack-manage-vm-backup\vm_backupdataflow_03.png)
 
Für die Wiederherstellung der Anwendung muss mindestens eine VM in der gleichen Cloud oder in einer neuen Cloud wiederhergestellt werden. Sie können als Ziel eine Cloud in Ihrem Rechenzentrum oder in der öffentlichen Cloud festlegen. Die Auswahl der als Ziel zu verwendenden Cloud liegt dabei vollständig in Ihrer Hand und hängt von Ihren Anforderungen hinsichtlich des Datenschutzes und der Datenhoheit ab. 
 
 - RTO: In Stunden gemessene Ausfallzeit 
 - RPO: Variabler Datenverlust (je nach Sicherungshäufigkeit)
 - Bereitstellungstopologie: Aktiv/Passiv 

#### <a name="planning-your-backup-strategy"></a>Planen der Sicherungsstrategie

Bei der Planung Ihrer Sicherungsstrategie und Definition der Skalierungsanforderungen müssen Sie zunächst die Anzahl der VM-Instanzen ermitteln, die geschützt werden müssen. Die Sicherung sämtlicher VM auf allen Servern in einer Umgebung ist eine sehr häufig angewendete Strategie. Bei Azure Stack gibt es jedoch einige VMs, die in jedem Fall gesichert werden müssen. VMs in einer Skalierungsgruppe werden beispielsweise als kurzlebige Ressourcen behandelt, die auch ohne vorherige Ankündigung beliebig hinzugefügt und entfernt werden können. Permanent zu speichernde Daten, die geschützt werden müssen, werden in einem separaten Repository wie einem Datenbank- oder Objektspeicher gespeichert. Wichtige Überlegungen zum Sichern von VMs in Azure Stack:

 - **Kategorisierung**
    - Ziehen Sie ein Modell in Betracht, bei dem Benutzer sich für die VM-Sicherung entscheiden.
    - Definieren Sie eine Wiederherstellungs-SLA basierend auf der Priorität der Anwendungen oder der Folgen für das Unternehmen.
 - **Skalieren**
    - Ziehen Sie gestaffelte Sicherungen in Betracht, wenn Sie eine große Anzahl neuer VMs integrieren (sofern eine Sicherung erforderlich ist).
    - Bewerten Sie Sicherungsprodukte, die effizient Sicherungsdaten erfassen und übertragen können, um Ressourceninhalte für die Lösung minimieren zu können.
    - Bewerten Sie Sicherungsprodukte, die effizient Sicherungsdaten mit inkrementellen oder differenziellen Sicherungen speichern, um die Notwendigkeit zum Abrufen vollständiger Sicherungen für alle VMs in der Umgebung zu minimieren.
 - **Restore**
    - Sicherungsprodukte können virtuelle Datenträger, Anwendungsdaten auf einer vorhandenen VM oder die gesamte VM-Ressource mit den zugehörigen virtuellen Datenträgern wiederherstellen. Das Wiederherstellungsschema, das Sie benötigen, hängt davon ab, wie Sie die Anwendung wiederherstellen möchten und wirkt sich auf den Zeitraum für die Wiederherstellung der Anwendung aus. Beispielsweise kann es einfacher sein, SQL Server über eine Vorlage erneut bereitzustellen und dann anstelle der gesamten VM oder Gruppe von VMs die Datenbanken wiederherzustellen.


### <a name="replicationmanual-failover"></a>Replikation und manuelles Failover

Ein alternativer Ansatz zur Unterstützung von Hochverfügbarkeit besteht darin, Ihre Anwendungs-VMs in eine andere Cloud zu replizieren und ein manuell ausgelöstes Failover zu veranlassen. Die Replikation des Betriebssystems, der Binärdateien der Anwendung und der Anwendungsdaten kann auf VM- oder Gastbetriebssystemebene ausgeführt werden. Steuern Sie das Failover mittels zusätzlicher Software getrennt von der Anwendung.
 
Bei diesem Ansatz wird die Anwendung nur in einer Cloud bereitgestellt. Die VM wird dann identisch mit Ihrem Rechenzentrum oder der öffentlichen Cloud in die andere Cloud repliziert. Wenn ein Failover ausgelöst wird, müssen die sekundären VMs in der zweiten Cloud eingeschaltet werden. In einigen Fällen werden beim Failover die VMs erstellt und an Datenträger angefügt. Die Durchführung dieses Vorgangs kann eine Weile dauern, insbesondere bei einer Multi-Tier-Anwendung mit einer bestimmten Startsequenz. Bevor die Anwendung mit der Anforderungsverarbeitung beginnen kann, müssen eventuell zusätzliche Schritte durchgeführt werden.

![Replikation und manuelles Failover](media\azure-stack-manage-vm-backup\vm_backupdataflow_02.png)

 - RTO: In Minuten gemessene Ausfallzeit 
 - RPO: Variabler Datenverlust (je nach Replikationshäufigkeit)
 - Bereitstellungstopologie: Aktiv/Passiv und Standby
 
### <a name="high-availabilityautomatic-failover"></a>Hochverfügbarkeit und automatisches Failover

Bei Anwendungen, bei denen Ihr Unternehmen Ausfallzeiten von wenigen Sekunden oder Minuten und minimalen Datenverlust tolerieren kann, müssen Sie eine Hochverfügbarkeitskonfiguration in Betracht ziehen. Hochverfügbarkeitsanwendungen sind für die schnelle und automatische Wiederherstellung nach Ausfällen konzipiert. Bei lokalen Hardwareausfällen implementiert die Azure Stack-Infrastruktur Hochverfügbarkeit im physischen Netzwerk mithilfe von zwei Top-of-Rack-Switches. Bei Ausfällen auf Compute-Ebene verwendet Azure Stack mehrere Knoten in einer Skalierungseinheit. Auf VM-Ebene können Sie Skalierungsgruppen in Kombination mit Fehlerdomänen verwenden, um sicherzustellen, dass Knotenausfälle nicht zum Ausfall Ihrer Anwendung führen. 
 
In Kombination mit Skalierungsgruppen muss Ihre Anwendung native Unterstützung für Hochverfügbarkeit oder die Verwendung von Clustersoftware bieten. Microsoft SQL Server bietet z.B. native Unterstützung für Hochverfügbarkeit für Datenbanken mit synchronem Commitmodus. Wenn Sie nur asynchrone Replikationen unterstützen können, so geht dies mit einem gewissen Datenverlust einher. Anwendungen können auch in einem Failovercluster bereitgestellt werden, in dem die Clustersoftware das automatische Failover der Anwendung verarbeitet. 
 
Bei dieser Vorgehensweise ist die Anwendung zwar nur in einer Cloud aktiv, doch die Software wird in mehreren Clouds bereitgestellt. Die anderen Clouds befinden sich im Standbymodus, um die Anwendung beim Auslösen des Failovers zu starten.

 - RTO: In Sekunden gemessene Ausfallzeit 
 - RPO: Minimaler Datenverlust
 - Bereitstellungstopologie: Aktiv/Aktiv und Standby

### <a name="fault-tolerance"></a>Fehlertoleranz

Die Verfügbarkeit des physischen Redundanz- und Infrastrukturdiensts Azure Stack schützt nur vor Ausfällen auf Hardwareebene, z.B. vor dem Ausfall eines Datenträgers, der Stromversorgung, eines Netzwerkports oder eines Knotens. Wenn die Anwendung jedoch durchgängig verfügbar sein muss und keine Daten verloren gehen dürfen, müssen Sie jedoch Fehlertoleranz nativ in Ihrer Anwendung implementieren oder Fehlertoleranz mit zusätzlicher Software aktivieren. 
 
Zunächst müssen Sie sicherstellen, dass die Anwendungs-VMs zum Schutz vor Ausfällen auf Knotenebene über Skalierungsgruppen bereitgestellt werden. Um zu verhindern, dass die Cloud offline geschaltet wird, muss die Anwendung bereits einer anderen Cloud bereitgestellt worden sein, damit die Anforderungsverarbeitung unterbrechungsfrei fortgesetzt werden kann. Dies wird in der Regel als „Aktiv/Aktiv-Bereitstellung“ bezeichnet.
 
Bedenken Sie, dass Azure Stack-Clouds unabhängig voneinander sind, weshalb die Clouds aus Sicht der Infrastruktur immer als aktiv gelten. In diesem Fall werden mehrere aktive Instanzen der Anwendung in einer oder in mehreren aktiven Clouds bereitgestellt. 
 
 - RTO: Keine Ausfallzeit
 - RPO: Kein Datenverlust
 - Bereitstellungstopologie: Aktiv/Aktiv

### <a name="no-recovery"></a>Keine Wiederherstellung

Einige Anwendungen in Ihrer Umgebung erfordern keinen Schutz vor ungeplanten Ausfallzeiten oder Datenverlusten. Die für die Entwicklung und Tests verwendeten VMs beispielsweise müssen normalerweise nicht wiederhergestellt werden. Es bleibt demnach Ihre Entscheidung, ob Sie eine Anwendung oder eine bestimmte VM mit einem Schutz versehen oder nicht. Azure Stack bietet keine Sicherung oder Replikation von VMs über die zugrunde liegende Infrastruktur. Ähnlich wie bei Azure müssen Sie den Schutz für die einzelnen VMs in jedem Ihrer Abonnements auswählen.  
 
 - RTO: Nicht behebbar 
 - RPO: Vollständiger Datenverlust
 
## <a name="recommended-topologies"></a>Empfohlene Topologien 

Wichtige Überlegungen zu Ihrer Azure Stack-Bereitstellung:

|     | Empfehlung | Kommentare |
|-------------------------------------------------------------------------------------------------|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Sicherung bzw. Wiederherstellung von VMs in einem bereits im Rechenzentrum bereitgestellten externen Sicherungsziel | Empfohlen | Nutzen Sie die vorhandene Sicherungsinfrastruktur und Ressourcen Ihres Betriebs. Passen Sie die Größe der Sicherungsinfrastruktur an, damit diese für den Schutz weiterer VM-Instanzen bereit ist. Stellen Sie sicher, dass sich die Sicherungsinfrastruktur nicht in der Nähe Ihrer Quelle befindet. Sie können VMs in der Azure Stack-Quellinstanz, in einer sekundären Azure Stack-Instanz oder in Azure wiederherstellen. |
| Sicherung bzw. Wiederherstellung von VMs in einem für Azure Stack dedizierten Sicherungsziel | Empfohlen | Sie können eine neue Sicherungsinfrastruktur erwerben oder eine dedizierte Sicherungsinfrastruktur für Azure Stack bereitstellen. Stellen Sie sicher, dass sich die Sicherungsinfrastruktur nicht in der Nähe Ihrer Quelle befindet. Sie können VMs in der Azure Stack-Quellinstanz, in einer sekundären Azure Stack-Instanz oder in Azure wiederherstellen. |
| Direkte Sicherung bzw. Wiederherstellung von VMs in einer globalen Azure-Umgebung oder bei einem vertrauenswürdige Dienstanbieter | Empfohlen | Solange Sie Ihre Datenschutz- und behördlichen Anforderungen erfüllen können, können Sie Ihre Sicherungen in einer globalen Azure-Umgebung oder bei einem vertrauenswürdigen Dienstanbieter speichern. Im Idealfall führt der Dienstanbieter auch Azure Stack aus. In diesem Fall profitieren Sie bei der Wiederherstellung von einer konsistenten Erfahrung hinsichtlich des Betriebs. |
| Replikation und Durchführung eines Failovers für VMs in einer separaten Azure Stack-Instanz | Empfohlen | Bei einem Failover müssen Sie über eine zweite vollständig funktionsfähige Azure Stack-Cloud verfügen, um längere Anwendungsausfallzeiten zu vermeiden. |
| Direkte Replikation und Durchführung eines Failovers für VMs in Azure oder bei einem vertrauenswürdige Dienstanbieter | Empfohlen | Solange Sie Ihre Datenschutz- und behördlichen Anforderungen erfüllen können, können Sie Ihre Daten in einer globalen Azure-Umgebung oder bei einem vertrauenswürdigen Dienstanbieter replizieren. Im Idealfall führt der Dienstanbieter auch Azure Stack aus. In diesem Fall profitieren Sie nach einem Failover von einer konsistenten Erfahrung hinsichtlich des Betriebs. |
| Bereitstellen eines Sicherungsziels in der gleichen Azure Stack-Cloud mit Ihren Anwendungsdaten | Nicht empfohlen | Speichern Sie Sicherungen nicht in der gleichen Azure Stack-Cloud. Ungeplante Ausfallzeiten der Cloud können Sie am Zugriff auf Ihre primären Daten und Sicherungsdaten hindern. Wenn Sie ein Sicherungsziel als virtuelles Gerät bereitstellen möchten (zwecks Optimierung der Sicherung und Wiederherstellung), müssen Sie sicherstellen, dass alle Daten fortlaufend in einen externen Speicherort für die Sicherung kopiert werden. |
| Bereitstellen einer physischen Sicherungsappliance im selben Rack, auf dem die Azure Stack-Lösung installiert ist | Nicht unterstützt | Zurzeit kann keine Verbindung mit Geräten für Top-of-Rack-Switches hergestellt werden, die nicht Teil der ursprünglichen Lösung sind. |
 
## <a name="next-steps"></a>Nächste Schritte 

In diesem Artikel werden die Richtlinien beschrieben, um in Azure Stack bereitgestellte Benutzer-VMs zu schützen. Weitere Informationen zum Schützen Ihrer VMs mithilfe von Azure-Diensten finden Sie unter folgenden Themen:
 - [Azure Backup Server-Unterstützung für Azure Stack](https://docs.microsoft.com/en-us/azure/backup/ ) 
 - [Azure Site Recovery-Unterstützung für Azure Stack](https://docs.microsoft.com/en-us/azure/site-recovery/)  
 
Weitere Informationen zu den Partnerprodukten, die VM-Schutz in Azure Stack bieten, finden Sie unter [Schutz von Anwendungen und Daten in Azure Stack](https://azure.microsoft.com/blog/protecting-applications-and-data-on-azure-stack/).
