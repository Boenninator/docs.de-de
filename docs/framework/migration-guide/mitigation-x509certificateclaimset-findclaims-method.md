---
title: 'Entschärfung: X509CertificateClaimSet.FindClaims-Methode'
ms.date: 03/30/2017
ms.assetid: ee356e3b-f932-48f5-875a-5e42340bee63
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b927ed2e68ddea537f87b692d5c3a949234f81f5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33388036"
---
# <a name="mitigation-x509certificateclaimsetfindclaims-method"></a>Entschärfung: X509CertificateClaimSet.FindClaims-Methode
Beginnend mit Apps, die auf [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] ausgerichtet sind, versucht die <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType>-Methode das `claimType`-Argument mit allen DNS-Einträgen in seinem SAN-Feld zu vergleichen.  
  
## <a name="impact"></a>Auswirkungen  
 Diese Änderung betrifft nur Apps, die auf Versionen von .NET Framework ausgerichtet sind, die mit [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] beginnen.  
  
 Bei Apps, die auf frühere Versionen von .NET Framework ausgerichtet sind, versucht die <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims%2A?displayProperty=nameWithType>-Methode, das `claimType`-Argument nur mit dem letzten DNS-Eintrag abzustimmen.  
  
## <a name="mitigation"></a>Minderung  
 Ist diese Änderung nicht erwünscht, kann sie für Apps, die auf Versionen von .NET Framework ausgerichtet sind, die mit [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] beginnen, abgelehnt werden. Dazu muss dem [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md)-Abschnitt der Konfigurationsdatei der App die folgende Konfigurationseinstellung hinzugefügt werden:  
  
```xml  
<runtime>  
   <AppContextSwitchOverrides value="Switch.System.IdentityModel.DisableMultipleDNSEntriesInSANCertificate=true" />   
</runtime>  
```  
  
 Für Apps, die für frühere Versionen von .NET Framework vorgesehen sind, aber unter [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] und höheren Versionen ausgeführt werden, kann dieses Verhalten übernommen werden, indem dem [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md)-Abschnitt der Konfigurationsdatei der Anwendung die folgende Konfigurationseinstellung hinzugefügt wird:  
  
```xml  
<runtime>  
    <AppContextSwitchOverrides value="Switch.System.IdentityModel.DisableMultipleDNSEntriesInSANCertificate=false" />   
</runtime>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Neuausrichtungsänderungen](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-6-1.md)
