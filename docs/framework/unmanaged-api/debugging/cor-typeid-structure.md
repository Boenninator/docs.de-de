---
title: COR_TYPEID-Struktur
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: COR_TYPEID
api_location: mscordbi.dll
api_type: COM
f1_keywords: COR_TYPEID
helpviewer_keywords: COR_TYPEID structure [.NET Framework debugging]
ms.assetid: 1e172b14-ee22-4943-b3b8-3740e7bdcd2e
topic_type: apiref
caps.latest.revision: "5"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 795dea77ac8dac1e1d22574c23f1e1c13344a71a
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="cortypeid-structure"></a><span data-ttu-id="4b15c-102">COR_TYPEID-Struktur</span><span class="sxs-lookup"><span data-stu-id="4b15c-102">COR_TYPEID Structure</span></span>
<span data-ttu-id="4b15c-103">Enthält einen Typbezeichner.</span><span class="sxs-lookup"><span data-stu-id="4b15c-103">Contains a type identifier.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="4b15c-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="4b15c-104">Syntax</span></span>  
  
```  
typedef struct COR_TYPEID{  
    UINT64 token1;  
    UINT64 token2;  
} COR_TYPEID;  
```  
  
## <a name="members"></a><span data-ttu-id="4b15c-105">Member</span><span class="sxs-lookup"><span data-stu-id="4b15c-105">Members</span></span>  
  
|<span data-ttu-id="4b15c-106">Member</span><span class="sxs-lookup"><span data-stu-id="4b15c-106">Member</span></span>|<span data-ttu-id="4b15c-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="4b15c-107">Description</span></span>|  
|------------|-----------------|  
|`token1`|<span data-ttu-id="4b15c-108">Das erste Token.</span><span class="sxs-lookup"><span data-stu-id="4b15c-108">The first token.</span></span>|  
|`token2`|<span data-ttu-id="4b15c-109">Das zweite-Token.</span><span class="sxs-lookup"><span data-stu-id="4b15c-109">The second token.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="4b15c-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="4b15c-110">Remarks</span></span>  
 <span data-ttu-id="4b15c-111">Die `COR_TYPEID` Struktur zurückgegeben wird, um eine Anzahl von debugging-Methoden, die Informationen zu Objekten, das speicherbereinigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="4b15c-111">The `COR_TYPEID` structure is returned by a number of debugging methods that provide information about objects to be garbage-collected.</span></span> <span data-ttu-id="4b15c-112">Sie können dann als Argument an anderen Debuggen-Methoden übergeben werden, die zusätzliche Informationen zu dem Element bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="4b15c-112">It can then be passed as an argument to other debugging methods that provide additional information about that item.</span></span> <span data-ttu-id="4b15c-113">Z. B. durch aufzählen einer [ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md) -Objekt, Sie können einzelne abrufen [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) Objekte, die einzelnen Objekte im verwalteten Heap darstellen.</span><span class="sxs-lookup"><span data-stu-id="4b15c-113">For example, by enumerating an [ICorDebugHeapEnum](../../../../docs/framework/unmanaged-api/debugging/icordebugheapenum-interface.md) object, you can retrieve individual [COR_HEAPOBJECT](../../../../docs/framework/unmanaged-api/debugging/cor-heapobject-structure.md) objects that represent individual objects on the managed heap.</span></span> <span data-ttu-id="4b15c-114">Sie können dann übergeben der `COR_TYPEID` Wert aus der `COR_HEAPOBJECT.type` -Feld der [icordebugprocess5:: Gettypefortypeid](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypefortypeid-method.md) Methode, um ein ICorDebugType abzurufen, die zu dem Objekt bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="4b15c-114">You can then pass the `COR_TYPEID` value from the `COR_HEAPOBJECT.type` field to the [ICorDebugProcess5::GetTypeForTypeID](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypefortypeid-method.md) method to retrieve an ICorDebugType object that provides type information about the object.</span></span>  
  
 <span data-ttu-id="4b15c-115">Ein `COR_TYPEID` -Objekt ist dazu gedacht, nicht transparent sein.</span><span class="sxs-lookup"><span data-stu-id="4b15c-115">A `COR_TYPEID` object is intended to be opaque.</span></span> <span data-ttu-id="4b15c-116">Die einzelne Felder sollten nicht zugegriffen oder bearbeitet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="4b15c-116">Its individual fields should not be accessed or manipulated.</span></span> <span data-ttu-id="4b15c-117">Die alleinige Verwendung wird als ein Bezeichner, der als bereitgestellt wird ein `out` Parameter im Aufruf einer Methode und diese kann wiederum weitere Methoden zum Bereitstellen zusätzlicher Informationen übergeben.</span><span class="sxs-lookup"><span data-stu-id="4b15c-117">Its sole use is as an identifier that is provided as an `out` parameter in a method call and that can, in turn, be passed to other methods to provide additional information.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="4b15c-118">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="4b15c-118">Requirements</span></span>  
 <span data-ttu-id="4b15c-119">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="4b15c-119">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="4b15c-120">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="4b15c-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="4b15c-121">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="4b15c-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="4b15c-122">**.NET Framework-Versionen:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="4b15c-122">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="4b15c-123">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="4b15c-123">See Also</span></span>  
 [<span data-ttu-id="4b15c-124">Debuggen von Strukturen</span><span class="sxs-lookup"><span data-stu-id="4b15c-124">Debugging Structures</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)  
 [<span data-ttu-id="4b15c-125">Debuggen</span><span class="sxs-lookup"><span data-stu-id="4b15c-125">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)