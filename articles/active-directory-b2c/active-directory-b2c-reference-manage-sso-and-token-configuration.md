---
title: Verwalten von SSO und der Tokenanpassung mit benutzerdefinierten Richtlinien | Microsoft-Dokumentation
description: Erfahren Sie mehr über die Verwaltung von SSO und der Tokenanpassung mit benutzerdefinierten Richtlinien.
services: active-directory-b2c
documentationcenter: ''
author: davidmu
manager: mtillman
editor: ''
ms.service: active-directory-b2c
ms.workload: identity
ms.topic: article
ms.date: 05/02/2017
ms.author: davidmu
ms.openlocfilehash: c9eb7f7711a8987945b8aeaee8d6798b7a6b8284
ms.sourcegitcommit: 48ab1b6526ce290316b9da4d18de00c77526a541
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="azure-active-directory-b2c-manage-sso-and-token-customization-with-custom-policies"></a>Azure Active Directory B2C: Verwalten von SSO und der Tokenanpassung mit benutzerdefinierten Richtlinien
Bei Verwendung von benutzerdefinierten Richtlinien haben Sie die gleiche Kontrolle über Ihre Konfigurationen für die Bereiche für Token, Sitzung und einmaliges Anmelden (Single Sign-On, SSO) wie mit integrierten Richtlinien.  Informationen zu den einzelnen Einstellungen finden Sie in [dieser Dokumentation](#active-directory-b2c-token-session-sso).

## <a name="token-lifetimes-and-claims-configuration"></a>Tokengültigkeitsdauern und Anspruchskonfiguration
Zum Ändern der Einstellungen für Ihre Tokengültigkeitsdauern müssen Sie in der Datei der vertrauenden Seite für die gewünschte Richtlinie ein `<ClaimsProviders>`-Element hinzufügen.  Das `<ClaimsProviders>`-Element ist ein untergeordnetes Element von `<TrustFrameworkPolicy>`.  Darin fügen Sie die Informationen ein, die sich auf Ihre Tokengültigkeitsdauern auswirken.  Der XML-Code sieht wie folgt aus:

```XML
<ClaimsProviders>
   <ClaimsProvider>
      <DisplayName>Token Issuer</DisplayName>
      <TechnicalProfiles>
         <TechnicalProfile Id="JwtIssuer">
            <Metadata>
               <Item Key="token_lifetime_secs">3600</Item>
               <Item Key="id_token_lifetime_secs">3600</Item>
               <Item Key="refresh_token_lifetime_secs">1209600</Item>
               <Item Key="rolling_refresh_token_lifetime_secs">7776000</Item>
               <Item Key="IssuanceClaimPattern">AuthorityAndTenantGuid</Item>
               <Item Key="AuthenticationContextReferenceClaimPattern">None</Item>
            </Metadata>
         </TechnicalProfile>
      </TechnicalProfiles>
   </ClaimsProvider>
</ClaimsProviders>
```

**Access token lifetimes (Gültigkeitsdauer Zugriffstoken)** Sie können die Gültigkeitsdauer des Zugriffstokens ändern, indem Sie den Wert im `<Item>`-Element mit Key="token_lifetime_secs" anpassen (Sekunden).  Der integrierte Standardwert beträgt 3.600 Sekunden (60 Minuten).

**ID token lifetime (Gültigkeitsdauer ID-Token)** Sie können die Gültigkeitsdauer des ID-Tokens ändern, indem Sie den Wert im `<Item>`-Element mit Key="id_token_lifetime_secs" anpassen (Sekunden).  Der integrierte Standardwert beträgt 3.600 Sekunden (60 Minuten).

**Refresh token lifetime (Gültigkeitsdauer Aktualisierungstoken)** Sie können die Gültigkeitsdauer des Aktualisierungstokens ändern, indem Sie den Wert im `<Item>`-Element mit Key="refresh_token_lifetime_secs" anpassen (Sekunden).  Der integrierte Standardwert beträgt 1.209.600 Sekunden (14 Tage).

**Refresh token sliding window lifetime (Lebensdauer für gleitendes Fenster des Aktualisierungstokens)** Wenn Sie die Lebensdauer für das gleitende Fenster des Aktualisierungstokens festlegen möchten, können Sie den Wert in `<Item>` mit Key="rolling_refresh_token_lifetime_secs" ändern (Sekunden).  Der integrierte Standardwert beträgt 7.776.000 Sekunden (90 Tage).  Falls Sie keine Gültigkeitsdauer für das gleitende Fenster erzwingen möchten, ersetzen Sie diese Zeile wie folgt:
```XML
<Item Key="allow_infinite_rolling_refresh_token">True</Item>
```

**Issuer (iss) claim (Ausstelleranspruch)** Wenn Sie den Ausstelleranspruch ändern möchten, können Sie den Wert in `<Item>` mit Key="IssuanceClaimPattern" anpassen.  Die gültigen Werte sind `AuthorityAndTenantGuid` und `AuthorityWithTfp`.

**Setting claim representing policy ID (Festlegen des Anspruchs, der die Richtlinien-ID darstellt)** Die Optionen zum Festlegen dieses Werts sind „TFP“ (Vertrauensframework-Richtlinie) und „ACR“ (Authentifizierungskontext-Referenz).  
Wir empfehlen Ihnen, diese Option auf „TFP“ festzulegen. Stellen Sie hierfür sicher, dass `<Item>` mit Key="AuthenticationContextReferenceClaimPattern" vorhanden ist und der Wert `None` lautet.
Fügen Sie in Ihrem `<OutputClaims>`-Element dieses Element hinzu:
```XML
<OutputClaim ClaimTypeReferenceId="trustFrameworkPolicy" Required="true" DefaultValue="{policy}" />
```
Entfernen Sie für ACR `<Item>` mit Key="AuthenticationContextReferenceClaimPattern".

**Subject (sub) claim (Anspruch „Antragsteller“)** Diese Option hat standardmäßig den Wert „ObjectID“. Gehen Sie wie folgt vor, wenn Sie die Umstellung auf `Not Supported` durchführen möchten:

Ersetzen Sie diese Zeile: 
```XML
<OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub" />
```
Durch diese Zeile:
```XML
<OutputClaim ClaimTypeReferenceId="sub" />
```

## <a name="session-behavior-and-sso"></a>Sitzungsverhalten und SSO
Zum Ändern Ihres Sitzungsverhaltens und der SSO-Konfigurationen ist es erforderlich, dass Sie im `<RelyingParty>`-Element ein `<UserJourneyBehaviors>`-Element hinzufügen.  Auf das `<UserJourneyBehaviors>`-Element muss unmittelbar `<DefaultUserJourney>` folgen.  Das `<UserJourneyBehavors>`-Element sollte Folgendes enthalten:

```XML
<UserJourneyBehaviors>
   <SingleSignOn Scope="Application" />
   <SessionExpiryType>Absolute</SessionExpiryType>
   <SessionExpiryInSeconds>86400</SessionExpiryInSeconds>
</UserJourneyBehaviors>
```
**Single sign-on (SSO) configuration (Einmaliges Anmelden (SSO) – Konfiguration)** Zum Ändern der Konfiguration des einmaligen Anmeldens müssen Sie den Wert von `<SingleSignOn>` ändern.  Die gültigen Werte sind `Tenant`, `Application`, `Policy` und `Disabled`. 

**Web app session lifetime (minutes) (Lebensdauer der Web-App-Sitzung (Minuten))** Zum Ändern der Lebensdauer der Web-App-Sitzung müssen Sie den Wert des `<SessionExpiryInSeconds>`-Elements ändern.  Der Standardwert von integrierten Richtlinien beträgt 86.400 Sekunden (1.440 Minuten).

**Web app session timeout (Timeout für Web-App-Sitzung)** Zum Ändern des Timeouts für Web-App-Sitzung müssen Sie den Wert von `<SessionExpiryType>` anpassen.  Die gültigen Werte sind `Absolute` und `Rolling`.
