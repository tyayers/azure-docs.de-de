---
title: Zweistufige Überprüfung und AD FS – Azure MFA | Microsoft-Dokumentation
description: Auf dieser Seite zur Azure Multi-Factor Authentication werden die ersten Schritte mit Azure MFA und AD FS beschrieben.
services: multi-factor-authentication
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: joflore
ms.openlocfilehash: 77e7bec69b2f8d237b6e71d13b88fd26c104fc23
ms.sourcegitcommit: fa493b66552af11260db48d89e3ddfcdcb5e3152
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2018
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Erste Schritte mit Azure Multi-Factor Authentication und Active Directory-Verbunddiensten
<center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Wenn Ihre Organisation über einen Verbund Ihres lokalen Active Directory mit Azure Active Directory über AD FS verfügt, gibt es zwei Optionen für die Verwendung von Multi-Factor Authentication.

* Sichern von Cloud-Ressourcen mit Azure Multi-Factor Authentication oder Active Directory-Verbunddiensten
* Sichern von Cloud- und lokalen Ressourcen mithilfe von Azure Multi-Factor Authentication-Server

In der folgenden Tabelle sind die Überprüfungsverfahren beim Sichern von Ressourcen mit Azure Multi-Factor Authentication und AD FS zusammengefasst.

| Überprüfungsvorgang bei browserbasierten Apps | Überprüfungsvorgang bei Nicht-Browser-Apps |
|:--- |:--- |:--- |
| Sichern von Azure AD-Ressourcen mit Azure Multi-Factor Authentication |<li>Der erste Überprüfungsschritt erfolgt lokal über AD FS.</li> <li>Der zweite Schritt ist eine telefonbasierte Methode mithilfe der Cloudauthentifizierung.</li> |
| Sichern von Azure AD-Ressourcen mit Active Directory-Verbunddiensten |<li>Der erste Überprüfungsschritt erfolgt lokal über AD FS.</li><li>Der zweite Schritt wird lokal unter Berücksichtigung des Anspruchs ausgeführt.</li> |

Sicherheitshinweise zu App-Kennwörtern für Verbundbenutzer:

* App-Kennwörter werden über die Cloudauthentifizierung überprüft, daher werden Verbunde umgangen. Der Verbund wird nur beim Einrichten eines App-Kennworts aktiv verwendet.
* Lokale Einstellungen für die Clientzugriffssteuerung werden von App-Kennwörtern nicht berücksichtigt.
* Wenn Sie App-Kennwörter verwenden, geht die Möglichkeit zum lokalen Protokollieren der Authentifizierung verloren.
* Das Deaktivieren oder Löschen von Konten kann für die Verzeichnissynchronisierung bis zu drei Stunden dauern, sodass das Deaktivieren bzw. Löschen von App-Kennwörtern in der Cloudidentität verzögert wird.

Informationen zum Einrichten von Azure Multi-Factor Authentication oder des Azure Multi-Factor Authentication-Servers mit AD FS finden Sie in den folgenden Artikeln:

* [Sichern von Cloudressourcen mit Azure Multi-Factor Authentication und AD FS](howto-mfa-adfs.md)
* [Sichern von Cloud- und lokalen Ressourcen mithilfe von Azure Multi-Factor Authentication-Server mit Windows Server 2012 R2 AD FS](howto-mfaserver-adfs-2012.md)
* [Sichern von Cloud- und lokalen Ressourcen mithilfe von Azure Multi-Factor Authentication-Server mit AD FS 2.0](howto-mfaserver-adfs-2.md)
