---
title: ICLRMetaHostPolicy-Schnittstelle
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRMetaHostPolicy
api_location: mscoree.dll
api_type: COM
f1_keywords: ICLRMetaHostPolicy
helpviewer_keywords: ICLRMetaHostPolicy interface [.NET Framework hosting]
ms.assetid: 1bdeccb6-0698-4c97-ad69-eae2b69e59f1
topic_type: apiref
caps.latest.revision: "23"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 6b8cbe1d397e1214cfa4d3f4cbc3d6cdf2d3ccd5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="iclrmetahostpolicy-interface"></a><span data-ttu-id="2494f-102">ICLRMetaHostPolicy-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="2494f-102">ICLRMetaHostPolicy Interface</span></span>
<span data-ttu-id="2494f-103">Stellt die [GetRequestedRuntime](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) -Methode, die einen Zeiger auf eine common Language Runtime (CLR)-Schnittstelle basierend auf einer Richtlinie Kriterien zurückgibt, verwaltete Assembly, die Version und die Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="2494f-103">Provides the [GetRequestedRuntime](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) method, which returns a pointer to a common language runtime (CLR) interface based on a policy criteria, managed assembly, version and configuration file.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="2494f-104">Methoden</span><span class="sxs-lookup"><span data-stu-id="2494f-104">Methods</span></span>  
  
|<span data-ttu-id="2494f-105">Methode</span><span class="sxs-lookup"><span data-stu-id="2494f-105">Method</span></span>|<span data-ttu-id="2494f-106">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="2494f-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="2494f-107">GetRequestedRuntime-Methode</span><span class="sxs-lookup"><span data-stu-id="2494f-107">GetRequestedRuntime Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md)|<span data-ttu-id="2494f-108">Bietet eine bevorzugte CLR-Schnittstelle auf der Grundlage einer Richtlinie Kriterien sowie eine verwaltete Assembly, die Version und die Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="2494f-108">Provides a preferred CLR interface based on a policy criteria, managed assembly, version, and configuration file.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="2494f-109">Hinweise</span><span class="sxs-lookup"><span data-stu-id="2494f-109">Remarks</span></span>  
 <span data-ttu-id="2494f-110">Sie erhalten einen Verweis auf diese Schnittstelle durch Aufrufen der [CLRCreateInstance](../../../../docs/framework/unmanaged-api/hosting/clrcreateinstance-function.md) -Funktion wie im folgenden Code gezeigt:</span><span class="sxs-lookup"><span data-stu-id="2494f-110">You can get a reference to this interface by calling the [CLRCreateInstance](../../../../docs/framework/unmanaged-api/hosting/clrcreateinstance-function.md) function as shown in the following code:</span></span>  
  
```  
ICLRMetaHostPolicy *pMetaHostPolicy = NULL;  
HRESULT hr = CLRCreateInstance(CLSID_CLRMetaHostPolicy,  
                   IID_ICLRMetaHostPolicy, (LPVOID*)&pMetaHostPolicy);  
```  
  
> [!NOTE]
>  <span data-ttu-id="2494f-111">Diese Schnittstelle nicht lädt oder aktiviert die CLR, sondern einfach gibt die bevorzugte CLR-Version anhand der verfügbaren Versionen, die installiert oder geladen werden.</span><span class="sxs-lookup"><span data-stu-id="2494f-111">This interface does not actually load or activate the CLR, but simply returns the preferred CLR version based on the available versions that are installed or loaded.</span></span>  
  
 <span data-ttu-id="2494f-112">Die [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] Richtlinien hosting-API konsolidiert werden, sodass die Hosts mit spezifischen Anforderungen Grundfunktionen verwenden können, ohne dass das unbeabsichtigte Strafen anfallen.</span><span class="sxs-lookup"><span data-stu-id="2494f-112">The [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] hosting API consolidates policies so that hosts with specific needs may use basic functionality without incurring unintended penalties.</span></span> <span data-ttu-id="2494f-113">Beispielsweise werden viele der Exporte "Mscoree.dll" zu einer bestimmten CLR binden, obwohl eine Methode nicht logisch erfordert möglicherweise.</span><span class="sxs-lookup"><span data-stu-id="2494f-113">For example, many of the MSCorEE.dll exports will bind to a specific CLR, although a method might not logically require it.</span></span> <span data-ttu-id="2494f-114">Die [METAHOST_POLICY_FLAGS](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md) Enumeration stellt Bindungsrichtlinien für die, die für die Mehrheit der Hosts gelten.</span><span class="sxs-lookup"><span data-stu-id="2494f-114">The [METAHOST_POLICY_FLAGS](../../../../docs/framework/unmanaged-api/hosting/metahost-policy-flags-enumeration.md) enumeration provides binding policies that are common to the majority of hosts.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="2494f-115">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="2494f-115">Requirements</span></span>  
 <span data-ttu-id="2494f-116">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="2494f-116">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="2494f-117">**Header:** MetaHost.h</span><span class="sxs-lookup"><span data-stu-id="2494f-117">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="2494f-118">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="2494f-118">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="2494f-119">**.NET Framework-Versionen:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="2494f-119">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="2494f-120">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="2494f-120">See Also</span></span>  
 [<span data-ttu-id="2494f-121">CLR-Hostingschnittstellen hinzugefügt in .NET Framework 4 und 4.5</span><span class="sxs-lookup"><span data-stu-id="2494f-121">CLR Hosting Interfaces Added in the .NET Framework 4 and 4.5</span></span>](../../../../docs/framework/unmanaged-api/hosting/clr-hosting-interfaces-added-in-the-net-framework-4-and-4-5.md)  
 [<span data-ttu-id="2494f-122">Hosten von Schnittstellen</span><span class="sxs-lookup"><span data-stu-id="2494f-122">Hosting Interfaces</span></span>](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)  
 [<span data-ttu-id="2494f-123">Hosting</span><span class="sxs-lookup"><span data-stu-id="2494f-123">Hosting</span></span>](../../../../docs/framework/unmanaged-api/hosting/index.md)