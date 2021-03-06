---
title: Verwenden von Zeppelin zum Ausführen von Hive-Abfragen in Azure HDInsight | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Zeppelin zum Ausführen von Hive-Abfragen verwenden.
keywords: hdinsight, hadoop, hive, interactive query, LLAP
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ''
ms.service: hdinsight
ms.custom: hdinsightactive,
ms.devlang: na
ms.topic: conceptual
ms.date: 09/26/2017
ms.author: jgao
ms.openlocfilehash: 59e8e40360702d623827f6784856b874ca629591
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="use-zeppelin-to-run-hive-queries-in-azure-hdinsight"></a>Verwenden von Zeppelin zum Ausführen von Hive-Abfragen in Azure HDInsight 

Interactive Query-Cluster von HDInsight umfassen Zeppelin-Notebooks, die Sie verwenden können, um interaktive Hive-Abfragen auszuführen. In diesem Artikel erfahren Sie, wie Sie Zeppelin zum Ausführen von Hive-Abfragen in Azure HDInsight verwenden. 

## <a name="prerequisites"></a>Voraussetzungen
Bevor Sie diesen Artikel durchgehen können, benötigen Sie Folgendes:

* **Interactive Query-Cluster von HDInsight**. Informationen zum Erstellen eines HDInsight-Clusters finden Sie unter [Cluster erstellen](hadoop/apache-hadoop-linux-tutorial-get-started.md#create-cluster).  Wählen Sie den Typ „Interactive Query“ aus. 

## <a name="create-a-zeppelin-note"></a>Erstellen einer Zeppelin-Notiz

1. Navigieren Sie zu folgender URL:

        https://CLUSTERNAME.azurehdinsight.net/zeppelin
    Ersetzen Sie **CLUSTERNAME** durch den Namen Ihres Clusters.

2. Geben Sie Ihren Hadoop-Benutzernamen und Ihr Kennwort ein. Auf der Zeppelin-Seite können Sie entweder eine neue Notiz erstellen oder vorhandene Notizen öffnen. HiveSample enthält einige Beispiel-Hive-Abfragen.  

    ![HDInsight Interactive Query Zeppelin](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin.png)
3. Klicken Sie auf **Create new Note** (Neue Notiz erstellen).
4. Geben Sie folgende Werte ein bzw. wählen diese aus:

    - Notizname: Geben Sie einen Namen für die Notiz ein.
    - Standardinterpreter: Wählen Sie **JDBC** aus.

5. Klicken Sie auf **Create Note** (Notiz erstellen).
6. Führen Sie die folgende Hive-Abfrage aus:

        %jdbc(hive)
        show tables

    ![HDInsight Interactive Query Zeppelin führt Abfrage aus](./media/hdinsight-connect-hive-zeppelin/hdinsight-hive-zeppelin-query.png)

    Die Anweisung **%jdbc(hive)** in der ersten Zeile gibt dem Notebook an, dass es den Hive-JDBC-Interpreter verwenden soll.

    Die Abfrage soll eine Hive-Tabelle namens *hivesampletable* zurückgeben.

    Es folgen zwei weitere Hive-Abfragen, die Sie auf „hivesampletable“ ausführen können. 

        %jdbc(hive)
        select * from hivesampletable limit 10

        %jdbc(hive)
        select ${group_name}, count(*) as total_count
        from hivesampletable
        group by ${group_name=market,market|deviceplatform|devicemake}
        limit ${total_count=10}

    Verglichen mit früheren Hive-Abfragen werden die Abfrageergebnisse viel schneller zurückgegeben.


## <a name="next-steps"></a>Nächste Schritte
In diesem Artikel haben Sie gelernt, wie Sie Daten aus HDInsight mithilfe von Power BI visualisieren.  Weitere Informationen finden Sie in den folgenden Artikeln:

* [Visualize Hive data with Microsoft Power BI in Azure HDInsight (Visualisieren von Hive-Daten mit Microsoft Power BI in Azure HDInsight)](hadoop/apache-hadoop-connect-hive-power-bi.md).
* [Visualisieren von Interactive Query-Hive-Daten mit Power BI in Azure HDInsight](./interactive-query/apache-hadoop-connect-hive-power-bi-directquery.md)
* [Verbinden von Excel mit Hadoop in Azure HDInsight mithilfe des Microsoft Hive ODBC-Treibers](hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).
* [Verbinden von Excel mit Hadoop mithilfe von Power Query](hadoop/apache-hadoop-connect-excel-power-query.md).
* [Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio (Verbinden mit Azure HDInsight und Ausführen von Hive-Abfragen mithilfe von Data Lake-Tools für Visual Studio)](hadoop/apache-hadoop-visual-studio-tools-get-started.md).
* [Verwenden von Azure HDInsight-Tools für Visual Studio Code](hdinsight-for-vscode.md)
* [Upload data to HDInsight (Hochladen von Daten in HDInsight)](./hdinsight-upload-data.md).
