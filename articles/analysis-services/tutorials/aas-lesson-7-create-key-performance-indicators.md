---
title: 'Azure Analysis Services-Tutorial – Lektion 7: Erstellen von Key Performance Indicators | Microsoft-Dokumentation'
description: Dieser Artikel beschreibt, wie Key Performance Indicators im Azure Analysis Services-Tutorialprojekt erstellt werden.
author: minewiskan
manager: kfile
ms.service: analysis-services
ms.topic: conceptual
ms.date: 04/12/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 8534640822030a7aa93c8eafe2a1b1a4a8bc5bc4
ms.sourcegitcommit: 9cdd83256b82e664bd36991d78f87ea1e56827cd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-key-performance-indicators"></a>Erstellen von Key Performance Indicators

In dieser Lektion erstellen Sie Key Performance Indicators (KPIs). KPIs werden verwendet, um die Leistung eines Werts zu messen, der von dem *Base*-Measure definiert wird. Dies geschieht anhand eines *Target*-Werts, der ebenfalls von einem Measure oder einem absoluten Wert definiert wird. Mit KPIs können Geschäftsleuten in Berichterstellungsclientanwendungen Zusammenfassungen von Geschäftserfolgen schnell und einfach verstehen bzw. Trends erkennen. Weitere Informationen finden Sie unter [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Voraussetzungen  
Dieses Thema ist Teil eines Tutorials zur Tabellenmodellierung, das in der richtigen Reihenfolge absolviert werden sollte. Bevor Sie diese Lektion beginnen, sollten Sie die vorherige [Lektion 6: Erstellen von Measures](../tutorials/aas-lesson-6-create-measures.md) abgeschlossen haben.   
  
## <a name="create-key-performance-indicators"></a>Erstellen von Key Performance Indicators  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>So erstellen Sie einen KPI „InternetCurrentQuarterSalesPerformance“  
  
1.  Klicken Sie im Modell-Designer auf die Tabelle **FactInternetSales**.  
  
2.  Klicken Sie im Measureraster auf eine leere Zelle.  
  
3.  Geben Sie in der Bearbeitungsleiste über der Tabelle folgende Formel ein: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Dieses Measure fungiert als Basiskennzahl für den KPI.  
  
4.  Klicken Sie im Measureraster mit der rechten Maustaste auf **InternetCurrentQuarterSalesPerformance** > **KPI erstellen**.   
  
5.  Wählen Sie im Dialogfeld „Key Performance Indicator (KPI)“ unter **Target** (Zielwert) **Absolute Value** (Absoluter Wert) aus, und geben Sie anschließend **1,1** ein.  
  
7.  Geben Sie im linken Schiebereglerfeld (niedrig) **1** ein und im rechten Schiebereglerfeld (hoch) **1,07**.  
  
8.  Wählen Sie unter **Symbolart auswählen** die Raute (rot), das Dreieck, (gelb) und den Kreis (grün) aus.
  
    ![aas-lektion7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Beachten Sie die erweiterbare Beschriftung **Beschreibungen** unter den verfügbaren Symbolarten. Verwenden Sie Beschreibungen der verschiedenen KPI-Elemente, damit diese in Clientanwendungen besser voneinander unterschieden werden können.  
  
9. Klicken Sie auf **OK**, um den KPI fertigzustellen.  
  
    Beachten Sie im Measureraster das Symbol neben dem Measure **InternetCurrentQuarterSalesPerformance**. Dieses Symbol gibt an, dass dieses Measure der Basewert für einen KPI ist.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>So erstellen Sie einen KPI „InternetCurrentQuarterMarginPerformance“  
  
1.  Klicken Sie im Measureraster der Tabelle **FactInternetSales** auf eine leere Zelle.  
  
2.  Geben Sie in der Bearbeitungsleiste über der Tabelle folgende Formel ein:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Klicken Sie mit der rechten Maustaste auf **InternetCurrentQuarterMarginPerformance** > **KPI erstellen**.  
  
4.  Wählen Sie im Dialogfeld „Key Performance Indicator (KPI)“ unter **Target** (Zielwert) **Absolute Value** (Absoluter Wert) aus, und geben Sie anschließend **1,25** ein.   
  
5.  Schieben Sie den Regler im linken Schiebereglerfeld (niedrig) bis zu **0,8**, und schieben Sie anschließend den Regler im rechten Schiebereglerfeld (hoch) bis zu **1,03**.  
  
6.  Wählen Sie unter **Symbolart auswählen** die Raute (rot), das Dreieck, (gelb) und den Kreis (grün) aus, und klicken Sie anschließend auf **OK**.  
  
## <a name="whats-next"></a>Wie geht es weiter?
[Lektion 8: Erstellen von Perspektiven](../tutorials/aas-lesson-8-create-perspectives.md)
  
  
