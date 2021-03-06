---
title: Neuerungen in Azure Machine Learning
description: In diesem Dokument werden die Updates für Azure Machine Learning beschrieben.
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.service: machine-learning
ms.workload: data-services
ms.topic: reference
ms.date: 03/28/2018
ms.openlocfilehash: e30943426ad68171e1464f828a9c8672b06c975a
ms.sourcegitcommit: 59914a06e1f337399e4db3c6f3bc15c573079832
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="whats-new-in-azure-machine-learning"></a>Neuerungen in Azure Machine Learning

Dieser Artikel enthält Informationen zu den neuen Versionen für [Azure Machine Learning Services](../service/overview-what-is-azure-ml.md). 

## <a name="2018-03-sprint-4"></a>2018-03 (Sprint 4)
**Versionsnummer**: 0.1.1801.24353 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([Suchen Sie Ihre Version.](../service/known-issues-and-troubleshooting-guide.md#find-the-workbench-build-number))


Willkommen beim fünften Update von Azure Machine Learning Workbench. Bei vielen der unten angegebenen Aktualisierungen wurde Ihr Feedback direkt umgesetzt. Senden Sie weiter Feedback!

**Wichtige neue Features und Änderungen**

- Native Unterstützung der Ausführung von Skripts auf virtuellen Ubuntu-Remotecomputern in Ihrer eigenen Umgebung (zusätzlich zur Docker-basierten Remoteausführung)
- Neue Umgebung in der Workbench-App zum Erstellen von Computezielen und Laufzeitkonfigurationen (zusätzlich zur CLI-basierten Umgebung)
![Registerkarte für Umgebungen](media/azure-machine-learning-release-notes/environment-page.png)
- Anpassbare Ausführungsverlaufsberichte ![Abbildung neuer Ausführungsverlaufsberichte](media/azure-machine-learning-release-notes/new-run-history-reports.png)

**Detaillierte Aktualisierungen**

Die nachstehende Liste zeigt die detaillierten Aktualisierungen für jeden Komponentenbereich von Azure Machine Learning in diesem Sprint.

### <a name="workbench-ui"></a>Workbench-Benutzeroberfläche
- Anpassbare Ausführungsverlaufsberichte
  - Verbesserte Diagrammkonfiguration für Ausführungsverlaufsberichte
    - Die verwendeten Einstiegspunkte können geändert werden.
    - Filter der obersten Ebene können hinzugefügt und geändert werden. ![Hinzufügen von Filtern](media/azure-machine-learning-release-notes/add-filters.jpg)
    - Diagramme und Statistiken können hinzugefügt/geändert und per Drag & Drop neu angeordnet werden.
    ![Erstellen neuer Diagramme](media/azure-machine-learning-release-notes/configure-charts.png)

  - CRUD für Ausführungsverlaufsberichte
  - Alle vorhandenen Listenansichtskonfigurationen für den Ausführungsverlauf wurden in serverseitige Berichte verschoben, die als Pipelines für Ausführungen der ausgewählten Einstiegspunkte fungieren.

- Registerkarte für Umgebungen
  - Fügen Sie Ihrem Projekt ganz einfach neue Computeziel- und Ausführungskonfigurationsdateien hinzu. ![Neues Computeziel](media/azure-machine-learning-release-notes/add-new-environments.png)
  - Verwalten und aktualisieren Sie Ihre Konfigurationsdateien über eine einfache, formularbasierte Benutzerumgebung.
  - Neue Schaltfläche zum Vorbereiten Ihrer Umgebungen für die Ausführung

- Leistungsverbesserungen für die Dateiliste auf der Randleiste

### <a name="data-preparation"></a>Vorbereitung der Daten 
- Mit Azure Machine Learning Workbench können Sie jetzt anhand eines bekannten Spaltennamens nach einer Spalte suchen.


### <a name="experimentation"></a>Experimentieren
- Azure Machine Learning Workbench unterstützt jetzt das native Ausführen Ihrer Skripts in Ihrer eigenen Python- oder PySpark-Umgebung. Für diese Funktion erstellt und verwaltet der Benutzer seine eigene Umgebung auf dem virtuellen Remotecomputer und verwendet Azure Machine Learning Workbench, um seine Skripts für dieses Ziel auszuführen. Weitere Informationen finden Sie unter [Konfigurieren des Azure Machine Learning-Experimentieren-Diensts](experimentation-service-configuration.md). 

### <a name="model-management"></a>Modellverwaltung
- Unterstützung der Anpassung der bereitgestellten Container: Ermöglicht das Anpassen des Containerimages durch Installation externer Bibliotheken mit „apt-get“ usw. Ist nicht mehr auf Bibliotheken beschränkt, die über pip installiert werden können. Weitere Informationen finden Sie in der [Dokumentation](model-management-custom-container.md).
  - Verwenden Sie das Flag `--docker-file myDockerStepsFilename` und den Dateinamen in Manifest-, Image- oder Diensterstellungsbefehlen.
  - Beachten Sie, dass das Ubuntu-Basisimage nicht geändert werden kann.
  - Beispielbefehl: 
  
      ```shell
      $ az ml image create -n myimage -m mymodel.pkl -f score.py --docker-file mydockerstepsfile
      ```



## <a name="2018-01-sprint-3"></a>2018-01 (Sprint 3) 
**Versionsnummer**: 0.1.1712.18263  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([Suchen Sie Ihre Version.](../service/known-issues-and-troubleshooting-guide.md#find-the-workbench-build-number))

Nachfolgend werden die Aktualisierungen und Verbesserungen in diesem Sprint beschrieben. Viele dieser Aktualisierungen sind eine direkte Umsetzung des Benutzerfeedbacks. 


Die nachstehende Liste zeigt die detaillierten Aktualisierungen für jeden Komponentenbereich von Azure Machine Learning in diesem Sprint.

- Aktualisierung des Authentifizierungsstapels erzwingt Anmeldung und Kontoauswahl beim Start

### <a name="workbench"></a>Workbench
- Möglichkeit zum Installieren/Deinstallieren der App über „Programme hinzufügen/entfernen“
- Aktualisierung des Authentifizierungsstapels erzwingt Anmeldung und Kontoauswahl beim Start
- Verbesserte Oberfläche für einmaliges Anmelden (SSO) in Windows
- Benutzer, die mehreren Mandanten mit unterschiedlichen Anmeldeinformationen angehören, können sich jetzt bei Workbench anmelden

### <a name="ui"></a>Benutzeroberfläche
- Allgemeine Verbesserungen und Fehlerbehebungen

### <a name="notebooks"></a>Notebooks
- Allgemeine Verbesserungen und Fehlerbehebungen

### <a name="data-preparation"></a>Vorbereitung der Daten 
- Verbesserte automatische Vorschläge beim Durchführen von Transformationen nach Beispiel
- Verbesserter Algorithmus für Musterhäufigkeitsprüfung
- Möglichkeit zum Senden von Beispieldaten und Feedback während der Durchführung von Transformationen nach Beispiel ![Screenshot mit dem Link zum Senden von Feedback bei der Transformation zur Spaltenableitung](media/azure-machine-learning-release-notes/SendFeedbackFromDeriveColumn.png)
- Verbesserungen an der Spark-Laufzeit
- Pyspark durch Scala ersetzt
- Korrektur eines Fehlers, durch den „Daten nicht anwendbar“ für den Time Series-Inspektor nicht geschlossen werden konnte 
- Korrektur eines Fehlers, bei dem bei der Datenvorbereitung für HDI keine Reaktion erfolgte

### <a name="model-management-cli-updates"></a>CLI-Aktualisierungen für Modellverwaltung 
  - Für das Bereitstellen von Ressourcen ist es nicht mehr erforderlich, der Besitzer des Abonnements zu sein. Um die Bereitstellungsumgebung einzurichten, reicht der Zugriff „Mitwirkender“ für die Ressourcengruppe aus.
  - Für kostenlose Abonnements wurde die Einrichtung der lokalen Umgebung aktiviert. 

## <a name="2017-12-sprint-2-qfe"></a>2017-12 (Sprint 2 QFE) 
**Versionsnummer**: 0.1.1711.15323  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([Suchen Sie Ihre Version.](../service/known-issues-and-troubleshooting-guide.md#find-the-workbench-build-number))

Dies ist das QFE (Quick Fix Engineering)-Release, eine Nebenversion. Sie bietet Korrekturen für verschiedene Telemetrieprobleme und unterstützt das Produktteam dabei, besseren Einblick in die Produktverwendung zu erhalten. Die gewonnenen Erkenntnisse werden dazu genutzt, die Produktbenutzerfreundlichkeit weiter zu verbessern. 

Zusätzlich werden zwei wichtige Aktualisierungen bereitgestellt:

- Korrektur eines Fehlers beim Vorbereiten der Daten, der verhinderte, dass der Time Series-Inspektor in Datenvorbereitungspaketen angezeigt wurde.
- Im Befehlszeilentool ist es nicht länger erforderlich, Machine Learning-Compute-ACS-Cluster als Azure-Abonnementbesitzer bereitzustellen. 

## <a name="2017-12-sprint-2"></a>2017-12 (Sprint 2)
**Versionsnummer**: 0.1.1711.15263  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([Suchen Sie Ihre Version.](../service/known-issues-and-troubleshooting-guide.md#find-the-workbench-build-number))

Willkommen beim dritten Update von Azure Machine Learning. Dieses Update enthält Verbesserungen in der Workbench-App, der Befehlszeilenschnittstelle (CLI) und den Back-End-Diensten. Vielen Dank, dass Sie uns ein Lächeln oder Stirnrunzeln gesendet haben. Bei vielen der unten angegebenen Aktualisierungen wurde Ihr Feedback direkt umgesetzt. 

**Wichtige neue Features**
- [Unterstützung für SQL Server und Azure SQL-Datenbank als Datenquelle](data-prep-appendix2-supported-data-sources.md#types) 
- [Deep Learning in Spark mit GPU-Unterstützung unter Verwendung von MMLSpark](https://github.com/Azure/mmlspark/blob/master/docs/gpu-setup.md)
- [Alle AML-Container sind nach der Bereitstellung mit Azure IoT Edge-Geräten kompatibel (keine zusätzlichen Schritte erforderlich)](http://aka.ms/aml-iot-edge-blog)
- Liste der registrierten Modelle und Detailansichten im Azure-Portal verfügbar
- Zugriff auf Computeziele unter Verwendung der Authentifizierung mit SSH-Schlüsseln zusätzlich zum Zugriff über Benutzername/Kennwort 
- Neue Musterhäufigkeitsprüfung bei der Datenvorbereitung 

**Detaillierte Aktualisierungen** Die nachstehende Liste zeigt die detaillierten Aktualisierungen für jeden Komponentenbereich von Azure Machine Learning in diesem Sprint.

### <a name="installer"></a>Installer
- Der Installer kann eigenständig Updates ausführen, sodass Fehlerbehebungen und neue Features ohne eine erneute Installation unterstützt werden können.

### <a name="workbench-authentication"></a>Workbench-Authentifizierung
- Verschiedene Fehlerbehebungen für das Authentifizierungssystem. Teilen Sie uns mit, wenn weiterhin Anmeldeprobleme auftreten.
- Änderungen an der Benutzeroberfläche erleichtern das Auffinden der Proxy-Manager-Einstellungen.

### <a name="workbench"></a>Workbench
- Die schreibgeschützte Dateiansicht wird jetzt mit einem hellblauen Hintergrund angezeigt.
- Die Schaltfläche „Bearbeiten“ wurde nach rechts verschoben, damit sie leichter aufzufinden ist.
- Die Dateiformate „dsource“, „dprep“ und „ipynb“ können jetzt als unformatierter Text gerendert werden.
- Die Workbench verfügt nun über eine neue Bearbeitungsoberfläche, um den Benutzer an die Verwendung externer IDEs zum Bearbeiten von Skripts heranzuführen und die Workbench nur zum Bearbeiten von Dateitypen mit umfangreicher Bearbeitungsfunktionalität zu nutzen (z.B. Notebooks, Datenquellen, Datenvorbereitungspakete).
- Die Liste der Arbeitsbereiche und Projekte, auf die der Benutzer Zugriff hat, wird wesentlich schneller geladen.

### <a name="data-preparation"></a>Vorbereitung der Daten 
- Mithilfe einer Musterhäufigkeitsprüfung können die Zeichenfolgenmuster in einer Spalte angezeigt werden. Sie können Ihre Daten auch mithilfe dieser Muster filtern. Die angezeigte Ansicht ähnelt der Prüfung für die Anzahl von Werten. Der Unterschied liegt darin, dass die Musterhäufigkeit anstelle der Anzahl eindeutiger Daten die Anzahl eindeutiger Datenmuster zeigt. Sie können auch einen Filter verwenden, mit dem alle Zeilen, die einem bestimmten Muster entsprechen, entweder angezeigt werden oder nicht angezeigt werden.

![Abbildung zur Musterhäufigkeitsprüfung für die Produktnummer](media/azure-machine-learning-release-notes/pattern-inspector-product-number.png)

- Leistungsverbesserungen bei gleichzeitiger Empfehlung von Grenzfällen zur Überprüfung in der Transformation „Derive Column by Example“ (Spalte nach Beispiel ableiten)

- [Unterstützung für SQL Server und Azure SQL-Datenbank als Datenquelle](data-prep-appendix2-supported-data-sources.md#types) 

![Abbildung zum Erstellen einer neuen SQL Server-Datenquelle](media/azure-machine-learning-release-notes/sql-server-data-source.png)

- Die Ansicht „Auf einen Blick“ wurde für Zeilen- und Spaltenanzahl aktiviert.

![Abbildung zur Zeilen- und Spaltenanzahl auf einen Blick](media/azure-machine-learning-release-notes/row-col-count.png)

- Die Datenvorbereitung ist jetzt in allen Computekontexten aktiviert.
- Datenquellen mit Verwendung einer SQL Server-Datenbank sind in allen Computekontexten aktiviert.
- Rasterspalten zur Datenvorbereitung können nach Datentyp gefiltert werden.
- Ein Problem beim Konvertieren mehrerer Spalten in Datumswerte wurde behoben.
- Es wurde ein Problem behoben, durch das der Benutzer in „Derive Column by Example“ die Ausgabespalte als Quelle auswählen konnte, wenn der Name der Ausgabespalte im erweiterten Modus durch den Benutzer geändert wurde.

### <a name="job-execution"></a>Auftragsausführung
Sie können ab sofort mithilfe der auf SSH-Schlüsseln basierenden Authentifizierung ein Remotedocker- oder Clustercomputeziel erstellen und darauf zugreifen, indem Sie die folgenden Schritte ausführen:
- Fügen Sie mithilfe des folgenden Befehls in der CLI ein Computeziel an.

    ```azure-cli
    $ az ml computetarget attach remotedocker --name "remotevm" --address "remotevm_IP_address" --username "sshuser" --use-azureml-ssh-key
    ```
>[!NOTE]
>Die Option „-k“ (oder „--use-azureml-ssh-key“) im Befehl gibt an, dass ein SSH-Schlüssel generiert und verwendet werden soll.

- Azure ML Workbench generiert einen öffentlichen Schlüssel und gibt diesen in Ihrer Konsole aus. Melden Sie sich beim Computeziel mit demselben Benutzernamen an, und fügen Sie die Datei „~/.ssh/authorized_keys“ mit diesem öffentlichen Schlüssel an.

- Sie können dieses Computeziel vorbereiten und zur Ausführung verwenden, und Azure ML Workbench verwendet diesen Schlüssel für die Authentifizierung.  

Weitere Informationen zum Erstellen von Computezielen finden Sie unter [Konfigurieren des Azure Machine Learning-Experimentieren-Diensts](experimentation-service-configuration.md).

### <a name="visual-studio-tools-for-ai"></a>Visual Studio-Tools für AI
- Ab sofort werden die [Visual Studio-Tools für AI](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vstoolsai-vs2017) unterstützt. 

### <a name="command-line-interface-cli"></a>Befehlszeilenschnittstelle (Command Line Interface, CLI)
- Der neu hinzugefügte Befehl `az ml datasource create` ermöglicht das Erstellen einer Datenquellendatei über die Befehlszeile.

### <a name="model-management-and-operationalization"></a>Modellverwaltung und Operationalisierung
- [Alle AML-Container sind nach der Operationalisierung mit Azure IoT Edge-Geräten kompatibel (keine zusätzlichen Schritte erforderlich)](http://aka.ms/aml-iot-edge-blog) 
- Verbesserungen an den Fehlermeldungen in der o16n-CLI
- Fehlerbehebungen für die Portalbenutzeroberfläche für die Modellverwaltung  
- Konsistente Groß- und Kleinschreibung für Modellverwaltungsattribute auf der Detailseite
- Timeout für Aufrufe zur Echtzeitbewertung auf 60 Sekunden festgelegt
- Liste der registrierten Modelle und Detailansichten im Azure-Portal verfügbar

![Modelldetails im Portal](media/azure-machine-learning-release-notes/model-list.jpg)

![Modellübersicht im Portal](media/azure-machine-learning-release-notes/model-overview-portal.jpg)

### <a name="mmlspark"></a>MMLSpark
- Deep Learning in Spark mit [GPU-Unterstützung](https://github.com/Azure/mmlspark/blob/master/docs/gpu-setup.md)
- Unterstützung für Resource Manager-Vorlagen für eine einfache Ressourcenbereitstellung
- Unterstützung für das SparklyR-Ökosystem
- [AZTK-Integration](https://github.com/Azure/aztk/wiki/Spark-on-Azure-for-Python-Users#optional-set-up-mmlspark)

### <a name="sample-projects"></a>Beispielprojekte
- Die [Iris](https://github.com/Azure/MachineLearningSamples-Iris)- und [MMLSpark](https://github.com/Azure/mmlspark)-Beispiele wurden mit der neuen Azure ML SDK-Version aktualisiert.

### <a name="breaking-changes"></a>Wichtige Änderungen
- Die Option `--type` in `az ml computetarget attach` wurde zu einem Unterbefehl hochgestuft. 

    - `az ml computetarget attach --type remotedocker` ist jetzt `az ml computetarget attach remotedocker`
    - `az ml computetarget attach --type cluster` ist jetzt `az ml computetarget attach cluster`

## <a name="2017-11-sprint-1"></a>2017-11 (Sprint 1) 
**Versionsnummer**: 0.1.1710.31013  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([Suchen Sie Ihre Version.](../service/known-issues-and-troubleshooting-guide.md#find-the-workbench-build-number))

In diesem Release haben wir Verbesserungen in den Bereichen Sicherheit, Stabilität und Wartbarkeit in der Workbench-App, der CLI und für die Back-End-Diensteebene vorgenommen. Vielen Dank, dass Sie uns ein Lächeln oder Stirnrunzeln gesendet haben. Bei vielen der unten angegebenen Aktualisierungen handelt es sich um direkte Ergebnisse aufgrund Ihres Feedbacks. Senden Sie weiter Feedback!

### <a name="notable-new-features"></a>Wichtige neue Features
- Azure ML ist jetzt in zwei neuen Azure-Regionen verfügbar: **Europa, Westen** und **Asien, Südosten**. Hierdurch werden die vorherigen Regionen **USA, Osten 2**, **USA, Westen-Mitte** und **Australien, Osten** erweitert, sodass es insgesamt fünf Bereitstellungsregionen sind.
- Wir haben in der Workbench-App die Hervorhebung der Python-Codesyntax aktiviert, um das Lesen und Bearbeiten von Python-Quellcode zu vereinfachen. 
- Sie können Ihre bevorzugte IDE jetzt direkt aus einer Datei starten, anstatt über das gesamte Projekt.  Wenn Sie in Workbench eine Datei öffnen und dann auf „Bearbeiten“ klicken, wird Ihre IDE (derzeit werden VS Code und PyCharm unterstützt) mit der aktuellen Datei und dem dazugehörigen Projekt gestartet.  Sie können auch auf den Pfeil der Schaltfläche „Bearbeiten“ klicken, um die Datei im Workbench-Text-Editor zu bearbeiten.  Die Dateien sind schreibgeschützt, bis Sie auf „Bearbeiten“ klicken, um versehentliche Änderungen zu verhindern.
- Version 2.1.0 der beliebten Bibliothek `matplotlib` für das Zeichnen ist jetzt im Lieferumfang der Workbench-App enthalten.
- Wir haben die .NET Core-Version für die  Datenvorbereitungs-Engine auf 2.0 aktualisiert. Es ist dadurch nicht mehr erforderlich, während der Installation der App unter macOS den Schritt „brew-install openssl“ auszuführen. Außerdem ist dies die Grundlage noch besserer Features für die Datenvorbereitung, die für die nahe Zukunft geplant sind. 
- Wir haben eine versionsspezifische App-Startseite aktiviert, damit Sie relevantere Versionshinweise und Updateaufforderungen je nach Ihrer aktuellen App-Version erhalten.
- Auch wenn Ihr lokaler Benutzername eine Leerstelle enthält, kann die Anwendung jetzt erfolgreich installiert werden. 

### <a name="detailed-updates"></a>Detaillierte Aktualisierungen
Unten ist eine Liste mit detaillierten Aktualisierungen für jeden Komponentenbereich von Azure Machine Learning in diesem Sprint angegeben.

#### <a name="installer"></a>Installer
- Der App-Installer bereinigt nun das Installationsverzeichnis, das von der älteren Version der App erstellt wurde.
- Es wurde ein Fehler behoben, bei dem der Installer unter macOS High Sierra bei 100% hängen bleibt.
- Es ist jetzt ein direkter Link zum Installerverzeichnis vorhanden, damit Benutzer die Installerprotokolle prüfen können, falls die Installation nicht erfolgreich ist.
- Die Installation funktioniert nun für Benutzer, deren Benutzername eine Leerstelle enthält.

#### <a name="workbench-authentication"></a>Workbench-Authentifizierung
- Es ist Unterstützung für die Authentifizierung im Proxy-Manager vorhanden.
- Das Anmelden funktioniert jetzt auch, wenn sich Benutzer hinter einer Firewall befinden. 
- Wenn Benutzer über Experimentieren-Konten in mehreren Azure-Regionen verfügen und eine Region nicht verfügbar ist, hängt die App nicht mehr.
- Wenn die Authentifizierung nicht abgeschlossen ist und das dazugehörige Dialogfeld noch sichtbar ist, versucht die App nicht mehr, den Arbeitsbereich aus dem lokalen Cache zu laden.

#### <a name="workbench-app"></a>Workbench-App
- Die Hervorhebung der Python-Codesyntax ist im Text-Editor aktiviert.
- Mit der Schaltfläche „Bearbeiten“ im Text-Editor können Sie die Datei entweder in einer IDE (VS Code und PyCharm werden unterstützt) oder im integrierten Text-Editor bearbeiten.
- Der Text-Editor befindet sich standardmäßig im schreibgeschützten Modus. 
- Der Anzeigezustand der Schaltfläche „Speichern“ wird nach dem Speichern der aktuellen Datei, die dann keine ungespeicherten Änderungen enthält, jetzt in den deaktivierten Zustand geändert.
- Workbench speichert _alle_ ungespeicherten Dateien, wenn Sie eine Ausführung initiieren.
- Workbench speichert den zuletzt verwendeten Arbeitsbereich auf dem lokalen Computer, damit er automatisch geöffnet werden kann.
- Es kann jetzt nur noch eine einzelne Instanz von Workbench ausgeführt werden. Bisher konnten mehrere Instanzen gestartet werden, und es konnte zu Problemen kommen, wenn darin an demselben Projekt gearbeitet wurde.
- Im Menü „Datei“ wurde die Option „Open Project...“ (Projekt öffnen...) in „Add Existing Folder as Project...“ (Vorhandenen Ordner als Projekt hinzufügen...) umbenannt. 
- Registerkarten können nun viel schneller gewechselt werden.
- Dem Dialogfeld „Configuring IDE“ (IDE konfigurieren) wurden Hilfelinks hinzugefügt.
- Im Feedbackformular wird jetzt die E-Mail-Adresse gespeichert, die Sie beim letzten Besuch eingegeben haben.
- Im Formular ist der Textbereich für Lächeln und Stirnrunzeln jetzt größer, damit Sie uns mehr Feedback senden können! 
- Der Hilfetext zum Switch `--owner` unter `az ml workspace create` wurde korrigiert.
- Wir haben das Dialogfeld „About“ (Info) hinzugefügt, damit Benutzer die Versionsnummer der App leicht anzeigen und kopieren können.
- Dem Menü „Hilfe“ wurde das Menüelement „Feature vorschlagen“ hinzugefügt.
- Der Name des Experimentieren-Kontos ist jetzt in der App-Titelleiste sichtbar und wird vor dem App-Namen „Azure Machine Learning Workbench“ angezeigt.
- Basierend auf der erkannten App-Version wird jetzt eine versionsspezifische App-Homepage angezeigt.

#### <a name="data-preparation"></a>Vorbereitung der Daten 
- Eine externe Website kann über den Karteninspektor nicht mehr geladen werden, um potenzielle Sicherheitsprobleme zu verhindern.
- Die Inspektoren für Histogramm und Wertanzahl enthalten jetzt eine Option zum Anzeigen des Graphen mit einer logarithmischen Skala.
- Bei Durchführung einer Berechnung wird im Balken zur Datenqualität jetzt eine andere Farbe angezeigt, um den Berechnungszustand anzugeben.
- Spaltenmetriken zeigen jetzt statistische Daten für Spalten mit Kategoriewerten an.
- Das letzte Zeichen des Datenquellennamens wird nicht mehr abgeschnitten.
- Das Datenvorbereitungspaket bleibt beim Wechseln von Registerkarten jetzt geöffnet, um die Leistung deutlich zu erhöhen.
- In der Datenquelle ändert sich die Reihenfolge der Spalten beim Wechseln zwischen Daten- und Metrikansicht nicht mehr.
- Wenn eine ungültige `.dprep`- oder `.dsource`-Datei geöffnet wird, stürzt Workbench nicht mehr ab.
- Im Datenvorbereitungspaket kann der relative Pfad jetzt für die Ausgabe in der Transformation _Write to CSV_ (In CSV schreiben) verwendet werden.
- Mit der Transformation _Keep Column_ (Spalte beibehalten) können Benutzer bei der Bearbeitung jetzt zusätzliche Spalten hinzufügen.
- Über das Menü _Replace this_ (Ersetzen) wird jetzt das Dialogfeld _Replace Value_ (Wert ersetzen) geöffnet.
- Mit _Replace Value_ (Wert ersetzen) werden Funktionen jetzt wie erwartet transformiert, und es wird kein Fehler mehr ausgelöst.
- Für das Datenvorbereitungspaket wird jetzt der absolute Pfad verwendet, wenn auf Datendateien außerhalb des Projektordners verwiesen wird, sodass das Paket im lokalen Kontext mit dem absoluten Pfad zur Datendatei ausgeführt werden kann.
- _Full file_ (Vollständige Datei) wird jetzt als Strategie für die Stichprobenentnahme unterstützt, wenn Azure Blob als Datenquelle verwendet wird.
- Generierter Python-Code (aus dem Datenvorbereitungspaket) enthält jetzt Wagenrückläufe und Zeilenvorschübe, um die Benutzerfreundlichkeit für Windows zu erhöhen.
- In der Dropdownliste _Auswählen von Metriken_ wird „property“ jetzt ausgeblendet, wenn zur Datenansicht gewechselt wird.
- In Workbench können Parquet-Dateien jetzt auch verarbeitet werden, wenn die Python-Laufzeit verwendet wird. Bisher konnte beim Verarbeiten von Parquet-Dateien nur Spark verwendet werden. 
- Das Herausfiltern von Werten einer Spalte mit dem Datentyp _date_ führt nicht mehr dazu, dass die Datenvorbereitungs-Engine abstürzt.
- In der Metrikansicht werden jetzt Aktualisierungen der Strategie für die Stichprobenentnahme akzeptiert.
- Remoteaufträge für die Stichprobenentnahme funktionieren jetzt richtig.

#### <a name="job-execution"></a>Auftragsausführung
- Das Argument ist jetzt im Ausführungsverlauf-Datensatz enthalten.
- In der CLI ausgelöste Aufträge werden jetzt automatisch im Auftragsbereich „Ausführungsverlauf“ angezeigt.
- Im Auftragsbereich werden jetzt Aufträge angezeigt, die von Gastbenutzern erstellt und dem Azure AD-Mandanten hinzugefügt wurden.
- Die Aktionen zum Abbrechen und Löschen im Auftragsbereich sind jetzt stabiler.
- Beim Klicken auf die Schaltfläche „Ausführen“ wird jetzt eine Fehlermeldung ausgelöst, wenn das Format der Konfigurationsdateien fehlerhaft ist.
- Beim Beenden der App kommt es nicht mehr zu Konflikten mit Aufträgen, die in der CLI ausgelöst wurden.
- Für Aufträge, die in der CLI ausgelöst wurden, wird die „standard-out“-Ausgabe jetzt auch nach einer Stunde der Ausführung fortgesetzt.
- Es werden bessere Fehlermeldungen angezeigt, wenn die Ausführung des Datenvorbereitungspakets in Python/PySpark fehlschlägt.
- Für `az ml experiment clean` werden jetzt auch Docker-Images auf dem virtuellen Remotecomputer bereinigt.
- `az ml experiment clean` funktioniert für das lokale Ziel unter macOS jetzt richtig.
- Fehlermeldungen für Docker-Ausführungen (lokal oder remote) wurden bereinigt und sind einfacher zu lesen.
- Es wird eine bessere Fehlermeldung angezeigt, wenn der Name des Hauptknotens für den HDInsight-Cluster bei Anfügung als Ausführungsziel nicht richtig formatiert ist.
- Es wird eine bessere Fehlermeldung angezeigt, wenn das Geheimnis im Anmeldeinformationsdienst nicht gefunden wird. 
- Die MMLSpark-Bibliothek wurde aktualisiert, damit Apache Spark 2.2 unterstützt wird.
- MMLSpark enthält jetzt eine Transformation für die Antragstellercodierung („Mesh Encoding“) für medizinische Dokumente.
- Version 2.1.0 von `matplotlib` ist jetzt im Lieferumfang von Workbench enthalten.

#### <a name="jupyter-notebook"></a>Jupyter Notebook
- Die Notebook-Namenssuche funktioniert in der Ansicht „Notebooks“ jetzt richtig.
- Sie können ein Notebook jetzt in der Ansicht „Notebooks“ löschen.
- Das neue Magic-Element `%upload_artifact` wurde hinzugefügt, um Dateien, die in der Notebook-Ausführungsumgebung erzeugt wurden, in den Ausführungsverlauf-Datenspeicher hochzuladen.
- Kernel-Fehler werden jetzt im Notebook-Auftragsstatus angezeigt, um das Debuggen zu vereinfachen.
- Der Jupyter-Server wird jetzt richtig heruntergefahren, wenn sich der Benutzer von der App abmeldet.

#### <a name="azure-portal"></a>Azure-Portal
- Das Experimentieren-Konto und das Konto für die Modellverwaltung können jetzt in zwei neuen Azure-Regionen erstellt werden: „Europa, Westen“ und „Asien, Südosten“.
- Der DevTest-Plan für das Konto für die Modellverwaltung ist jetzt nur verfügbar, wenn er im Abonnement als erster Plan erstellt wird. 
- Der Hilfelink im Azure-Portal wurde aktualisiert und führt jetzt zur richtigen Seite der Dokumentation.
- Das Beschreibungsfeld wurde von der Seite mit den Details zum Docker-Image entfernt, da es nicht benötigt wird.
- Der Seite mit den Details zum Webdienst wurden weitere Details hinzugefügt, z.B. AppInsights und Einstellungen für die automatische Skalierung.
- Die Seite für die Modellverwaltung wird jetzt auch gerendert, wenn Cookies von Drittanbietern im Browser deaktiviert sind. 

#### <a name="operationalization"></a>Operationalisierung
- Der Webdienst mit „score“ im Namen führt nicht mehr zu einem Fehler.
- Benutzer können jetzt eine Bereitstellungsumgebung erstellen, für die nur der Zugriff vom Typ „Mitwirkender“ auf eine Azure-Ressourcengruppe oder das Abonnement besteht. Der Besitzerzugriff auf das gesamte Abonnement wird nicht mehr benötigt.
- Für die Operationalisierungs-CLI ist unter Linux jetzt die automatische Vervollständigung für Registerkarten möglich.
- Der Imageerstellungsdienst unterstützt jetzt das Erstellen von Images für Azure IoT-Dienste und -Geräte.

#### <a name="sample-projects"></a>Beispielprojekte
- Beispielprojekt [_Klassifizieren von Iris_](./tutorial-classifying-iris-part-1.md):
    - `iris_pyspark.py` wird umbenannt in `iris_spark.py`.
    - `iris_score.py` wird umbenannt in `score_iris.py`.
    - `iris.dprep` und `iris.dsource` wurden aktualisiert, um die neuesten Aktualisierungen für die Datenvorbereitungs-Engine widerzuspiegeln.
    - Das Notebook `iris.ipynb` wurde geändert, damit es in einem HDInsight-Cluster funktioniert.
    - Der Ausführungsverlauf wurde in Zellen des Notebooks `iris.ipynb` aktiviert.
- Für das Beispielprojekt [_Advanced Data Prep using Bike Share Data_](./tutorial-bikeshare-dataprep.md) (Erweiterte Datenaufbereitung mit Daten für Leihfahrräder) wurde der Schritt „Handle Error Value“ (Behandeln des Fehlerwerts) korrigiert.
- Das `docker.runconfig`-Format des Beispielprojekts [_MMLSpark on Adult Census Data_](https://github.com/Azure/MachineLearningSamples-mmlspark) (MMLSpark für Volkszählungsdaten) wurde von JSON in YAML aktualisiert.
- Das `docker.runconfig`-Format des Beispielprojekts [_Distributed Hyperparameter Tuning_](./scenario-distributed-tuning-of-hyperparameters.md) (Optimierung von verteilten Hyperparametern) wurde von JSON in YAML aktualisiert.
- Es ist ein neues Beispielprojekt mit dem Namen [_Bildklassifizierung mit CNTK_](./scenario-image-classification-using-cntk.md) verfügbar.


## <a name="2017-10-sprint-0"></a>2017-10 (Sprint 0) 
**Versionsnummer**: 0.1.1710.31013  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;([Suchen Sie Ihre Version.](../service/known-issues-and-troubleshooting-guide.md#find-the-workbench-build-number))

Willkommen beim ersten Update für Azure Machine Learning Workbench, das auf unsere erste, auf der Microsoft Ignite 2017-Konferenz vorgestellte Public Preview-Version folgt. Die wichtigsten Änderungen in dieser Version sind Korrekturen für mehr Zuverlässigkeit und Stabilität.  Einige der von uns aufgegriffenen kritischen Punkte sind u.a:

### <a name="new-features"></a>Neue Funktionen
- macOS High Sierra wird nun unterstützt.

### <a name="bug-fixes"></a>Fehlerbehebungen
#### <a name="workbench-experience"></a>Workbench-Oberfläche
- Beim Ziehen und Ablegen einer Datei in Workbench stürzt Workbench ab.
- Das Terminalfenster in Visual Studio Code, das als IDE für Workbench konfiguriert ist, erkennt keine Befehle des Typs _az ml_.

#### <a name="workbench-authentication"></a>Workbench-Authentifizierung
Wir haben eine Reihe von Änderungen vorgenommen, um verschiedene gemeldete Anmelde- und Authentifizierungsprobleme zu korrigieren.
- Das Authentifizierungsfenster wird ständig eingeblendet, insbesondere wenn die Internetverbindung nicht stabil ist.
- Korrigierte Zuverlässigkeitsprobleme im Zusammenhang mit dem Ablauf von Authentifizierungstoken.
- In einigen Fällen wird das Authentifizierungsfenster zweimal angezeigt.
- Im Workbench-Hauptfenster wird immer noch die Meldung zur laufenden Authentifizierung angezeigt, wenn der Authentifizierungsvorgang abgeschlossen ist und das Popupdialogfeld bereits geschlossen wurde.
- Wenn keine Internetverbindung besteht, wird der Authentifizierungsdialog mit einem leeren Bildschirm angezeigt.

#### <a name="data-preparation"></a>Vorbereitung der Daten 
- Wenn ein bestimmter Wert gefiltert wird, werden auch Fehler und fehlende Werte herausgefiltert.
- Wenn Sie eine Stichprobenstrategie ändern, werden nachfolgende vorhandene Join-Vorgänge entfernt.
- Beim Ersetzen der Transformation „Fehlender Wert“ wird NaN nicht berücksichtigt.
- Datumstypableitung bewirkt eine Ausnahme, wenn NULL-Wert gefunden wird.

#### <a name="job-execution"></a>Auftragsausführung
- Es gibt keine eindeutige Fehlermeldung, wenn die Auftragsausführung den Projektordner nicht hochladen kann, weil die Größenbeschränkung überschritten wurde.
- Wenn das Python-Skript des Benutzers das Arbeitsverzeichnis ändert, werden die Dateien, die in die Ausgabeordner geschrieben wurden, nicht nachverfolgt. 
- Wenn sich das aktive Azure-Abonnement von dem des aktuellen Projekts unterscheidet, führt die Auftragsübermittlung zum Fehler 403.
- Wenn Docker nicht vorhanden ist, wird keine eindeutige Fehlermeldung zurückgegeben, sobald der Benutzer versucht, Docker als Ausführungsziel zu verwenden.
- Die RUNCONFIG-Datei wird nicht automatisch gespeichert, wenn der Benutzer auf die Schaltfläche _Ausführen_ klickt.

#### <a name="jupyter-notebook"></a>Jupyter Notebook
- Notebook-Server kann nicht gestartet werden, wenn der Benutzer diesen mit bestimmten Anmeldungstypen verwendet.
- Notebook-Serverfehlermeldungen werden in den für Benutzer sichtbaren Protokollen nicht angezeigt.

#### <a name="azure-portal"></a>Azure-Portal
- Wenn Sie das Design „Dunkel“ des Azure-Portals auswählen, wird das Blatt „Modellverwaltung“ als schwarzes Feld angezeigt.

#### <a name="operationalization"></a>Operationalisierung
- Die Wiederverwendung eines Manifests zur Aktualisierung eines Webdiensts führt zu einem neu erstellten Docker-Image mit einem Zufallsnamen.
- Webdienstprotokolle können nicht aus einem Kubernetes-Cluster abgerufen werden.
- Irreführende Fehlermeldung wird ausgegeben, wenn der Benutzer versucht, ein Modellverwaltungskonto oder ein ML-Computekonto zu erstellen. Zudem treten Berechtigungsprobleme auf.

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie die Übersicht für [Azure Machine Learning](../service/overview-what-is-azure-ml.md).