---
title: ICorDebugType::EnumerateTypeParameters-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugType.EnumerateTypeParameters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::EnumerateTypeParameters
helpviewer_keywords:
- EnumerateTypeParameters method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::EnumerateTypeParameters method [.NET Framework debugging]
ms.assetid: 1ee1f6e6-1bd7-4ebb-83b8-ff9a08ca03de
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 12b002aaad65fd5f2a1207700c8de2ca8dd60eec
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33421878"
---
# <a name="icordebugtypeenumeratetypeparameters-method"></a>ICorDebugType::EnumerateTypeParameters-Methode
Ruft einen Schnittstellenzeiger auf eine ICorDebugTypeEnum, die enthält die <xref:System.Type> Parameter von der Klasse, die dieser ICorDebugType verweist.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT EnumerateTypeParameters (  
    [out] ICorDebugTypeEnum   **ppTyParEnum  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `ppTyParEnum`  
 [out] Ein Zeiger auf die Adresse einer `ICorDebugTypeEnum` , die die Parameter des Typs enthält.  
  
## <a name="remarks"></a>Hinweise  
 Können Sie `EnumerateTypeParameters` , wenn der CorElementType-durch Rückgabewert [ICorDebugType:: GetType](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-gettype-method.md) ELEMENT_TYPE_CLASS, ELEMENT_TYPE_VALUETYPE, einem, ELEMENT_TYPE_SZARRAY, ELEMENT_TYPE_BYREF, ELEMENT_TYPE_ ist PTR oder ELEMENT_TYPE_FNPTR. Die Anzahl von Parametern und deren Reihenfolge hängt vom Typ:  
  
-   ELEMENT_TYPE_CLASS oder ELEMENT_TYPE_VALUETYPE: die Anzahl von Typparametern, die in enthaltenen der `ICorDebugTypeEnum` , dass diese Methode zurückgibt, hängt die Anzahl der formalen Parameter für die entsprechende Klasse. Z. B., wenn der Typ ist `class Dict<String,int32>`, klicken Sie dann `EnumerateTypeParameters` zurück ein `ICorDebugTypeEnum` , die Objekte, die darstellt enthält `String` und `int32` nacheinander.  
  
-   ELEMENT_TYPE_FNPTR: Die Anzahl von Typparametern, die in enthaltenen der `ICorDebugTypeEnum` ist um eins größer als die Anzahl von Argumenten akzeptiert, die von der Funktion. Der erste Typparameter, der in enthalten die `ICorDebugTypeEnum` ist der Rückgabetyp für die Funktion und die nachfolgenden Typparameter sind den Funktionsparametern.  
  
-   Einem ELEMENT_TYPE_SZARRAY, ELEMENT_TYPE_BYREF oder ELEMENT_TYPE_PTR: ein Typparameter wird zurückgegeben. Angenommen, wenn der Typ ein Arraytyp ist, z. B. `int32[]`,`EnumerateTypeParameters` zurück ein `ICorDebugTypeEnum` , enthält ein Objekt darstellt, `int32`.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
