---
title: 'Sichern und Wiederherstellen von Informationen mit Microsoft Authenticator: Azure | Microsoft-Dokumentation'
description: Hier erfahren Sie, wie Sie Ihre Kontoanmeldeinformationen mithilfe der Microsoft Authenticator-App sichern und wiederherstellen.
services: multi-factor-authentication
documentationcenter: ''
author: eross-msft
manager: mtillman
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2018
ms.author: lizross
ms.reviewer: olhaun
ms.custom: end-user
ms.openlocfilehash: 0b76d2debb9814188e5551252e52bd0dae38eb50
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2018
---
# <a name="backup-and-recover-account-credentials-with-the-microsoft-authenticator-app"></a>Sichern und Wiederherstellen von Kontoanmeldeinformationen mithilfe der Microsoft Authenticator-App
**Anwendungsbereich:**

- iOS-Geräte

Die Microsoft Authenticator-App sichert Ihre Kontoanmeldeinformationen und zugehörige App-Einstellungen, etwa die Reihenfolge Ihrer Konten, in der Cloud. Nach dem Sichern können Sie die App auch zum Wiederherstellen der Informationen auf einem neuen Gerät verwenden und dadurch möglicherweise vermeiden, dass Sie gesperrt werden oder Konten neu erstellen müssen.

>[!IMPORTANT]
> Sie benötigen ein persönliches Microsoft-Konto und ein iCloud-Konto für jeden Sicherungsspeicherort. An diesem Speicherort können Sie jedoch mehrere Konten sichern. Sie können beispielsweise ein persönliches Konto, ein Geschäfts-, Schul- oder Unikonto und ein Drittanbieterkonto (etwa Facebook, Google usw.) haben.<br><br>Nur ihre Kontoanmeldeinformationen werden gespeichert. Diese umfassen Ihren Benutzernamen und den achtstelligen Kontoprüfcode, der zum Bestätigen Ihrer Identität bei der Microsoft Authenticator-App erforderlich ist. Es werden keine weiteren Informationen zu Ihrem Konto wie E-Mails oder Dateien gespeichert. Darüber hinaus werden Ihre Konten keinesfalls mit einem anderen Produkt oder Dienst verknüpft oder geteilt. Ihr IT-Administrator erhält ebenfalls keine Informationen zu diesen Konten.

## <a name="back-up-your-account-credentials"></a>Sichern Ihrer Anmeldeinformationen
Bevor Sie Ihre Anmeldeinformationen sichern können, benötigen Sie Folgendes:

- Ein persönliches [Microsoft-Konto](https://account.microsoft.com/account), das als Wiederherstellungskonto fungiert

- Ein [iCloud-Konto](https://www.icloud.com/) für den tatsächlichen Speicherort 

Durch die erforderliche Anmeldung bei beiden Konten erhöht sich die Sicherheit Ihrer Sicherungsinformationen.

**So aktivieren Sie die Cloudsicherung**
-   Wählen Sie auf Ihrem iOS-Gerät **Settings** (Einstellungen) und **Backup** (Sicherung), und aktivieren Sie dann **Auto backup** (Automatische Sicherung).

    Die Anmeldeinformationen für Ihr Konto werden in Ihrem iCloud-Konto gesichert.

    ![Bildschirm mit den iOS-Einstellungen und den Einstellungen für die automatische Sicherung](./media/authenticator-app-backup-and-recovery/backup-and-recovery-turn-on.png)

## <a name="recover-your-account-credentials-on-your-new-device"></a>Wiederherstellen Ihrer Kontoanmeldeinformationen auf einem neuen Gerät
Sie können die Kontoanmeldeinformationen in Ihrem iCloud-Konto mit dem gleichen Microsoft-Wiederherstellungskonto wiederherstellen, das Sie beim Sichern Ihrer Informationen eingerichtet haben.

**So stellen Sie Ihre Informationen wieder her**
1.  Öffnen Sie auf dem iOS-Gerät die Microsoft Authenticator-App, und wählen Sie unten auf dem Bildschirm die Option **Wiederherstellung starten**.

    ![Microsoft Authenticator-App mit hervorgehobener Option „Wiederherstellung starten“](./media/authenticator-app-backup-and-recovery/backup-and-recovery-begin-recovery.png)

2.  Melden Sie sich bei Ihrem Wiederherstellungskonto mit dem gleichen persönlichen Microsoft-Konto an, das Sie während des Wiederherstellungsprozesses verwendet haben.

    Ihre Kontoanmeldeinformationen werden auf dem neuen Gerät wiederhergestellt.

Nach der Wiederherstellung stellen Sie unter Umständen fest, dass die Prüfcodes des persönlichen Microsoft-Kontos in der Microsoft Authenticator-App auf dem alten und dem neuen Smartphone voneinander abweichen. Die Codes unterscheiden sich, da jedes Gerät über eigene eindeutige Anmeldeinformationen verfügt. Beide sind jedoch gültig und können bei der Anmeldung mit dem zugehörigen Smartphone verwendet werden.

## <a name="recover-additional-accounts-requiring-more-verification"></a>Wiederherstellen weiterer Konten, für die ein zusätzlicher Überprüfungsschritt erforderlich ist
Wenn Sie Pushbenachrichtigungen für persönliche Konten oder Geschäfts-, Schul- oder Unikonten verwenden, wird eine Bildschirmmeldung mit dem Hinweis angezeigt, dass zum Wiederherstellen der Informationen eine zusätzliche Überprüfung erforderlich ist. Da für Pushbenachrichtigungen die Verwendung von Anmeldeinformationen erforderlich ist, die mit einem bestimmten Gerät verknüpft sind und nie über das Netzwerk gesendet werden, müssen Sie Ihre Identität bestätigen, bevor die Anmeldeinformationen auf dem Gerät erstellt werden.

Bei persönlichen Microsoft-Konten können Sie Ihre Identität bestätigen, indem Sie Ihr Kennwort zusammen mit einer alternativen E-Mail-Adresse oder Telefonnummer eingeben. Bei Geschäfts-, Schul- oder Unikonten müssen Sie einen QR-Code scannen, den Sie vom Kontoanbieter erhalten.

**So führen Sie einen zusätzlichen Überprüfungsschritt für persönliche Konten aus**
1.  Klicken Sie in der Microsoft Authenticator-App auf dem Bildschirm **Konten** auf den Dropdownpfeil neben dem Konto, das Sie wiederherstellen möchten.

    ![Microsoft Authenticator-App mit den verfügbaren Konten und den zugehörigen Dropdownpfeilen](./media/authenticator-app-backup-and-recovery/backup-and-recovery-arrow.png)

2.  Klicken Sie auf **Sign in to recover** (Zur Wiederherstellung anmelden), geben Sie Ihr Kennwort ein, und bestätigen Sie in einem zusätzlichen Überprüfungsschritt Ihre E-Mail-Adresse oder Telefonnummer.

    ![Microsoft Authenticator-App, die die Eingabe der Anmeldeinformationen ermöglicht](./media/authenticator-app-backup-and-recovery/backup-and-recovery-sign-in.png)

**So führen Sie einen zusätzlichen Überprüfungsschritt für Geschäfts-, Schul- oder Unikonten aus**
1.  Klicken Sie in der Microsoft Authenticator-App auf dem Bildschirm **Konten** auf den Dropdownpfeil neben dem Konto, das Sie wiederherstellen möchten.

    ![Microsoft Authenticator-App mit den verfügbaren Konten und den zugehörigen Dropdownpfeilen](./media/authenticator-app-backup-and-recovery/backup-and-recovery-additonal-accts.png)

2.  Wählen Sie **Scan QR code to recover** (Zur Wiederherstellung QR-Code scannen), und scannen Sie dann den vom Administrator bereitgestellten QR-Code.

    ![Microsoft Authenticator-App, die das Scannen des QR-Codes ermöglicht](./media/authenticator-app-backup-and-recovery/backup-and-recovery-scan-qr-code.png)

## <a name="troubleshooting-backup-and-recovery-problems"></a>Beheben von Problemen bei Sicherung und Wiederherstellung
Es gibt einige Gründe, warum die Sicherung möglicherweise nicht verfügbar ist:

-   **Änderung der Betriebssysteme.** Die Sicherung wird mit der vom Betriebssystem des Smartphones bereitgestellten Cloudspeicheroption gespeichert. Das bedeutet, dass die Sicherung nicht verfügbar ist, wenn Sie zwischen Android und iOS wechseln. In diesem Fall müssen Sie Ihr Konto in der App manuell neu erstellen.

-   **Netzwerk- oder Kennwortprobleme.** Stellen Sie sicher, dass eine Verbindung mit einem Netzwerk besteht und Sie mit der gleichen AppleID bei Ihrem iCloud-Konto angemeldet sind, die Sie auch auf dem letzten iPhone verwendet haben.

-   **Versehentliche Löschung.** Möglicherweise haben Sie Ihr Sicherungskonto auf dem alten Gerät oder beim Verwalten des Cloudspeicherkontos gelöscht. In diesem Fall müssen Sie Ihr Konto in der App manuell neu erstellen.

-   **Vorhandene Microsoft Authenticator-Konten.** Wenn Sie in der Microsoft Authenticator-App bereits Konten eingerichtet haben, kann die App die gesicherten Konten nicht wiederherstellen. Durch das Verhindern der Wiederherstellung wird sichergestellt, dass Ihre Kontodetails nicht mit veralteten Informationen überschrieben werden. In diesem Fall müssen Sie alle vorhandenen Kontoinformationen aus den in der Authenticator-App eingerichteten Konten entfernen, damit Sie die Sicherung wiederherstellen können.

## <a name="next-steps"></a>Nächste Schritte
Sie haben Ihre Kontoinformationen gesichert und auf dem neuen Gerät wiederhergestellt und können nun mit der Microsoft Authenticator-App Ihre Identität bestätigen.

## <a name="related-topics"></a>Verwandte Themen
- [Erste Schritte mit der Microsoft Authenticator-App](microsoft-authenticator-app-how-to.md)  

- [Mit dem Telefon anmelden](microsoft-authenticator-app-phone-signin-faq.md)

- [Microsoft Authenticator-App – häufig gestellte Fragen](microsoft-authenticator-app-faq.md)

- [Multi-Factor Authentication](https://docs.microsoft.com/en-us/azure/multi-factor-authentication/)