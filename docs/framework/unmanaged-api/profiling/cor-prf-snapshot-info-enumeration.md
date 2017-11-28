---
title: COR_PRF_SNAPSHOT_INFO-Enumeration
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COR_PRF_SNAPSHOT_INFO
api_location: mscorwks.dll
api_type: COM
f1_keywords: COR_PRF_SNAPSHOT_INFO
helpviewer_keywords: COR_PRF_SNAPSHOT_INFO enumeration [.NET Framework profiling]
ms.assetid: a5906b2a-ad4a-4cc6-a421-2d7d8adf7468
topic_type: apiref
caps.latest.revision: "15"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: a9c854360881426f2fc7fc9e401da1dc93b9bd84
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="corprfsnapshotinfo-enumeration"></a>COR_PRF_SNAPSHOT_INFO-Enumeration
Gibt an, wie viel Sichern von Daten an, mit einer Stapelmomentaufnahme bei jedem Aufruf an des Profilers [StackSnapshotCallback](../../../../docs/framework/unmanaged-api/profiling/stacksnapshotcallback-function.md) Funktion.  
  
## <a name="syntax"></a>Syntax  
  
```  
typedef enum _COR_PRF_SNAPSHOT_INFO {  
    COR_PRF_SNAPSHOT_DEFAULT = 0x0,  
    COR_PRF_SNAPSHOT_REGISTER_CONTEXT = 0x1,  
    COR_PRF_SNAPSHOT_X86_OPTIMIZED = 0X2  
} COR_PRF_SNAPSHOT_INFO;  
```  
  
## <a name="members"></a>Member  
  
|Mitglieder|Beschreibung|  
|-------------|-----------------|  
|`COR_PRF_SNAPSHOT_DEFAULT`|Gibt an, dass für alle Werte übergeben werden müssen `StackSnapshotCallback` Parameter, mit Ausnahme der `context` Parameter.|  
|`COR_PRF_SNAPSHOT_REGISTER_CONTEXT`|Gibt an, dass für alle Werte übergeben werden müssen `StackSnapshotCallback` Parameter, einschließlich der `context` Parameter.|  
|`COR_PRF_SNAPSHOT_X86_OPTIMIZED`|Gibt an, dass ein einfacherer und alternativer Stackwalk Algorithmus verwendet werden.|  
  
## <a name="remarks"></a>Hinweise  
 Werte, die von bereitgestellt werden die `COR_PRF_SNAPSHOT_INFO` -Enumeration als Parameter übergeben werden die [DoStackSnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) Methode.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [DoStackSnapshot-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md)  
 [Profilerstellungsenumerationen](../../../../docs/framework/unmanaged-api/profiling/profiling-enumerations.md)