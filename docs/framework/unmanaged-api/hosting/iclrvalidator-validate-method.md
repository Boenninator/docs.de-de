---
title: ICLRValidator::Validate-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRValidator.Validate
api_location: mscoree.dll
api_type: COM
f1_keywords: ICLRValidator::Validate
helpviewer_keywords:
- Validate method, ICLRValidator interface [.NET Framework hosting]
- ICLRValidator::Validate method [.NET Framework hosting]
ms.assetid: 0b1b432a-d234-4002-839b-81366c3a8bdc
topic_type: apiref
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 50915201b6e57bd116b80f067f01b8862372bc5b
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="iclrvalidatorvalidate-method"></a><span data-ttu-id="1a403-102">ICLRValidator::Validate-Methode</span><span class="sxs-lookup"><span data-stu-id="1a403-102">ICLRValidator::Validate Method</span></span>
<span data-ttu-id="1a403-103">Überprüft die Datei (portable Executable) oder Microsoft intermediate Language (MSIL) in der angegebenen Datei.</span><span class="sxs-lookup"><span data-stu-id="1a403-103">Validates the portable executable (PE) or Microsoft intermediate language (MSIL) in the specified file.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="1a403-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="1a403-104">Syntax</span></span>  
  
```  
HRESULT Validate (  
    [in] IVEHandler        *veh,  
    [in] unsigned long      ulAppDomainId,  
    [in] unsigned long      ulFlags,  
    [in] unsigned long      ulMaxError,  
    [in] unsigned long      token,  
    [in] LPWSTR             fileName,  
    [in, size_is(ulSize)] BYTE *pe,  
    [in] unsigned long      ulSize  
);      
```  
  
#### <a name="parameters"></a><span data-ttu-id="1a403-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="1a403-105">Parameters</span></span>  
 `veh`  
 <span data-ttu-id="1a403-106">[in] Ein Zeiger auf eine `IVEHandler` -Instanz, die Validierungsfehler behandelt.</span><span class="sxs-lookup"><span data-stu-id="1a403-106">[in] A pointer to an `IVEHandler` instance that handles validation errors.</span></span>  
  
 `ulAppDomainId`  
 <span data-ttu-id="1a403-107">[in] Der Bezeichner für die aktuelle <xref:System.AppDomain>.</span><span class="sxs-lookup"><span data-stu-id="1a403-107">[in] The identifier for the current <xref:System.AppDomain>.</span></span>  
  
 `ulFlags`  
 <span data-ttu-id="1a403-108">[in] Eine Kombination von [ValidatorFlags](../../../../docs/framework/unmanaged-api/hosting/validatorflags-enumeration.md) Werte, der angibt, welche Art von Validierung, die ausgeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="1a403-108">[in] A combination of [ValidatorFlags](../../../../docs/framework/unmanaged-api/hosting/validatorflags-enumeration.md) values, indicating the kind of validation that should be performed.</span></span>  
  
 `ulMaxError`  
 <span data-ttu-id="1a403-109">[in] Die maximale Anzahl von Fehlern, um zuzulassen, bevor Sie die Überprüfung beendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="1a403-109">[in] The maximum number of errors to allow before exiting the validation.</span></span>  
  
 `token`  
 <span data-ttu-id="1a403-110">[in] Wird nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="1a403-110">[in] Unused.</span></span>  
  
 `fileName`  
 <span data-ttu-id="1a403-111">[in] Der Name der Datei, die überprüft werden.</span><span class="sxs-lookup"><span data-stu-id="1a403-111">[in] The name of the file to be validated.</span></span>  
  
 `pe`  
 <span data-ttu-id="1a403-112">[in] Ein Zeiger auf die Dateipuffer.</span><span class="sxs-lookup"><span data-stu-id="1a403-112">[in] A pointer to the file buffer.</span></span>  
  
 `ulSize`  
 <span data-ttu-id="1a403-113">[in] Die Größe in Bytes der Datei überprüft werden.</span><span class="sxs-lookup"><span data-stu-id="1a403-113">[in] The size, in bytes, of the file to be validated.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="1a403-114">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="1a403-114">Return Value</span></span>  
  
|<span data-ttu-id="1a403-115">HRESULT</span><span class="sxs-lookup"><span data-stu-id="1a403-115">HRESULT</span></span>|<span data-ttu-id="1a403-116">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1a403-116">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="1a403-117">S_OK</span><span class="sxs-lookup"><span data-stu-id="1a403-117">S_OK</span></span>|<span data-ttu-id="1a403-118">`Validate`wurde erfolgreich zurückgegeben.</span><span class="sxs-lookup"><span data-stu-id="1a403-118">`Validate` returned successfully.</span></span>|  
|<span data-ttu-id="1a403-119">HOST_E_CLRNOTAVAILABLE ZURÜCK</span><span class="sxs-lookup"><span data-stu-id="1a403-119">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="1a403-120">Die common Language Runtime (CLR) wurde nicht in einen Prozess geladen, oder die CLR wird in einem Zustand, in dem er nicht verwalteten Code ausführen oder den Aufruf erfolgreich verarbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="1a403-120">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="1a403-121">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="1a403-121">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="1a403-122">Der Aufruf ist ein Timeout aufgetreten.</span><span class="sxs-lookup"><span data-stu-id="1a403-122">The call timed out.</span></span>|  
|<span data-ttu-id="1a403-123">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="1a403-123">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="1a403-124">Der Aufrufer ist nicht Besitzer der Sperre.</span><span class="sxs-lookup"><span data-stu-id="1a403-124">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="1a403-125">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="1a403-125">HOST_E_ABANDONED</span></span>|<span data-ttu-id="1a403-126">Ein Ereignis wurde abgebrochen, während ein blockierten Thread oder eine Fiber darauf gewartet.</span><span class="sxs-lookup"><span data-stu-id="1a403-126">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="1a403-127">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="1a403-127">E_FAIL</span></span>|<span data-ttu-id="1a403-128">Ein Unbekannter Schwerwiegender Fehler aufgetreten ist.</span><span class="sxs-lookup"><span data-stu-id="1a403-128">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="1a403-129">Wenn eine Methode E_FAIL zurückgibt, ist die CLR nicht mehr verwendbar innerhalb des Prozesses.</span><span class="sxs-lookup"><span data-stu-id="1a403-129">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="1a403-130">Nachfolgende Aufrufe zum Hosten der Methoden HOST_E_CLRNOTAVAILABLE zurück.</span><span class="sxs-lookup"><span data-stu-id="1a403-130">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="1a403-131">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="1a403-131">Requirements</span></span>  
 <span data-ttu-id="1a403-132">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="1a403-132">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="1a403-133">**Header:** IValidator.idl, IValidator.h</span><span class="sxs-lookup"><span data-stu-id="1a403-133">**Header:** IValidator.idl, IValidator.h</span></span>  
  
 <span data-ttu-id="1a403-134">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="1a403-134">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="1a403-135">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="1a403-135">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="1a403-136">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="1a403-136">See Also</span></span>  
 [<span data-ttu-id="1a403-137">ICLRValidator-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="1a403-137">ICLRValidator Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrvalidator-interface.md)