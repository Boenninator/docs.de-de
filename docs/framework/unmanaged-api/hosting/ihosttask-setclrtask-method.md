---
title: IHostTask::SetCLRTask-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostTask.SetCLRTask
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostTask::SetCLRTask
helpviewer_keywords:
- SetCLRTask method [.NET Framework hosting]
- IHostTask::SetCLRTask method [.NET Framework hosting]
ms.assetid: e9d39c80-41a1-49e7-bb5e-ea3433bfb5d7
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 54706b1c3a6ea1864137e2eca135fa6bd883b345
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="ihosttasksetclrtask-method"></a><span data-ttu-id="e1f9d-102">IHostTask::SetCLRTask-Methode</span><span class="sxs-lookup"><span data-stu-id="e1f9d-102">IHostTask::SetCLRTask Method</span></span>
<span data-ttu-id="e1f9d-103">Ordnet eine `ICLRTask` Instanz mit dem aktuellen [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md) Instanz.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-103">Associates an `ICLRTask` instance with the current [IHostTask](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md) instance.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="e1f9d-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="e1f9d-104">Syntax</span></span>  
  
```  
HRESULT SetCLRTask (  
    [in] ICLRTask *pCLRTask  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="e1f9d-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="e1f9d-105">Parameters</span></span>  
 `pCLRTask`  
 <span data-ttu-id="e1f9d-106">[in] Einen Schnittstellenzeiger auf die `ICLRTask` Instanz mit dem aktuellen zugeordnet werden soll `IHostTask` Instanz.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-106">[in] An interface pointer to the `ICLRTask` instance to be associated with the current `IHostTask` instance.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="e1f9d-107">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="e1f9d-107">Return Value</span></span>  
  
|<span data-ttu-id="e1f9d-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="e1f9d-108">HRESULT</span></span>|<span data-ttu-id="e1f9d-109">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="e1f9d-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="e1f9d-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="e1f9d-110">S_OK</span></span>|<span data-ttu-id="e1f9d-111">`SetCLRTask`wurde erfolgreich zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-111">`SetCLRTask` returned successfully.</span></span>|  
|<span data-ttu-id="e1f9d-112">HOST_E_CLRNOTAVAILABLE ZURÜCK</span><span class="sxs-lookup"><span data-stu-id="e1f9d-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="e1f9d-113">Die common Language Runtime (CLR) wurde nicht in einen Prozess geladen, oder die CLR wird in einem Zustand, in dem er nicht verwalteten Code ausführen oder den Aufruf erfolgreich verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-113">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="e1f9d-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="e1f9d-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="e1f9d-115">Der Aufruf ist ein Timeout aufgetreten.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-115">The call timed out.</span></span>|  
|<span data-ttu-id="e1f9d-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="e1f9d-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="e1f9d-117">Der Aufrufer ist nicht Besitzer der Sperre.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="e1f9d-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="e1f9d-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="e1f9d-119">Ein Ereignis wurde abgebrochen, während ein blockierten Thread oder eine Fiber darauf gewartet.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="e1f9d-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="e1f9d-120">E_FAIL</span></span>|<span data-ttu-id="e1f9d-121">Ein Unbekannter Schwerwiegender Fehler aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="e1f9d-122">Wenn eine Methode E_FAIL zurückgibt, ist die CLR nicht mehr verwendbar innerhalb des Prozesses.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="e1f9d-123">Nachfolgende Aufrufe zum Hosten der Methoden HOST_E_CLRNOTAVAILABLE zurück.</span><span class="sxs-lookup"><span data-stu-id="e1f9d-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="e1f9d-124">Hinweise</span><span class="sxs-lookup"><span data-stu-id="e1f9d-124">Remarks</span></span>  
 <span data-ttu-id="e1f9d-125">Die CLR ruft `SetCLRTask` Zuordnen einer `ICLRTask` Instanz mit dem aktuellen `IHostTask` -Instanz, die durch einen Aufruf erstellt wurde [IHostTaskManager:: CreateTask](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-createtask-method.md).</span><span class="sxs-lookup"><span data-stu-id="e1f9d-125">The CLR calls `SetCLRTask` to associate an `ICLRTask` instance with the current `IHostTask` instance, which was created by a call to [IHostTaskManager::CreateTask](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-createtask-method.md).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="e1f9d-126">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="e1f9d-126">Requirements</span></span>  
 <span data-ttu-id="e1f9d-127">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="e1f9d-127">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="e1f9d-128">**Header:** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="e1f9d-128">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="e1f9d-129">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="e1f9d-129">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="e1f9d-130">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="e1f9d-130">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="e1f9d-131">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="e1f9d-131">See Also</span></span>  
 [<span data-ttu-id="e1f9d-132">ICLRTask-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="e1f9d-132">ICLRTask Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)  
 [<span data-ttu-id="e1f9d-133">ICLRTaskManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="e1f9d-133">ICLRTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)  
 [<span data-ttu-id="e1f9d-134">IHostTask-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="e1f9d-134">IHostTask Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)  
 [<span data-ttu-id="e1f9d-135">IHostTaskManager-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="e1f9d-135">IHostTaskManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)