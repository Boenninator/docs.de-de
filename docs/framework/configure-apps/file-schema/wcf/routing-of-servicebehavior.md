---
title: '&lt;routing&gt; von &lt;serviceBehavior&gt;'
ms.date: 03/30/2017
ms.assetid: d8f9c844-4629-4a45-9599-856dc8f01794
ms.openlocfilehash: 5fb7febe365f73acf09ba74b07215fe9cc659efb
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
ms.locfileid: "32750751"
---
# <a name="ltroutinggt-of-ltservicebehaviorgt"></a>&lt;routing&gt; von &lt;serviceBehavior&gt;
Bietet Laufzeitzugriff auf den Routingdienst, um eine dynamische Änderung der Routingkonfiguration zu ermöglichen.  
  
 \<system.ServiceModel>  
\<behaviors>  
\<serviceBehaviors>  
\<Verhalten >  
\<Routing >  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<behaviors>
  <serviceBehaviors>
    <behavior name="String">
      <routing filterTable="String" 
               routeOnHeadersOnly="Boolean" 
               SoapProcessingEnabled="Boolean" />
    </behavior>
  </serviceBehaviors>
</behaviors>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|filterTable|Eine Zeichenfolge, die den Namen der Routingtabelle angibt, die Filter enthält, die vom Routingdienst ausgewertet werden sollen. Dieser Wert übereinstimmen der `name` Attribut eine [ \<FilterTable >](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertable.md) Element in der [ \<FilterTables >](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertables.md) Abschnitt.|  
|routeOnHeaderOnly|Ein boolescher Wert, der angibt, ob der Filter sowohl den Nachrichtentext als auch den Header oder nur den Header prüft. Die Standardeinstellung ist `true`.|  
|soapProcessingEnabled|Ein boolescher Wert, der angibt, ob SOAP-Verarbeitung erfolgen soll.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<behavior>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Gibt ein Verhaltenselement an.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn dieses Konfigurationselement der Verhaltenskonfiguration des Diensts hinzugefügt wird, aktiviert es Routing für den Dienst. Sie können die Routingtabelle angeben, die vom Dienst in diesem Element verwendet werden soll.  
  
 Mit diesem Konfigurationsabschnitt können Sie die Routingeinstellungen dynamisch ändern, wenn sich das Bereitstellungsmuster ändert. Zur Laufzeit können Sie eine eigene Routingerweiterung mit neuen Routingeinstellungen registrieren, und der Routingdienst verwendet die aktualisierten Konfigurationsinformationen für neue Nachrichten und Sitzungen, während die Regeln für Nachrichten/Sitzungen in Bearbeitung nicht geändert werden.  So erhalten Sie die Möglichkeit, den Routingdienst zur Laufzeit sitzungssicher neu zu konfigurieren.  
  
