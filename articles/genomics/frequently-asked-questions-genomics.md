---
title: 'Microsoft Genomics: Häufig gestellte Fragen | Microsoft-Dokumentation'
titleSuffix: Azure
description: Antworten auf häufig gestellte Fragen zu Microsoft Genomics.
services: microsoft-genomics
author: grhuynh
manager: jhubbard
editor: jasonwhowell
ms.author: grhuynh
ms.service: microsoft-genomics
ms.workload: genomics
ms.topic: article
ms.date: 12/07/2017
ms.openlocfilehash: b3f30dc5d185615370a8273f71554f784d286cd9
ms.sourcegitcommit: 1362e3d6961bdeaebed7fb342c7b0b34f6f6417a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="microsoft-genomics-common-questions"></a>Microsoft Genomics: Häufig gestellte Fragen

In diesem Artikel finden Sie die wichtigsten Fragen im Zusammenhang mit Microsoft Genomics. Weitere Informationen zum Microsoft Genomics-Dienst finden Sie unter [Was ist Microsoft Genomics?](overview-what-is-genomics.md) Weitere Informationen zur Problembehandlung finden Sie in unserem [Leitfaden zur Problembehandlung](troubleshooting-guide-genomics.md). 


## <a name="what-is-the-sla-for-microsoft-genomics"></a>Wie lautet die Vereinbarung zum Servicelevel für Microsoft Genomics?
Wir garantieren, dass der Microsoft Genomics-Dienst 99,9% der Zeit für den Empfang von Workflow-API-Anforderungen zur Verfügung steht. Weitere Informationen finden Sie unter [SLA](https://azure.microsoft.com/support/legal/sla/genomics/v1_0/).

## <a name="how-does-the-usage-of-microsoft-genomics-show-up-on-my-bill"></a>Wie wird die Nutzung von Microsoft Genomics auf meiner Rechnung ausgewiesen?
Microsoft Genomics wird nach der Anzahl der pro Workflow verarbeiteten Gigabasen abgerechnet. Weitere Informationen finden Sie unter [Preise](https://azure.microsoft.com/pricing/details/genomics/).


## <a name="where-can-i-find-a-list-of-all-possible-commands-and-arguments-for-the-msgen-client"></a>Wo finde ich eine Liste aller möglichen Befehle und Argumente für den `msgen`-Client?
Sie erhalten eine vollständige Liste der verfügbaren Befehle und Argumente, indem Sie `msgen help` ausführen. Wenn keine weiteren Argumente angegeben werden, wird eine Liste der verfügbaren Hilfeabschnitte angezeigt, jeweils einer für `submit`, `list`, `cancel` und `status`. Um Hilfe für einen bestimmten Befehl zu erhalten, geben Sie `msgen help command` ein. Beispielsweise listet `msgen help submit` alle Übermittlungsoptionen auf.

## <a name="what-are-the-most-commonly-used-commands-for-the-msgen-client"></a>Was sind die am häufigsten verwendeten Befehle für den `msgen`-Client?
Zu den am häufigsten verwendeten Befehlsargumenten für den `msgen`-Client zählen u.a.: 

 |**Befehl**          |  **Feldbeschreibung** |
 |:--------------------|:-------------         |
 |`list`               |Gibt eine Liste der Aufträge zurück, die Sie gesendet haben. Argumente finden Sie unter `msgen help list`.  |
 |`submit`             |Übermittelt eine Workflowanforderung an den Dienst. Argumente finden Sie unter `msgen help submit`.|
 |`status`             |Gibt den Status des Workflows zurück, der von `--workflow-id` angegeben wird. Siehe auch `msgen help status`. |
 |`cancel`             |Sendet eine Anforderung zum Abbrechen der Verarbeitung des Workflows, der von `--workflow-id` angegeben wird. Siehe auch `msgen help cancel`. |

## <a name="where-do-i-get-the-value-for---api-url-base"></a>Wo erhalte ich den Wert für `--api-url-base`?
Wechseln Sie zum Azure-Portal, und öffnen Sie die Seite Ihres Genomics-Kontos. Klicken Sie unter der Überschrift **Verwaltung** auf **Zugriffsschlüssel**. Dort finden Sie die API-URL und Ihre Zugriffsschlüssel.

## <a name="where-do-i-get-the-value-for---access-key"></a>Wo erhalte ich den Wert für `--access-key`?
Wechseln Sie zum Azure-Portal, und öffnen Sie die Seite Ihres Genomics-Kontos. Klicken Sie unter der Überschrift **Verwaltung** auf **Zugriffsschlüssel**. Dort finden Sie die API-URL und Ihre Zugriffsschlüssel.

## <a name="why-do-i-need-two-access-keys"></a>Warum benötige ich zwei Zugriffsschlüssel?
Sie benötigen zwei Zugriffsschlüssel, wenn Sie diese aktualisieren (neu erstellen) möchten, ohne die Nutzung des Diensts zu unterbrechen. Angenommen, Sie möchten den ersten Schlüssel aktualisieren. In diesem Fall schalten Sie alle neuen Workflows auf den zweiten Schlüssel um. Warten Sie dann, bis die bereits ausgeführten Workflows, die den ersten Schlüssel verwenden, beendet sind. Aktualisieren Sie erst dann den Schlüssel.

## <a name="do-you-save-my-storage-account-keys"></a>Speichern Sie meine Speicherkontoschlüssel?
Ihr Speicherkontoschlüssel wird verwendet, um kurzfristige Zugriffstoken für den Microsoft Genomics-Dienst zu erstellen, um Ihre Eingabedateien zu lesen und die Ausgabedateien zu schreiben. Die Standardgültigkeitsdauer von Token beträgt 48 Stunden. Die Tokendauer kann mit der Option `-sas/--sas-duration` des „submit“-Befehls geändert werden. Der Wert wird in Stunden angegeben.

## <a name="what-genome-references-can-i-use"></a>Welche Genomreferenzen kann ich verwenden?

Diese Referenzen werden unterstützt:
 |Verweis              | Wert von `-pa/--process-args` |
 |:-------------         |:-------------                 |
 |b37                    | `R=b37m1`                     |
 |hg38                   | `R=hg38m1`                    |      
 |hg38 (keine alternative Analyse) | `R=hg38m1x`                   |  
 |hg19                   | `R=hg19m1`                    |    

## <a name="how-do-i-format-my-command-line-arguments-as-a-config-file"></a>Wie formatiere ich meine Befehlszeilenargumente als Konfigurationsdatei? 

msgen versteht Konfigurationsdateien im folgendem Format:
* Alle Optionen werden als Schlüssel-Wert-Paare bereitgestellt, wobei die Werte durch einen Doppelpunkt von den Schlüsseln getrennt sind.
Leerraum wird ignoriert.
* Zeilen, die mit `#` beginnen, werden ignoriert.
* Befehlszeilenargumente im Langformat können in Schlüssel umgewandelt werden, indem die führenden Bindestriche entfernt und Bindestriche zwischen Wörtern durch Unterstriche ersetzt werden. Hier einige Konvertierungsbeispiele:

 |Befehlszeilenargument            | Konfigurationsdateizeile |
 |:-------------                   |:-------------                 |
 |`-u/--api-url-base https://url`  | *api_url_base:https://url*    |
 |`-k/--access-key KEY`            | *access_key:KEY*              |      
 |`-pa/--process-args R=B37m1`     | *process_args:R-b37m1*        |  

## <a name="next-steps"></a>Nächste Schritte

Verwenden Sie für die ersten Schritte mit Microsoft Genomics die folgenden Ressourcen:
- Steigen Sie ein, indem Sie Ihren ersten Workflow über den Microsoft Genomics-Dienst ausführen. [Ausführen eines Workflows über den Microsoft Genomics-Dienst](quickstart-run-genomics-workflow-portal.md)
- Übermitteln Sie Ihre eigenen Daten zur Verarbeitung durch den Microsoft Genomics-Dienst: [Paired FASTQ](quickstart-input-pair-FASTQ.md) | [BAM](quickstart-input-BAM.md) | [Multiple FASTQ oder BAM](quickstart-input-multiple.md) 

