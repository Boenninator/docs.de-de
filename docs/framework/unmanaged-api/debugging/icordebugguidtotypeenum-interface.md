---
title: ICorDebugGuidToTypeEnum-Schnittstelle
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugGuidToTypeEnum
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugGuidToTypeEnum
helpviewer_keywords: ICorDebugGuidToTypeEnum interface [.NET Framework debugging]
ms.assetid: aa32b12b-05fc-4ea8-a904-adae25034269
topic_type: apiref
caps.latest.revision: "6"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: e419c61d2918a1f17c0739c9782472f25dfe8cfa
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugguidtotypeenum-interface"></a><span data-ttu-id="a51cc-102">ICorDebugGuidToTypeEnum-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="a51cc-102">ICorDebugGuidToTypeEnum Interface</span></span>
<span data-ttu-id="a51cc-103">Stellt einen Enumerator, der definiert die Zuordnung zwischen einem Satz von GUIDs und die zugehörigen Typen, die von Instanzen ICorDebugType dargestellt werden.</span><span class="sxs-lookup"><span data-stu-id="a51cc-103">Provides an enumerator that defines the mapping between a set of GUIDs and their corresponding types, which are represented by ICorDebugType instances.</span></span> <span data-ttu-id="a51cc-104">Diese Schnittstelle erbt die Methoden von ICorDebugEnum-Schnittstelle.</span><span class="sxs-lookup"><span data-stu-id="a51cc-104">This interface inherits the methods from the ICorDebugEnum interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="a51cc-105">Methoden</span><span class="sxs-lookup"><span data-stu-id="a51cc-105">Methods</span></span>  
  
|<span data-ttu-id="a51cc-106">Methode</span><span class="sxs-lookup"><span data-stu-id="a51cc-106">Method</span></span>|<span data-ttu-id="a51cc-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a51cc-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="a51cc-108">Icordebugguidtotypeenum:: Next</span><span class="sxs-lookup"><span data-stu-id="a51cc-108">ICorDebugGuidToTypeEnum::Next</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugguidtotypeenum-next-method.md)|<span data-ttu-id="a51cc-109">Ruft die angegebene Anzahl von [CorDebugGuidToTypeMapping](../../../../docs/framework/unmanaged-api/debugging/cordebugguidtotypemapping-structure.md) Instanzen, die GUIDs für die Typinformationen zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="a51cc-109">Gets the specified number of [CorDebugGuidToTypeMapping](../../../../docs/framework/unmanaged-api/debugging/cordebugguidtotypemapping-structure.md) instances that map GUIDs to type information.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="a51cc-110">Hinweise</span><span class="sxs-lookup"><span data-stu-id="a51cc-110">Remarks</span></span>  
 <span data-ttu-id="a51cc-111">Ein `ICorDebugGuidToTypeEnum` -Schnittstellenobjekt abgerufen werden kann, durch Aufrufen der [icordebugappdomain3:: Getcachedwinrttypes](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-getcachedwinrttypes-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="a51cc-111">An `ICorDebugGuidToTypeEnum` interface object can be retrieved by calling the [ICorDebugAppDomain3::GetCachedWinRTTypes](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-getcachedwinrttypes-method.md) method.</span></span> <span data-ttu-id="a51cc-112">Ein Debugger kann diese Schnittstelle aufrufen [Weiter](../../../../docs/framework/unmanaged-api/debugging/icordebugguidtotypeenum-next-method.md) -Methode abrufen [CorDebugGuidToTypeMapping](../../../../docs/framework/unmanaged-api/debugging/cordebugguidtotypemapping-structure.md) verwalteten Darstellungen von Objekten, die Zuordnungen von darstellen [!INCLUDE[wrt](../../../../includes/wrt-md.md)] geladene Typen der die Anwendungsdomäne für den Aufruf von verwendet die [icordebugappdomain3:: Getcachedwinrttypes](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-getcachedwinrttypes-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="a51cc-112">A debugger can call this interface's [Next](../../../../docs/framework/unmanaged-api/debugging/icordebugguidtotypeenum-next-method.md) method to retrieve [CorDebugGuidToTypeMapping](../../../../docs/framework/unmanaged-api/debugging/cordebugguidtotypemapping-structure.md) objects that represent mappings of managed representations of [!INCLUDE[wrt](../../../../includes/wrt-md.md)] types loaded in the application domain used for the call to the [ICorDebugAppDomain3::GetCachedWinRTTypes](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-getcachedwinrttypes-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="a51cc-113">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="a51cc-113">Requirements</span></span>  
 <span data-ttu-id="a51cc-114">**Plattformen:**[!INCLUDE[wrt](../../../../includes/wrt-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a51cc-114">**Platforms:** [!INCLUDE[wrt](../../../../includes/wrt-md.md)]</span></span>  
  
 <span data-ttu-id="a51cc-115">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="a51cc-115">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="a51cc-116">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="a51cc-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="a51cc-117">**.NET Framework-Versionen:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="a51cc-117">**.NET Framework Versions:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="a51cc-118">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="a51cc-118">See Also</span></span>  
 [<span data-ttu-id="a51cc-119">Debugschnittstellen</span><span class="sxs-lookup"><span data-stu-id="a51cc-119">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)