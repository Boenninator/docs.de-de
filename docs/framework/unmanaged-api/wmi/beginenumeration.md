---
title: BeginEnumeration-Funktion (Referenz zur nicht verwalteten API)
description: "Die BeginEnumeration-Funktion setzt einen Enumerator zurück, auf den Anfang der enumeration"
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: BeginEnumeration
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: BeginEnumeration
helpviewer_keywords: BeginEnumeration function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 12a742774bff22030bdfaaa34e431059e016a4bf
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="beginenumeration-function"></a><span data-ttu-id="ce222-103">BeginEnumeration-Funktion</span><span class="sxs-lookup"><span data-stu-id="ce222-103">BeginEnumeration function</span></span>
<span data-ttu-id="ce222-104">Setzt einen Enumerator zurück an den Anfang der Enumeration zurück.</span><span class="sxs-lookup"><span data-stu-id="ce222-104">Resets an enumerator back to the beginning of the enumeration.</span></span>  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="ce222-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="ce222-105">Syntax</span></span>  
  
```  
HRESULT BeginEnumeration (
   [in] int               vFunc, 
   [in] IWbemClassObject* ptr, 
   [in] LONG              lEnumFlags
); 
```  

## <a name="parameters"></a><span data-ttu-id="ce222-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="ce222-106">Parameters</span></span>

`vFunc`  
<span data-ttu-id="ce222-107">[in] Dieser Parameter wird nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="ce222-107">[in] This parameter is unused.</span></span>

<span data-ttu-id="ce222-108">`ptr`[in] Ein Zeiger auf ein [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) Instanz.</span><span class="sxs-lookup"><span data-stu-id="ce222-108">`ptr` [in] A pointer to an [IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) instance.</span></span>

`lEnumFlags`  
<span data-ttu-id="ce222-109">[in] Eine bitweise Kombination der Flags oder Werte, die in beschriebenen der ["Hinweise"](#remarks) Abschnitt, der steuert, in der Enumeration enthaltenen Eigenschaften.</span><span class="sxs-lookup"><span data-stu-id="ce222-109">[in] A bitwise combination of the flags or values described in the [Remarks](#remarks) section that controls the properties included in the enumeration.</span></span>

## <a name="return-value"></a><span data-ttu-id="ce222-110">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="ce222-110">Return value</span></span>

<span data-ttu-id="ce222-111">Die folgenden Werte, die von dieser Funktion zurückgegebenen werden definiert, der *WbemCli.h* Header-Datei, oder Sie können diese definieren als Konstanten in Ihrem Code:</span><span class="sxs-lookup"><span data-stu-id="ce222-111">The following values returned by this function are defined in the *WbemCli.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="ce222-112">Konstante</span><span class="sxs-lookup"><span data-stu-id="ce222-112">Constant</span></span>  |<span data-ttu-id="ce222-113">Wert</span><span class="sxs-lookup"><span data-stu-id="ce222-113">Value</span></span>  |<span data-ttu-id="ce222-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce222-114">Description</span></span>  |
|---------|---------|---------|
|`WBEM_E_INVALID_PARAMETER` | <span data-ttu-id="ce222-115">0 x 80041008</span><span class="sxs-lookup"><span data-stu-id="ce222-115">0x80041008</span></span> | <span data-ttu-id="ce222-116">Die Kombination der Flags `lEnumFlags` ist ungültig, oder ein ungültiges Argument wurde angegeben.</span><span class="sxs-lookup"><span data-stu-id="ce222-116">The combination of flags in `lEnumFlags` is invalid, or an invalid argument was specified.</span></span> |
|`WBEM_E_UNEXPECTED` | <span data-ttu-id="ce222-117">0x8004101d</span><span class="sxs-lookup"><span data-stu-id="ce222-117">0x8004101d</span></span> | <span data-ttu-id="ce222-118">Einen zweiten Aufruf von `BeginEnumeration` wurde versucht, ohne einen zwischenzeitlichen Aufruf von [ `EndEnumeration` ](endenumeration.md).</span><span class="sxs-lookup"><span data-stu-id="ce222-118">A second call to `BeginEnumeration` was made without an intervening call to [`EndEnumeration`](endenumeration.md).</span></span> |
|`WBEM_E_OUT_OF_MEMORY` | <span data-ttu-id="ce222-119">0x80041006</span><span class="sxs-lookup"><span data-stu-id="ce222-119">0x80041006</span></span> | <span data-ttu-id="ce222-120">Es ist nicht genügend Arbeitsspeicher verfügbar, um eine neue Enumeration zu beginnen.</span><span class="sxs-lookup"><span data-stu-id="ce222-120">Not enough memory is available to begin a new enumeration.</span></span> |
|`WBEM_S_NO_ERROR` | <span data-ttu-id="ce222-121">0</span><span class="sxs-lookup"><span data-stu-id="ce222-121">0</span></span> | <span data-ttu-id="ce222-122">Der Funktionsaufruf war erfolgreich.</span><span class="sxs-lookup"><span data-stu-id="ce222-122">The function call was successful.</span></span>  |
  
## <a name="remarks"></a><span data-ttu-id="ce222-123">Hinweise</span><span class="sxs-lookup"><span data-stu-id="ce222-123">Remarks</span></span>

<span data-ttu-id="ce222-124">Diese Funktion dient als Wrapper für einen Aufruf der [IWbemClassObject::BeginEnumeration](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) Methode.</span><span class="sxs-lookup"><span data-stu-id="ce222-124">This function wraps a call to the [IWbemClassObject::BeginEnumeration](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx) method.</span></span>

<span data-ttu-id="ce222-125">Die Flags, die als übergeben werden können die `lEnumFlags` Argument definiert werden, der *WbemCli.h* Header-Datei, oder Sie können diese definieren als Konstanten in Ihrem Code.</span><span class="sxs-lookup"><span data-stu-id="ce222-125">The flags that can be passed as the `lEnumFlags` argument are defined in the *WbemCli.h* header file, or you can define them as constants in your code.</span></span>  <span data-ttu-id="ce222-126">Sie können einen Flag aus jeder Gruppe mit einem Flag aus einer anderen Gruppe kombinieren.</span><span class="sxs-lookup"><span data-stu-id="ce222-126">You can combine one flag from each group with any flag from any other group.</span></span> <span data-ttu-id="ce222-127">Es gibt jedoch Flags aus der gleichen Gruppe sich gegenseitig ausschließende.</span><span class="sxs-lookup"><span data-stu-id="ce222-127">However, flags from the same group are mutually exclusive.</span></span> 

<span data-ttu-id="ce222-128">**Gruppe 1**</span><span class="sxs-lookup"><span data-stu-id="ce222-128">**Group 1**</span></span>

|<span data-ttu-id="ce222-129">Konstante</span><span class="sxs-lookup"><span data-stu-id="ce222-129">Constant</span></span>  |<span data-ttu-id="ce222-130">Wert</span><span class="sxs-lookup"><span data-stu-id="ce222-130">Value</span></span>  |<span data-ttu-id="ce222-131">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce222-131">Description</span></span>  |
|---------|---------|---------|
|`WBEM_FLAG_KEYS_ONLY` | <span data-ttu-id="ce222-132">0 x 4</span><span class="sxs-lookup"><span data-stu-id="ce222-132">0x4</span></span> | <span data-ttu-id="ce222-133">Schließen Sie die Eigenschaften, die nur den Schlüssel bilden.</span><span class="sxs-lookup"><span data-stu-id="ce222-133">Include properties that constitute the key only.</span></span> |
|`WBEM_FLAG_REFS_ONLY` | <span data-ttu-id="ce222-134">0 x 8</span><span class="sxs-lookup"><span data-stu-id="ce222-134">0x8</span></span> | <span data-ttu-id="ce222-135">Schließen Sie die Eigenschaften, die nur Objektverweise sind.</span><span class="sxs-lookup"><span data-stu-id="ce222-135">Include properties that are object references only.</span></span> |

<span data-ttu-id="ce222-136">**Gruppe 2**</span><span class="sxs-lookup"><span data-stu-id="ce222-136">**Group 2**</span></span>

<span data-ttu-id="ce222-137">Konstante</span><span class="sxs-lookup"><span data-stu-id="ce222-137">Constant</span></span>  |<span data-ttu-id="ce222-138">Wert</span><span class="sxs-lookup"><span data-stu-id="ce222-138">Value</span></span>  |<span data-ttu-id="ce222-139">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce222-139">Description</span></span>  |
|---------|---------|---------|
|`WBEM_FLAG_SYSTEM_ONLY` | <span data-ttu-id="ce222-140">0 x 30</span><span class="sxs-lookup"><span data-stu-id="ce222-140">0x30</span></span> | <span data-ttu-id="ce222-141">Die Enumeration, die nur Systemeigenschaften zu beschränken.</span><span class="sxs-lookup"><span data-stu-id="ce222-141">Limit the enumeration to system properties only.</span></span> |
|`WBEM_FLAG_NONSYSTEM_ONLY` | <span data-ttu-id="ce222-142">0 x 40</span><span class="sxs-lookup"><span data-stu-id="ce222-142">0x40</span></span> | <span data-ttu-id="ce222-143">Enthalten Sie lokale und verteilten Eigenschaften, aber schließen Sie Systemeigenschaften aus der Enumeration aus.</span><span class="sxs-lookup"><span data-stu-id="ce222-143">Include local and propagated properties but exclude system properties from the enumeration.</span></span> |

<span data-ttu-id="ce222-144">Für Klassen:</span><span class="sxs-lookup"><span data-stu-id="ce222-144">For classes:</span></span>

<span data-ttu-id="ce222-145">Konstante</span><span class="sxs-lookup"><span data-stu-id="ce222-145">Constant</span></span>  |<span data-ttu-id="ce222-146">Wert</span><span class="sxs-lookup"><span data-stu-id="ce222-146">Value</span></span>  |<span data-ttu-id="ce222-147">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce222-147">Description</span></span>  |
|---------|---------|---------|
|`WBEM_FLAG_CLASS_OVERRIDES_ONLY` | <span data-ttu-id="ce222-148">0 x 100</span><span class="sxs-lookup"><span data-stu-id="ce222-148">0x100</span></span> | <span data-ttu-id="ce222-149">Begrenzen Sie die Enumeration, die Eigenschaften, die in der Klassendefinition überschrieben.</span><span class="sxs-lookup"><span data-stu-id="ce222-149">Limit the enumeration to properties overridden in the class definition.</span></span> |
|`WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` | <span data-ttu-id="ce222-150">0 x 100</span><span class="sxs-lookup"><span data-stu-id="ce222-150">0x100</span></span> | <span data-ttu-id="ce222-151">Begrenzen Sie die Enumeration, um Eigenschaften, die in der aktuellen Klassendefinition überschrieben und neue Eigenschaften, die in der Klasse definiert.</span><span class="sxs-lookup"><span data-stu-id="ce222-151">Limit the enumeration to properties overridden in the current class definition and to new properties defined in the class.</span></span> |
| `WBEM_MASK_CLASS_CONDITION` | <span data-ttu-id="ce222-152">0x300</span><span class="sxs-lookup"><span data-stu-id="ce222-152">0x300</span></span> | <span data-ttu-id="ce222-153">Ein zu maskieren (statt ein Flag) anzuwendende gegen eine `lEnumFlags` Wert, wenn entweder überprüfen `WBEM_FLAG_CLASS_OVERRIDES_ONLY` oder `WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="ce222-153">A mask (rather than a flag) to apply against a `lEnumFlags` value to check if either `WBEM_FLAG_CLASS_OVERRIDES_ONLY` or `WBEM_FLAG_CLASS_LOCAL_AND_OVERRIDES` is set.</span></span> |
| `WBEM_FLAG_LOCAL_ONLY` | <span data-ttu-id="ce222-154">0 x 10</span><span class="sxs-lookup"><span data-stu-id="ce222-154">0x10</span></span> | <span data-ttu-id="ce222-155">Begrenzen Sie die Enumeration, die Eigenschaften, die definiert, oder in die Klasse selbst nicht geändert werden.</span><span class="sxs-lookup"><span data-stu-id="ce222-155">Limit the enumeration to properties that are defined or modified in the class itself.</span></span> |
| `WBEM_FLAG_PROPAGATED_ONLY` |  <span data-ttu-id="ce222-156">0 x 20</span><span class="sxs-lookup"><span data-stu-id="ce222-156">0x20</span></span> | <span data-ttu-id="ce222-157">Begrenzen Sie die Enumeration, die Eigenschaften, die Basis-Klassen geerbt werden.</span><span class="sxs-lookup"><span data-stu-id="ce222-157">Limit the enumeration to properties that are inherited from base classes.</span></span> |

<span data-ttu-id="ce222-158">Für Instanzen:</span><span class="sxs-lookup"><span data-stu-id="ce222-158">For instances:</span></span>

<span data-ttu-id="ce222-159">Konstante</span><span class="sxs-lookup"><span data-stu-id="ce222-159">Constant</span></span>  |<span data-ttu-id="ce222-160">Wert</span><span class="sxs-lookup"><span data-stu-id="ce222-160">Value</span></span>  |<span data-ttu-id="ce222-161">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ce222-161">Description</span></span>  |
|---------|---------|---------|
| `WBEM_FLAG_LOCAL_ONLY` | <span data-ttu-id="ce222-162">0 x 10</span><span class="sxs-lookup"><span data-stu-id="ce222-162">0x10</span></span> | <span data-ttu-id="ce222-163">Begrenzen Sie die Enumeration, die Eigenschaften, die definiert, oder in die Klasse selbst nicht geändert werden.</span><span class="sxs-lookup"><span data-stu-id="ce222-163">Limit the enumeration to properties that are defined or modified in the class itself.</span></span> |
| `WBEM_FLAG_PROPAGATED_ONLY` |  <span data-ttu-id="ce222-164">0 x 20</span><span class="sxs-lookup"><span data-stu-id="ce222-164">0x20</span></span> | <span data-ttu-id="ce222-165">Begrenzen Sie die Enumeration, die Eigenschaften, die Basis-Klassen geerbt werden.</span><span class="sxs-lookup"><span data-stu-id="ce222-165">Limit the enumeration to properties that are inherited from base classes.</span></span> |


## <a name="requirements"></a><span data-ttu-id="ce222-166">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="ce222-166">Requirements</span></span>  
 <span data-ttu-id="ce222-167">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ce222-167">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="ce222-168">**Header:** WMINet_Utils.idl</span><span class="sxs-lookup"><span data-stu-id="ce222-168">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="ce222-169">**.NET Framework-Versionen:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="ce222-169">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ce222-170">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="ce222-170">See also</span></span>  
[<span data-ttu-id="ce222-171">WMI und Leistungsindikatoren (Referenz zur nicht verwalteten API)</span><span class="sxs-lookup"><span data-stu-id="ce222-171">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)